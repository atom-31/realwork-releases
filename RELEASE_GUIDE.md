# GitHub CLI Release Guide

This guide covers how to create releases and upload files using the GitHub CLI (`gh`) instead of manual browser uploads.

## Prerequisites

Make sure you have GitHub CLI installed and authenticated:
```bash
gh auth status
```

## Creating a New Release

### 1. Create a Draft Release
```bash
gh release create v3.0.13 --draft --title "Realwork v3.0.13" --notes "Release notes here"
```

### 2. Create a Release with Files (All in One Command)
```bash
gh release create v3.0.13 \
  --title "Realwork v3.0.13" \
  --notes "Release notes here" \
  --draft \
  Realwork-3.0.13.dmg \
  Realwork-3.0.13.zip
```

### 3. Create a Pre-release
```bash
gh release create v3.0.13-beta \
  --title "Realwork v3.0.13 Beta" \
  --notes "Beta release notes" \
  --prerelease \
  Realwork-3.0.13-beta.dmg \
  Realwork-3.0.13-beta.zip
```

## Managing Existing Releases

### List All Releases
```bash
gh release list
```

### View Release Details
```bash
gh release view v3.0.12
```

### Upload Files to Existing Release
```bash
gh release upload v3.0.12 Realwork-3.0.12.dmg Realwork-3.0.12.zip
```

### Edit Release Details
```bash
gh release edit v3.0.12 --title "New Title" --notes "Updated notes"
```

### Publish a Draft Release
```bash
gh release edit v3.0.12 --draft=false
```

### Delete Release Assets
```bash
gh release delete-asset v3.0.12 Realwork-3.0.12.dmg
```

### Delete Entire Release
```bash
gh release delete v3.0.12 --yes
```

## Common Workflows

### Complete Release Process
1. **Create draft release with files:**
   ```bash
   gh release create v3.0.13 \
     --title "Realwork v3.0.13" \
     --notes "$(cat CHANGELOG.md)" \
     --draft \
     Realwork-3.0.13.dmg \
     Realwork-3.0.13.zip
   ```

2. **Review the draft release:**
   ```bash
   gh release view v3.0.13
   ```

3. **Publish when ready:**
   ```bash
   gh release edit v3.0.13 --draft=false
   ```

### Upload Multiple Files Pattern
```bash
# For current directory with version pattern
VERSION="3.0.13"
gh release upload v${VERSION} Realwork-${VERSION}.dmg Realwork-${VERSION}.zip
```

### Generate Release Notes from Commits
```bash
gh release create v3.0.13 \
  --title "Realwork v3.0.13" \
  --generate-notes \
  --draft \
  Realwork-3.0.13.dmg \
  Realwork-3.0.13.zip
```

## Tips

- **Always create drafts first** to review before publishing
- **Use consistent naming** for version tags (e.g., `v3.0.13`)
- **Include both DMG and ZIP** files for macOS releases
- **Test downloads** from the draft release before publishing
- **Use `--generate-notes`** to auto-generate release notes from commits
- **File uploads are much faster** via CLI than browser