# Backups folder

This folder stores only backups of the catalog's own generated code and outputs (not upstream repo code or forks). Backups are created by the backup workflow and stored here as snapshots or links to external storage. Do NOT store upstream fork source code here.

Policy (short):
- Frequency: weekly snapshots of generated outputs (index.json, site builds, LLM outputs).
- Retention: last 12 snapshots kept (configurable in workflow).
- Storage: for large backups (archives) consider external storage (S3 / Backblaze / Cloudflare R2).

If you want automatic snapshots in this folder, enable the backup workflow and provide storage credentials (S3 or R2).