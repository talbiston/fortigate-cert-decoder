# FortiGate Certificate Decoder PyPI Package

This document explains how to build, install, and publish the FortiGate Certificate Decoder package to PyPI.

## Package Structure

```
certificate/
├── fortigate_cert_decoder/
│   ├── __init__.py
│   └── cert_decode.py
├── setup.py
├── pyproject.toml
├── requirements.txt
├── MANIFEST.in
├── LICENSE
└── README.md
```

## Installation from PyPI

Once published, users can install the package with:

```bash
pip install fortigate-cert-decoder
```

## Usage After Installation

After installation, the tool is available as a command-line utility:

```bash
# Basic usage
fgt-cert-decode 192.168.1.1 MyCert -p "password"

# CA certificate (default)
fgt-cert-decode 10.0.0.1 Fortinet_CA -p "pass123"

# Local certificate
fgt-cert-decode 172.16.0.1 WebCert -t local -p "secret"

# With custom username
fgt-cert-decode 192.168.1.1 SSLCert -u admin -p "admin123"
```

## Development Installation

For local development and testing:

### 1. Install in Editable Mode

```bash
cd fortigate-cert-decoder
pip install -e .
```

This installs the package in development mode, allowing you to make changes without reinstalling.

### 2. Test the Installation

```bash
fgt-cert-decode --help
```

## Building the Package

### 1. Install Build Tools

```bash
pip install build twine
```

### 2. Build Distribution Files

```bash
cd fortigate-cert-decoder
python -m build
```

This creates:
- `dist/fortigate_cert_decoder-1.0.0.tar.gz` (source distribution)
- `dist/fortigate_cert_decoder-1.0.0-py3-none-any.whl` (wheel distribution)

### 3. Verify the Build

```bash
twine check dist/*
```

## Publishing to PyPI

### Test PyPI (Recommended First)

1. Create account at https://test.pypi.org/account/register/

2. Create API token at https://test.pypi.org/manage/account/token/

3. Upload to Test PyPI:
```bash
twine upload --repository testpypi dist/*
```

4. Test installation from Test PyPI:
```bash
pip install --index-url https://test.pypi.org/simple/ fortigate-cert-decoder
```

### Production PyPI

#### Manual Upload (Using Twine)

1. Create account at https://pypi.org/account/register/

2. Create API token at https://pypi.org/manage/account/token/

3. Upload to PyPI:
```bash
twine upload dist/*
```

#### Automated Upload (Using GitHub Actions)

The repository includes a GitHub Actions workflow that automatically publishes to PyPI when you create a GitHub Release.

**Prerequisites:**
1. Create a PyPI account at https://pypi.org/account/register/
2. Configure PyPI Trusted Publishing:
   - Go to https://pypi.org/manage/account/publishing/
   - Add a new pending publisher with:
     - PyPI Project Name: `fortigate-cert-decoder`
     - Owner: `talbiston`
     - Repository: `fortigate-cert-decoder`
     - Workflow name: `python-publish.yml`
     - Environment name: `pypi`

**To publish a new version:**
1. Update version numbers in:
   - `setup.py`
   - `pyproject.toml`
   - `fortigate_cert_decoder/__init__.py`
2. Commit and push your changes
3. Create a new release on GitHub:
   - Go to https://github.com/talbiston/fortigate-cert-decoder/releases/new
   - Create a new tag (e.g., `v1.0.0`)
   - Set the release title (e.g., `Release 1.0.0`)
   - Add release notes
   - Click "Publish release"
4. The GitHub Actions workflow will automatically:
   - Build the package
   - Publish to PyPI
   - Update the deployment status

**Note:** The first time you publish, you need to manually create the project on PyPI or configure Trusted Publishing as described above.

## Configuration

### PyPI Credentials (~/.pypirc)

Create `~/.pypirc` to store credentials:

```ini
[distutils]
index-servers =
    pypi
    testpypi

[pypi]
username = __token__
password = pypi-YOUR-API-TOKEN-HERE

[testpypi]
username = __token__
password = pypi-YOUR-TEST-API-TOKEN-HERE
```

**Security Note**: Use API tokens instead of passwords. Never commit `.pypirc` to version control!

## Version Management

Update version in both files when releasing:
- `setup.py`: `version="1.0.0"`
- `pyproject.toml`: `version = "1.0.0"`
- `fortigate_cert_decoder/__init__.py`: `__version__ = "1.0.0"`

## Before Publishing Checklist

- [ ] Update version number in all files
- [ ] Update README.md with any new features
- [ ] Update author name and email in setup.py and pyproject.toml
- [ ] Update GitHub URLs in setup.py and pyproject.toml
- [ ] Test locally: `pip install -e .`
- [ ] Build package: `python -m build`
- [ ] Check package: `twine check dist/*`
- [ ] Test on Test PyPI first
- [ ] Add git tag for version: `git tag v1.0.0`

## Updating the Package

When releasing a new version:

1. Make your changes
2. Update version numbers
3. Clean old builds:
   ```bash
   rm -rf dist/ build/ *.egg-info
   ```
4. Build new distribution:
   ```bash
   python -m build
   ```
5. Upload to PyPI:
   ```bash
   twine upload dist/*
   ```

## Package Metadata

You should customize these fields in `setup.py` and `pyproject.toml`:

- `author`: Your name
- `author_email`: Your email
- `url`: GitHub repository URL
- `project_urls`: Bug tracker and source URLs

## Dependencies

The package will automatically install these dependencies:
- `requests>=2.28.0`
- `cryptography>=41.0.0`
- `rich>=13.0.0`
- `urllib3>=1.26.0`

## License

The package uses MIT License. Update the LICENSE file with your name and year.

## Troubleshooting

### Import Errors

If you get import errors after installation:
```bash
pip uninstall fortigate-cert-decoder
pip cache purge
pip install fortigate-cert-decoder
```

### Build Errors

Clean build artifacts:
```bash
rm -rf build/ dist/ *.egg-info fortigate_cert_decoder.egg-info
```

### Command Not Found

Ensure pip's bin directory is in your PATH:
```bash
export PATH="$HOME/.local/bin:$PATH"
```

Or use:
```bash
python -m fortigate_cert_decoder.cert_decode --help
```

## Quick Start Commands

```bash
# Navigate to package directory
cd fortigate-cert-decoder

# Install build tools
pip install build twine

# Build the package
python -m build

# Check the package
twine check dist/*

# Upload to Test PyPI
twine upload --repository testpypi dist/*

# Test installation
pip install --index-url https://test.pypi.org/simple/ fortigate-cert-decoder

# If all looks good, upload to production PyPI
twine upload dist/*
```

## Example Usage After Installation

```python
# Can also be used as a Python module
from fortigate_cert_decoder import decode_certificate

decode_certificate(
    host="192.168.1.1",
    cert_name="MyCert",
    username="jsonadmin",
    password="mypass",
    cert_type="ca"
)
```

---

**Remember**: Always test on Test PyPI before publishing to production PyPI!
