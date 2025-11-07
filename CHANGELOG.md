# Changelog

All notable changes to this project will be documented in this file.

## [1.0.1] - 2025-11-06

### Improved
- **Much cleaner output** - Removed cryptography deprecation warnings
- **Better formatting** - Certificate details now displayed in a formatted table with panel
- **Readable dates** - Dates formatted as "YYYY-MM-DD HH:MM:SS UTC" instead of raw datetime
- **Organized sections** - Subject, Issuer, SANs, and Key Usage shown as bullet lists
- **Human-readable key usage** - Shows "Digital Signature", "Certificate Signing" instead of raw boolean values
- **Better status indicators** - Clear ✓/✗ symbols for valid/invalid status
- **Cleaner subject/issuer** - Displayed as bullet points with attribute names instead of RFC4514 string

### Technical Changes
- Suppressed `CryptographyDeprecationWarning` for cleaner output
- Added Rich table and panel components for better formatting
- Improved certificate attribute parsing
- Better error messages with ✓/✗ symbols

## [1.0.0] - 2025-11-06

### Added
- Initial release
- Support for CA and local certificates
- JSON-RPC API authentication
- Certificate decoding and validation
- Rich terminal output with colors
- Command-line interface
- Comprehensive documentation
