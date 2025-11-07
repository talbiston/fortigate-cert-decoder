# Publishing Guide

This guide explains how to publish the FortiGate Certificate Decoder package to PyPI.

## Prerequisites

Before publishing, ensure you have:

1. A PyPI account (create at https://pypi.org/account/register/)
2. Configured PyPI Trusted Publishing for automated releases (see below)

## Automated Publishing (Recommended)

The repository uses GitHub Actions to automatically publish to PyPI when you create a release.

### One-Time Setup: Configure PyPI Trusted Publishing

1. Go to https://pypi.org/manage/account/publishing/
2. Click "Add a new pending publisher"
3. Fill in the details:
   - **PyPI Project Name:** `fortigate-cert-decoder`
   - **Owner:** `talbiston`
   - **Repository name:** `fortigate-cert-decoder`
   - **Workflow name:** `python-publish.yml`
   - **Environment name:** `pypi`
4. Click "Add"

### Publishing a New Version

1. **Update version numbers** in all three files:
   - `setup.py` → line 8: `version="X.Y.Z"`
   - `pyproject.toml` → line 7: `version = "X.Y.Z"`
   - `fortigate_cert_decoder/__init__.py` → line 3: `__version__ = "X.Y.Z"`

2. **Commit and push** your changes:
   ```bash
   git add setup.py pyproject.toml fortigate_cert_decoder/__init__.py
   git commit -m "Bump version to X.Y.Z"
   git push
   ```

3. **Create a GitHub Release:**
   - Go to https://github.com/talbiston/fortigate-cert-decoder/releases/new
   - **Choose a tag:** Create a new tag `vX.Y.Z` (e.g., `v1.0.0`)
   - **Release title:** `Release X.Y.Z` or `vX.Y.Z`
   - **Description:** Add release notes describing what's new
   - Click **"Publish release"**

4. **Monitor the workflow:**
   - Go to https://github.com/talbiston/fortigate-cert-decoder/actions
   - The "Upload Python Package" workflow will automatically run
   - Once complete, the package will be available on PyPI

5. **Verify the release:**
   - Visit https://pypi.org/project/fortigate-cert-decoder/
   - Install and test: `pip install fortigate-cert-decoder`

## Manual Publishing (Alternative)

If you prefer to publish manually using Twine:

### 1. Install Build Tools

```bash
pip install build twine
```

### 2. Build the Package

```bash
python -m build
```

This creates distribution files in the `dist/` directory.

### 3. Verify the Build

```bash
twine check dist/*
```

### 4. Upload to PyPI

```bash
twine upload dist/*
```

You'll be prompted for your PyPI username and password (or API token).

## Testing Before Publishing

Always test on Test PyPI first:

1. **Upload to Test PyPI:**
   ```bash
   twine upload --repository testpypi dist/*
   ```

2. **Test installation:**
   ```bash
   pip install --index-url https://test.pypi.org/simple/ fortigate-cert-decoder
   ```

3. **Test the CLI:**
   ```bash
   fgt-cert-decode --help
   ```

## Troubleshooting

### "Package already exists" Error

If you get this error, you've already published this version. You need to:
1. Increment the version number
2. Rebuild the package
3. Upload again

### GitHub Actions Fails

Check the workflow logs at https://github.com/talbiston/fortigate-cert-decoder/actions

Common issues:
- Trusted Publishing not configured correctly
- Version number not updated
- Package build errors

## Version Numbering

Follow [Semantic Versioning](https://semver.org/):
- **MAJOR.MINOR.PATCH** (e.g., 1.2.3)
- **MAJOR:** Breaking changes
- **MINOR:** New features (backward compatible)
- **PATCH:** Bug fixes (backward compatible)

## Checklist Before Publishing

- [ ] All tests pass
- [ ] Version number updated in all 3 files
- [ ] CHANGELOG updated (if you have one)
- [ ] README updated with any new features
- [ ] Tested locally with `python -m build`
- [ ] Tested with `twine check dist/*`
- [ ] Created git tag matching the version
- [ ] Created GitHub Release

## After Publishing

1. Verify the package on PyPI: https://pypi.org/project/fortigate-cert-decoder/
2. Test installation in a fresh environment:
   ```bash
   python -m venv test-env
   source test-env/bin/activate  # On Windows: test-env\Scripts\activate
   pip install fortigate-cert-decoder
   fgt-cert-decode --help
   ```
3. Announce the release (if applicable)

## Additional Resources

- Full PyPI Guide: See `PYPI_GUIDE.md`
- PyPI Documentation: https://packaging.python.org/
- GitHub Actions Workflow: `.github/workflows/python-publish.yml`
