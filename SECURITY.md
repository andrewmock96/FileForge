# Security policy

## Supported version

Only the current public release is supported:

| Version | Supported |
|---|---|
| 1.0 | Yes |
| Internal development builds | No |

## Reporting a vulnerability

Report security issues privately to the maintainer through the official File
Forge distribution or repository contact channel. Do not publish exploit
details before the maintainer has had a reasonable opportunity to investigate.

Include the affected version, impact, reproduction steps, and a minimal test
case. Never send commercial game data, console keys, account credentials, or
other secrets.

## Security boundaries

File Forge parses untrusted binary files and writes converted output. Its main
defenses are strict bounds checks, path validation, source/destination
separation, exclusive file creation, GOD hash verification, and final
verification of generated packages.

File Forge does not provide:

- Malware scanning of extracted executables.
- A guarantee that an input game image is authentic or safe to run.
- Encryption, signing, marketplace entitlement, or console authorization.
- Protection against damage caused by disconnecting storage during a write.

Use a dedicated output directory, retain backups of original media, verify
release checksums, and cleanly unmount removable or FATX storage.
