# GitHub Publication Notes

This folder is prepared as a public, evidence-only repository for the embedded
processor-in-the-loop (PIL) validation.

## Repository Name

Use:

```text
wf-rs-c2000-pil-evidence
```

## Repository Description

Use:

```text
Processor-in-the-loop evidence for WF-RS autonomous sailing controller execution on a TI C2000 target.
```

## What To Publish

Publish the evidence files:

```text
README.md
UPLOAD_CHECKLIST.md
MDPI_DATA_AVAILABILITY.md
MANIFEST_SHA256.txt
.gitignore
.gitattributes
docs/
metadata/
results/
```

This is enough to show the PIL claim: host-reference logs, C2000 serial logs,
command-error summaries, figures, implementation notes, source metadata, and
integrity hashes.

## What Not To Publish

Do not publish these folders unless the professor explicitly asks for a code
release:

```text
firmware/
host/
requirements.txt
SOURCE_CODE_README.md
```

The `.gitignore` in this folder already excludes those optional code items, so
`git add .` will stage the evidence-only package.

Do not publish unrelated manuscript drafts, reviewer letters, private notes,
Overleaf archives, Monte Carlo simulation outputs, or MATLAB simulation runners
in this repository.

## Suggested Git Commands

From inside `PIL_GITHUB_RELEASE_2026-06-29/`:

```powershell
git init
git add .
git commit -m "Add C2000 PIL evidence package"
git branch -M main
git remote add origin https://github.com/<your-user-or-lab>/wf-rs-c2000-pil-evidence.git
git push -u origin main
```

If the repository already exists on GitHub, use the existing remote URL in the
`git remote add origin ...` line.

## Suggested Release Tag

After the first upload, create a GitHub release tagged:

```text
v1.0-mdpi-pil-evidence
```

For final publication, archive the GitHub release through Zenodo or an
institutional repository if a DOI is needed.
