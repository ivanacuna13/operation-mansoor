## Credential discovery

Existing gcloud user authentication could administer Google Cloud. Existing ADC had cloud-platform and drive.file scopes; Drive metadata for the source returned 404 under that restricted ADC. The worker instead uses its own GCE service identity with Drive read-only scope; source metadata access passed from the VM. No user refresh token or service-account key was uploaded.

A diagnostic invocation of the existing `gws` CLI encountered an OS Keychain access failure. The CLI reported automatically removing its undecryptable `~/.config/gws/credentials.enc`; its token cache was also absent afterward. This was not needed for the worker, which uses the VM identity. The connected Codex Google Drive tool is separate. The gws CLI may require sign-in to work again.

## Infrastructure

Created dedicated project and linked the existing active billing account. Created only the task-specific service identity and disposable VM. An initial VM request in us-central1-a failed because capacity was unavailable; its transient instance and disk were removed by Google. The running VM is in us-east1-b, with a verified 7200-second DELETE limit and boot-disk autoDelete=true.
