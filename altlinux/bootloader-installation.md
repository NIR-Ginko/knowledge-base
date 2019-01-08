# Bootloader installation

* [Problem](#problem)
* [Solution](#solution)

* * *


## Problem

There is a problem with installing boot loader because ALT Linux
is unable to correctly install EFI boot loader in auto-partitioning
mode so it will boot only in case rescue CD is used.

The problem is ALT Linux installs its UEFI boot loader into
```
FS0:\EFI\altlinux
```
but it does not check if
```
FS0:\EFI\boot
```
is present at all.


## Solution

The solution is pretty simple:
```
FS0:\
cp EFI\altlinux EFI\boot
cp EFI\boot\grubx64.efi EFI\boot\bootx64.efi
```

The main point of frustration that such a simple part of installation
process has not been done yet.

