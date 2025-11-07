# FortiGate Certificate Decoder - Quick Start

## Package is Ready! ✅

Your package has been successfully set up and built at:
`/home/albist50/Code/fortigate-cert-decoder`

## What's Included

- ✅ Package structure with `fortigate_cert_decoder/` module
- ✅ Author information updated (Todd Albiston)
- ✅ License updated (MIT - Todd Albiston)
- ✅ Build files configured (`setup.py`, `pyproject.toml`)
- ✅ Package built successfully
- ✅ Comprehensive README.md
- ✅ PyPI publishing guide (PYPI_GUIDE.md)

## Built Files

```
dist/
├── fortigate_cert_decoder-1.0.0-py3-none-any.whl  (wheel distribution)
└── fortigate_cert_decoder-1.0.0.tar.gz            (source distribution)
```

## Next Steps

### 1. Test Locally

```bash
cd /home/albist50/Code/fortigate-cert-decoder

# Install in development mode
pip install -e .

# Test the command
fgt-cert-decode --help

# Try it with a real device
fgt-cert-decode 192.168.1.1 MyCert -p "password"
```

### 2. Publish to Test PyPI (Recommended First)

```bash
# Install twine if you haven't
pip install twine

# Check the package
twine check dist/*

# Upload to Test PyPI
twine upload --repository testpypi dist/*
# You'll need a Test PyPI account: https://test.pypi.org

# Test installation from Test PyPI
pip install --index-url https://test.pypi.org/simple/ fortigate-cert-decoder
```

### 3. Publish to Production PyPI

```bash
# After testing, upload to production PyPI
twine upload dist/*
# You'll need a PyPI account: https://pypi.org
```

## Usage After Installation

Once installed via pip, users can use:

```bash
# Default CA certificate
fgt-cert-decode 192.168.1.1 Fortinet_CA -p "password"

# Local certificate
fgt-cert-decode 10.0.0.1 WebCert -t local -p "password"

# With custom username
fgt-cert-decode 172.16.0.1 SSLCert -u admin -p "admin123"
```

## Important Notes

1. **GitHub URL**: Update the GitHub URLs in `setup.py` and `pyproject.toml` when you create a repository
2. **Version Updates**: When releasing new versions, update version in:
   - `setup.py`
   - `pyproject.toml`
   - `fortigate_cert_decoder/__init__.py`

## File Structure

```
/home/albist50/Code/fortigate-cert-decoder/
├── fortigate_cert_decoder/       # Main package
│   ├── __init__.py              # Package initialization
│   └── cert_decode.py           # Main code
├── dist/                        # Built distributions
├── setup.py                     # Package setup (legacy)
├── pyproject.toml              # Modern package config
├── requirements.txt            # Dependencies
├── MANIFEST.in                 # Distribution files
├── LICENSE                     # MIT License
├── README.md                   # Full documentation
├── PYPI_GUIDE.md              # Publishing guide
└── .gitignore                 # Git ignore rules
```

## Clean Build

If you need to rebuild from scratch:

```bash
cd /home/albist50/Code/fortigate-cert-decoder

# Clean old builds
rm -rf build/ dist/ *.egg-info fortigate_cert_decoder.egg-info

# Rebuild
python3 -m build
```

## Documentation

- **README.md** - Comprehensive user documentation
- **PYPI_GUIDE.md** - Detailed publishing instructions
- **This file** - Quick reference

## Support

For detailed instructions on any step, see:
- Building: Check PYPI_GUIDE.md
- Usage: Check README.md
- Examples: Check README.md

---

**Your package is ready to publish to PyPI!** 🚀
