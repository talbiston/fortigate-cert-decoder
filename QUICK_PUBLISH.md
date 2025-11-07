# Quick Publishing Reference

## To Publish a New Version to PyPI

### Option 1: Automated via GitHub Release (Recommended)

1. Update version in these 3 files:
   - `setup.py` (line 8)
   - `pyproject.toml` (line 7)
   - `fortigate_cert_decoder/__init__.py` (line 3)

2. Commit and push:
   ```bash
   git add setup.py pyproject.toml fortigate_cert_decoder/__init__.py
   git commit -m "Bump version to X.Y.Z"
   git push
   ```

3. Create a GitHub Release at:
   https://github.com/talbiston/fortigate-cert-decoder/releases/new
   - Tag: `vX.Y.Z`
   - Title: `Release X.Y.Z`
   - Description: Release notes

4. The package will automatically publish to PyPI!

### Option 2: Manual Publishing

```bash
# Build the package
python -m build

# Check the package
twine check dist/*

# Upload to PyPI
twine upload dist/*
```

## First Time Setup

Before publishing for the first time, configure PyPI Trusted Publishing:

1. Go to: https://pypi.org/manage/account/publishing/
2. Add pending publisher:
   - Project: `fortigate-cert-decoder`
   - Owner: `talbiston`
   - Repository: `fortigate-cert-decoder`
   - Workflow: `python-publish.yml`
   - Environment: `pypi`

## Verify After Publishing

```bash
# Install from PyPI
pip install fortigate-cert-decoder

# Test the CLI
fgt-cert-decode --help
```

## Links

- PyPI Project: https://pypi.org/project/fortigate-cert-decoder/
- GitHub Actions: https://github.com/talbiston/fortigate-cert-decoder/actions
- Full Guide: See `PUBLISHING.md`
