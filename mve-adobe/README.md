# mve-adobe (Mac Mini worker root)

Mirrors Eddie VM roles: VM = source of truth; this tree = Adobe/GPU execution.

```
queue/incoming   # VM drops job packages here
queue/claimed    # worker single-writer claims
queue/done|failed
results/         # result.json readback for VM
staging/sources  # temp originals (disposable after policy)
staging/proxies  # job proxies
staging/tmp
projects/        # versioned .prproj checkpoints (never overwrite)
exports/         # AME outputs before promote
fixtures/        # Stage 2–4 synthetic tests only
evidence/        # hashes, logs, smoke proofs
worker/bin       # mini_worker + scripts
worker/logs
worker/locks     # advisory single-writer locks
tools/           # helper scripts
```

ffmpeg: `/opt/homebrew/bin/ffmpeg` (source `worker/env.sh` in non-interactive SSH).
Premiere: `/Applications/Adobe Premiere Pro 2026/Adobe Premiere Pro 2026.app`
AME: `/Applications/Adobe Media Encoder 2026/Adobe Media Encoder 2026.app`
