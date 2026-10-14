# File Forge 1.0 known issues

- The executable is not Authenticode-signed, so Windows SmartScreen may warn on
  first launch.
- Aurora maintains its own database and artwork cache. Replacing a package with
  the same identity may require removing the stale Aurora entry before rescanning.
- Multi-disc correction currently relies on explicit `Disc N` text in filenames
  when a game's XEX incorrectly reports every disc as 1 of 1. Stage all discs
  together.
- Embedded package artwork is recovered for Xbox 360 XEX/XDBF titles when the
  resource is present. Artwork failure does not abort conversion.
- Original Xbox image support and hardware compatibility remain less thoroughly
  tested than Xbox 360 ISO input.
- Structural verification cannot prove that a later USB, FTP, or FATX transfer
  completed without corruption.
- GOD-to-XEX HDD fast mode intentionally skips payload SHA-1 verification.
  Corrupted source blocks can therefore be copied to the output; repeat any
  suspicious result with verification enabled.
- Generated-GOD fast mode intentionally skips the final full output read-back.
  Required GOD hashes are still created and structural checks still run, but a
  storage write error can go undetected until the package is read or launched.
