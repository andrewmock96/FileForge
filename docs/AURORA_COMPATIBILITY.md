# Aurora and RGH compatibility

This note separates three different questions that are easy to confuse when
diagnosing a Games on Demand package.

1. **Can Aurora discover it?** The `LIVE` header, Title ID, content type, path,
   and display metadata must be recognizable.
2. **Is the package internally intact?** The header digest, master/sub hash
   tables, payload hashes, part sizes, allocation count, and XDVDFS extents
   must agree.
3. **Will the Microsoft dashboard authorize it?** An unchanged GOD→XEX→GOD
   round trip can retain its original header and authorization data. A new or
   changed package cannot acquire a Microsoft publisher signature, account
   license, or console license from File Forge.

Aurora seeing a title proves only the first item. File Forge's post-build check
proves the second item. Neither substitutes for the console patch required by
the third item.

## Blank Title ID folder in Aurora's file manager

If Aurora can open `<TitleID>` but shows no `00007000` directory beneath it,
the failure happened during transfer. Aurora has not reached the GOD header
and cannot be rejecting package metadata or payload hashes at that point.

Check the mounted destination on the PC before changing the converter. The
complete destination must contain this tree:

```text
Content/0000000000000000/<TitleID>/00007000/
├── <ContentID>
└── <ContentID>.data/
    ├── Data0000
    ├── Data0001
    └── ...
```

Copy rather than move the package from the PC. For the safest manual install,
copy the `.data` directory and every `DataNNNN` part first, then copy the
extensionless `<ContentID>` header last. A partially copied package therefore
has no discoverable header. Read and verify the destination copy before using
FATXplorer to unmount the volume, and do not disconnect the disk while it is
mounted or while the copy is active.

## “The game couldn't start; try downloading the game again”

Check these in order:

1. Confirm that another known-good GOD game launches from the same device and
   content path. Do not treat DashLaunch `contpatch` as a general GOD fix: its
   documented purpose is patching license bits for add-on (`00000002`) content,
   not Games on Demand (`00007000`) packages.
2. Remove the failed copy before retesting. Copy the complete Title ID folder,
   including the extensionless header and its matching `.data` directory, in
   binary mode. Do not use a cut/move operation. A partial FTP or mounted-drive
   transfer can remain visible in Aurora.
3. Use the conventional path
   `Content/0000000000000000/<TitleID>/00007000/<ContentID>` or configure an
   Aurora scan path that points to the equivalent tree.
4. Rescan or restart Aurora after replacement. Do not mix the header from one
   conversion with the `.data` directory from another.
5. Temporarily disable a title update for the game. A mismatched or damaged
   update can produce the same dashboard message.
6. Test the same legally obtained ISO with established Windows Iso2God. If its
   package launches under the same console configuration but File Forge's does
   not, retain both 44 KiB headers and the File Forge activity log for a
   byte-level compatibility comparison. Do not share copyrighted data parts.

## What File Forge validates

By default, every generated package is read back before success is reported.
The verifier checks all SHA-1 relationships, exact part sizes, the declared
part count, the declared total size, GDF/XDVDFS structure, and the allocated
block count. Optional output fast mode skips the full SHA-1 reread but retains
strict header, part-layout, allocation, and GDF checks. It therefore cannot
detect every storage write error. Neither mode catches an incomplete later
transfer unless verification is run on the transferred copy.

New directory trees use zero for a missing child and store records physically
in prefix order (root, left subtree, right subtree). Source trees preserved by
GOD extraction retain their original links; both zero and `0xFFFF` leaf
sentinels occur in existing images and are accepted by the extractor.

Loose-folder builds advertise complete sector-rounded directory extents,
including the root, matching the `extract-xiso` followed by Iso2God workflow.
Round trips with authenticated layout metadata preserve the source table sizes
and record order instead of inventing replacements.

## Known boundary

File Forge preserves the original package header only when the rebuilt GOD hash
root and all size fields prove the payload is unchanged. If any game file is
changed, File Forge creates an unsigned Iso2God-style header instead of copying
a signature that no longer describes the payload. It does not forge a Microsoft
signature, marketplace entitlement, or console license. A console launch remains
an important acceptance test for each hardware, dashboard, storage, and package.
