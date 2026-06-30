# Upload Checklist

Use this repository for PIL evidence only.

## Repository Name

```text
wf-rs-c2000-pil-evidence
```

## Repository Description

```text
Processor-in-the-loop evidence for WF-RS autonomous sailing controller execution on a TI C2000 target.
```

## Upload These

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

## Do Not Upload These

```text
firmware/
host/
requirements.txt
SOURCE_CODE_README.md
```

They are optional code/provenance items and are ignored by `.gitignore`.

## If Using Git

Open PowerShell inside this folder:

```powershell
git init
git add .
git commit -m "Add C2000 PIL evidence package"
git branch -M main
git remote add origin https://github.com/<your-user-or-lab>/wf-rs-c2000-pil-evidence.git
git push -u origin main
```

Because `.gitignore` excludes the optional code folders, `git add .` stages only
the evidence package.

## If Using GitHub Web Upload

Drag only the files and folders listed in **Upload These** into the GitHub upload
page.
