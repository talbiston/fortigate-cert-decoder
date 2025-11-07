# FortiGate Certificate Decoder PyPI Publishing Guide

This guide explains how to publish the FortiGate Certificate Decoder package to PyPI.

## Prerequisites

1. **PyPI Account**: Create an account at https://pypi.org/account/register/
2. **Test PyPI Account** (recommended for testing): Create an account at https://test.pypi.org/account/register/
3. **GitHub Repository Access**: You need maintainer access to this repository

## Publishing Methods

There are two ways to publish to PyPI:

### Method 1: Automated Publishing via GitHub Actions (Recommended)

This method uses GitHub's trusted publishing (OIDC) - no API tokens needed!

#### Setup Steps:

1. **Configure PyPI Trusted Publisher**:
   - Go to https://pypi.org/manage/account/publishing/
   - Add a new trusted publisher with these details:
     - PyPI Project Name: `fortigate-cert-decoder`
     - Owner: `talbiston`
     - Repository name: `fortigate-cert-decoder`
     - Workflow name: `python-publish.yml`
     - Environment name: `pypi`

2. **Configure GitHub Environment** (Optional but Recommended):
   - Go to your repository Settings → Environments
   - Create a new environment named `pypi`
   - Add protection rules (e.g., require reviewers, deployment branches)

3. **Create a Release**:
   ```bash
   # Tag your release
   git tag v1.0.0
   git push origin v1.0.0
   ```
   
   - Go to https://github.com/talbiston/fortigate-cert-decoder/releases/new
   - Select the tag you just created (v1.0.0)
   - Set the release title (e.g., "v1.0.0 - Initial Release")
   - Add release notes describing the changes
   - Click "Publish release"

4. **Automatic Publishing**:
   - The GitHub Actions workflow will automatically:
     - Build the package
     - Run checks
     - Publish to PyPI
   - Monitor progress at: https://github.com/talbiston/fortigate-cert-decoder/actions

### Method 2: Manual Publishing

If you prefer to publish manually:

#### 1. Install Build Tools

```bash
pip install build twine
```

#### 2. Build the Package

```bash
cd /path/to/fortigate-cert-decoder
python -m build
```

This creates:
- `dist/fortigate-cert-decoder-1.0.0.tar.gz` (source distribution)
- `dist/fortigate_cert_decoder-1.0.0-py3-none-any.whl` (wheel distribution)

#### 3. Verify the Build

```bash
twine check dist/*
```

You should see:
```
Checking dist/fortigate_cert_decoder-1.0.0-py3-none-any.whl: PASSED
Checking dist/fortigate-cert-decoder-1.0.0.tar.gz: PASSED
```

#### 4. Test on Test PyPI (Recommended First)

```bash
# Upload to Test PyPI
twine upload --repository testpypi dist/*

# Test installation from Test PyPI
pip install --index-url https://test.pypi.org/simple/ --no-deps fortigate-cert-decoder
```

#### 5. Publish to Production PyPI

```bash
twine upload dist/*
```

You'll be prompted for your PyPI username and password/token.

## Version Management

Update the version number in these files before each release:
- `pyproject.toml`: `version = "1.0.0"`
- `setup.py`: `version="1.0.0"`
- `fortigate_cert_decoder/__init__.py`: `__version__ = "1.0.0"`

Use semantic versioning (MAJOR.MINOR.PATCH):
- MAJOR: Breaking changes
- MINOR: New features (backward compatible)
- PATCH: Bug fixes

## Pre-Release Checklist

Before publishing a new version:

- [ ] Update version numbers in all files
- [ ] Update CHANGELOG or release notes
- [ ] Ensure all tests pass
- [ ] Build package: `python -m build`
- [ ] Check package: `twine check dist/*`
- [ ] Test on Test PyPI (if using manual method)
- [ ] Create git tag: `git tag v1.0.0`
- [ ] Push tag: `git push origin v1.0.0`
- [ ] Create GitHub release (for automated publishing)

## After Publishing

1. **Verify Installation**:
   ```bash
   pip install fortigate-cert-decoder
   fgt-cert-decode --help
   ```

2. **Check PyPI Page**:
   Visit https://pypi.org/project/fortigate-cert-decoder/

3. **Update Documentation**:
   Ensure README.md has correct installation instructions

## Package Configuration

### pyproject.toml

The package uses modern `pyproject.toml` configuration:
- Build system: setuptools with wheel
- License: MIT (modern SPDX format)
- Entry point: `fgt-cert-decode` command
- Dependencies: requests, cryptography, rich, urllib3

### GitHub URLs

All URLs point to: `https://github.com/talbiston/fortigate-cert-decoder`

## Troubleshooting

### Build Errors

Clean build artifacts and try again:
```bash
rm -rf build/ dist/ *.egg-info
python -m build
```

### Twine Authentication Errors

For manual publishing, create an API token:
1. Go to https://pypi.org/manage/account/token/
2. Create a new API token
3. Use `__token__` as username and the token as password

Or configure `~/.pypirc`:
```ini
[distutils]
index-servers =
    pypi
    testpypi

[pypi]
username = __token__
password = pypi-YOUR-API-TOKEN

[testpypi]
username = __token__
password = pypi-YOUR-TEST-API-TOKEN
```

**Security Note**: Never commit `.pypirc` to version control!

### Package Already Exists

If the version already exists on PyPI:
1. Update the version number in all files
2. Rebuild: `rm -rf dist/ && python -m build`
3. Upload again

### Trusted Publishing Setup Issues

If GitHub Actions fails to publish:
1. Verify PyPI trusted publisher settings match exactly
2. Ensure the GitHub environment name is `pypi`
3. Check that the workflow file is named `python-publish.yml`
4. Review workflow logs for specific errors

## Quick Reference Commands

```bash
# Clean old builds
rm -rf build/ dist/ *.egg-info

# Install build tools
pip install build twine

# Build package
python -m build

# Check package
twine check dist/*

# Upload to Test PyPI
twine upload --repository testpypi dist/*

# Upload to Production PyPI
twine upload dist/*

# Test installation
pip install fortigate-cert-decoder

# Test CLI
fgt-cert-decode --help
```

## Resources

- [PyPI Packaging Guide](https://packaging.python.org/tutorials/packaging-projects/)
- [Trusted Publishing](https://docs.pypi.org/trusted-publishers/)
- [GitHub Actions for Python](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python)
- [Semantic Versioning](https://semver.org/)

## Support

For issues with:
- **This package**: Open an issue at https://github.com/talbiston/fortigate-cert-decoder/issues
- **PyPI**: Check https://status.python.org/ or PyPI help documentation
- **GitHub Actions**: Review workflow logs in the Actions tab
