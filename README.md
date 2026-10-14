# File Forge

File Forge is a portable Windows utility for converting lawfully obtained Xbox
and Xbox 360 backups between ISO images, Games on Demand packages, and extracted
XEX folders.

## Download

Open the repository's **Releases** page and download
`fileforge-1.0-windows-x64.zip` together with its `.sha256` checksum. Extract
the complete ZIP before running `FileForge.exe`.

File Forge supports:

- ISO to GOD
- XEX folder to GOD
- GOD to XEX folder
- Sequential conversion queues
- Optional full verification passes for faster HDD conversions
- Remembered input and output locations
- Configurable failed-output cleanup
- Automatic multi-disc grouping

File Forge works locally, requires no account, and sends no telemetry.

## Requirements

- Windows 10 or Windows 11, 64-bit
- A JTAG/RGH environment configured to run unsigned or unlicensed content for
  generated GOD packages
- Content that you own or are legally authorized to copy

Generated packages are not Microsoft retail signed and are not expected to run
on an unmodified retail Xbox 360.

## Source and license

File Forge is distributed as closed-source software. It is free for lawful
personal, educational, and other noncommercial use under the included license.
Redistribution, rehosting, resale, sublicensing, and distribution of modified
versions are not permitted without prior written permission from Andrew Mock.

See [LICENSE](LICENSE) for the controlling terms.

## Help and feedback

- [Aurora compatibility and transfer help](docs/AURORA_COMPATIBILITY.md)
- [Known issues](docs/KNOWN_ISSUES.md)
- [Reporting feedback](docs/REPORTING_FEEDBACK.md)
- [Security policy](SECURITY.md)

Do not upload copyrighted game images, GOD payloads, account data, console
keys, or credentials when reporting a problem.

## Support development

If File Forge saved you time or a headache, you can support continued updates
at [ko-fi.com/mockinteractive](https://ko-fi.com/mockinteractive).

File Forge is developed by Andrew Mock and published under Mock Interactive.
It is unofficial and is not affiliated with or endorsed by Microsoft.
