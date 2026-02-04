# GitHub Workflows

Automated release workflow for xAI Plus OpenClaw skill.

## Workflow

### release.yaml

Triggers on version tags (e.g., `v1.0.0`).

**Creates:**
- GitHub Release with version info
- `xai-openclaw.zip` (skill package)
- `xai-openclaw.zip.sha256` (checksum for verification)

## Release Process

1. Update CHANGELOG.md with new version
2. Commit changes
3. Create and push tag:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```
4. Workflow automatically creates GitHub Release
5. Download `xai-openclaw.zip` from release page

## Verification

Users can verify download integrity:

```bash
sha256sum -c xai-openclaw.zip.sha256
```

## What's Excluded

The following files/directories are excluded from releases:
- `.git/` - Git repository data
- `.github/` - Workflow files
- `.*` - Hidden files
- `__MACOSX/` - macOS metadata
- `.DS_Store` - macOS folder metadata
