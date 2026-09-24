# Mansoor temporary cloud proxy worker

Created for Ivan's mandatory media access override on 2026-09-09.

First batch completed: all three proxies passed cloud and local verification and were handed off. All staged originals/proxies, both VMs, and both VM disks were deleted. Empty instance and disk inventories are recorded in `cloud-cleanup.json`; full results are in `verification-report.json`. Temporary local capability files were removed. No original camera footage was downloaded locally during this run.

Scope: Take 0006, Take 0007, and The Biggest Lie in Life Insurance. 16x is excluded.

## Deployment

- Google Cloud project: `mansoor-media-20260909`
- VM: `mansoor-proxy-0909`, zone `us-east1-b`
- Machine: `n2-standard-4`; 30 GB boot disk, automatically deleted with the VM
- Automatic VM deletion: two hours after starting; delete earlier when the batch finishes
- Worker identity: `mansoor-proxy@mansoor-media-20260909.iam.gserviceaccount.com`
- OAuth scope: Drive read-only. No Drive writes, user refresh tokens, or service-account keys are needed.
- Original and proxy storage: `/var/tmp/mansoor-media/<job-id>` on the temporary VM only
- API binds to the VM's loopback interface, reached using SSH local forwarding
- Private endpoint capability is in `config.private.json` and `handoff.key`; do not publish these files.

`worker.py` refuses to run outside a Google Compute Engine VM. It downloads originals directly through the authenticated Drive API, transcodes, and verifies before making a proxy available. It never exposes an original download endpoint.

`handoff.py` runs locally. It requests jobs sequentially, downloads only ready verified proxies, checks their SHA-256 and size, probes and fully decodes them, then acknowledges successful handoff. The worker deletes both staged original and proxy before acknowledging deletion. Failed jobs delete their staged media. Abandoned jobs are bounded by VM auto-deletion.

## Proxy specification

H.264, AAC 48 kHz, CFR 30 fps, GOP 30 frames, 720x1280 portrait or 1280x720 landscape. Scaling preserves aspect ratio with padding when necessary. Rotation metadata is considered for orientation. Verification checks dimensions, codecs, duration against the cloud original, all frame timestamps, keyframe intervals, and a complete FFmpeg decode.

Per-proxy manifests record Drive ID, job ID, checksum, local path, duration, dimensions, frame rate, verification, and cloud-media deletion. They are stored beside the proxy. Status and job IDs are logged in `handoff.log`; URLs containing the private capability are not logged there.

## Reuse

The VM is intentionally disposable. `launch.py` provides the complete lifecycle for future batches using the existing dedicated project. Supply a JSON array of objects with `drive_source_id` and an absolute `local_proxy_path`:

```sh
python3 launch.py --sources sources.json
```

The launcher refuses existing destinations, creates a 16-core VM with a two-hour deletion limit, installs dependencies, creates an encrypted tunnel, runs jobs, verifies handoffs, and deletes the VM in a finally block. Its syntax and CLI were checked; the current first batch is exercising the same underlying worker/handoff components through the manual deployment described below.

For manual operation, recreate a VM using `startup.sh`, upload `worker.py` and a fresh `handoff.key`, start the worker via a systemd service with the environment file, and establish an SSH tunnel:

```sh
gcloud compute ssh mansoor-proxy-0909 --project=mansoor-media-20260909 --zone=us-east1-b -- -N -L 18765:127.0.0.1:8765 -o ExitOnForwardFailure=yes
python3 handoff.py --config config.private.json
```

After the batch, delete the VM with `gcloud compute instances delete ... --quiet` and verify both instance and disk inventories are empty. Keep source code and verification records; remove the local capability files.

For the first batch, a second worker, `mansoor-proxy-fast-0909` (`n2-standard-16`, same zone, 30 GB auto-deleting disk, two-hour deletion limit), handles 0007 and Biggest Lie concurrently with the four-core 0006 worker. Its local SSH port is 18766.

## Final rendering

This is the proxy acquisition worker, not a completed Premiere cloud conform system. Proxies are for editorial decisions only. Final rendering requires an explicit original-source conform in the cloud with the Premiere edit translated or run in a compatible renderer. Do not call proxy exports final-resolution masters or silently download originals to relink locally.
