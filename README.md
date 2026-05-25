# GitHub Artifact Attestation Setup

This repository is configured to generate a GitHub **artifact attestation** using `.github/workflows/generate-attestation.yml`.

## 1) Trigger the workflow

- Push to `main`, `master`, or `work`, **or**
- Run it manually from **Actions → Generate artifact attestation → Run workflow**.

The workflow will:
1. create `dist/build-info.txt`,
2. upload it as the `build-output` artifact,
3. generate provenance attestation for that artifact.

## 2) Download attestation JSON locally

After the workflow completes, use GitHub CLI:

```bash
gh attestation verify build-output \
  --repo <OWNER>/<REPO> \
  --format json > attestation.json
```

Then inspect it:

```bash
cat attestation.json | jq .
```

## Notes

- You need GitHub CLI (`gh`) authenticated with access to the repository.
- The `--format json` output is the easiest way to get a local JSON file view of the attestation.
