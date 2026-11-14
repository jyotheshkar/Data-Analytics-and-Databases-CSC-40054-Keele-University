# Repository maintenance

This repository preserves individual 2024 MSc coursework plus explicitly labelled 2026 maintenance and migration evidence. Keep the 89% overall module mark distinct from model metrics. Preserve `original-work/` snapshot bytes and manifests. The synthetic `web/` illustration is not the assessed data analysis.

Run `python -m unittest discover -s tests -v` after inspector changes. It uses standard-library fixtures and must pass on Windows and Linux. Close SQLite connections explicitly; the transaction context manager alone does not close them. Keep strict existing-path resolution, read-only SQLite URIs, quoted schema-derived identifiers, bounded export and exclusive output creation.

Never run the mutating notebook against the only database copy. Do not claim notebook/model validation without executing it with a documented input and environment. Avoid adding unlicensed course datasets; the historical KLE input's external licence is unverified. Update evidence hashes and describe redactions accurately when changing `docs/original/` derivatives. Keep student identifiers, transcripts and private source paths out of public files.
