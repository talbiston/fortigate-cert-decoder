# FortiGate Certificate Decoder - Quick Start

## Package is Ready for PyPI! ✅

Your package has been successfully configured and is ready to publish to PyPI.

## What's Configured

- ✅ Package structure with `fortigate_cert_decoder/` module
- ✅ Modern `pyproject.toml` with proper metadata
- ✅ GitHub URLs updated to `talbiston/fortigate-cert-decoder`
- ✅ GitHub Actions workflow for automated publishing
- ✅ MIT License (Todd Albiston)
- ✅ Comprehensive documentation (README.md, PYPI_GUIDE.md)
- ✅ Package tested and validated

## Quick Publish Guide

### Option 1: Automated Publishing via GitHub (Recommended)

This is the easiest and most secure method using GitHub's trusted publishing.

#### Setup (One-time):

1. **Configure PyPI Trusted Publisher**:
   - Go to https://pypi.org/manage/account/publishing/
   - Click "Add a new pending publisher"
   - Fill in:
     - PyPI Project Name: `fortigate-cert-decoder`
     - Owner: `talbiston`
     - Repository: `fortigate-cert-decoder`
     - Workflow name: `python-publish.yml`
     - Environment name: `pypi`
   - Click "Add"

2. **Create a Release on GitHub**:
   ```bash
   # Create and push a tag
   git tag v1.0.0
   git push origin v1.0.0
   ```

3. **Publish the Release**:
   - Go to https://github.com/talbiston/fortigate-cert-decoder/releases/new
   - Select the `v1.0.0` tag
   - Title: "v1.0.0 - Initial Release"
   - Add release notes
   - Click "Publish release"

4. **Automatic Publishing**:
   - The GitHub Actions workflow will automatically build and publish to PyPI
   - Monitor at: https://github.com/talbiston/fortigate-cert-decoder/actions

### Option 2: Manual Publishing

If you prefer manual control:

```bash
# 1. Install tools
pip install build twine

# 2. Build the package
python -m build

# 3. Check the package
twine check dist/*

# 4. Upload to PyPI
twine upload dist/*
# You'll need your PyPI username and API token
```

## Test Installation

After publishing, verify it works:

```bash
# Install from PyPI
pip install fortigate-cert-decoder

# Test the command
fgt-cert-decode --help

# Try with a FortiGate device
fgt-cert-decode 192.168.1.1 MyCertName -p "password"
```

## Version Updates

When releasing new versions:

1. Update version in these files:
   - `pyproject.toml`: `version = "1.0.1"`
   - `setup.py`: `version="1.0.1"`
   - `fortigate_cert_decoder/__init__.py`: `__version__ = "1.0.1"`

2. Create and push a new tag:
   ```bash
   git tag v1.0.1
   git push origin v1.0.1
   ```

3. Create a new release on GitHub (for automated publishing)

## Package URLs

- **GitHub**: https://github.com/talbiston/fortigate-cert-decoder
- **PyPI** (after publishing): https://pypi.org/project/fortigate-cert-decoder/

## Documentation

- **README.md** - Full user documentation with usage examples
- **PYPI_GUIDE.md** - Detailed publishing instructions and troubleshooting
- **This file** - Quick reference for publishing

## Important Files

```
fortigate-cert-decoder/
├── fortigate_cert_decoder/       # Main package
│   ├── __init__.py              # Package version and exports
│   └── cert_decode.py           # Main implementation
├── .github/
│   └── workflows/
│       └── python-publish.yml   # Automated PyPI publishing
├── setup.py                     # Package setup configuration
├── pyproject.toml              # Modern package configuration
├── requirements.txt            # Runtime dependencies
├── MANIFEST.in                 # Distribution file includes
├── LICENSE                     # MIT License
├── README.md                   # User documentation
└── PYPI_GUIDE.md              # Publishing guide
```

## Clean Build

If you need to rebuild:

```bash
# Clean old builds
rm -rf build/ dist/ *.egg-info

# Rebuild
python -m build
```

## Next Steps

1. **Read PYPI_GUIDE.md** for detailed publishing instructions
2. **Choose your publishing method** (automated or manual)
3. **Set up PyPI trusted publisher** (for automated method)
4. **Publish to PyPI**
5. **Test the installation** from PyPI

---

**Your package is ready to publish!** 🚀

For detailed instructions, see [PYPI_GUIDE.md](PYPI_GUIDE.md)
