# Changelog

All notable changes to MyOS will be documented in this file.


## [0.4.0] - 2026-07-21
### Added
- Two-stage bootloader: stage 1 loads stage 2 from disk
- Stage 2 entry stub (16-bit asm): sets up stack, calls into C
- First C kernel code — `cstart_` prints via `puts`
- Minimal freestanding headers (stdint.h, stdio.h)
- FAT12 reader prototype in C (tools/) for testing image parsing
- Open Watcom 16-bit toolchain integration (wcc, wlink)
- Linker script: raw binary output, custom entry point, _ENTRY first
### Changed
- Kernel now written in C instead of pure assembly
- Makefile: compiles C with Open Watcom, links with wlink

## [0.3.0] - 2026-07-XX
### Added
- FAT12 filesystem parsing in the bootloader
- Reads BIOS drive parameters (int 13h, ah=08h) instead of trusting formatted values
- Computes root directory location and size from the BPB
- Searches root directory for KERNEL.BIN (repe cmpsb over directory entries)
- Follows the FAT cluster chain to load the kernel (12-bit entry decoding)
- FAT12 reader prototype in C (tools/) to validate the parsing logic
- Loads kernel to 0x2000:0 and jumps to it
### Changed
- Bootloader now locates the kernel as a named file rather than a fixed sector

## [0.2.0] - 2026-07-09
### Added
- FAT12 filesystem header (BPB + EBR) in boot sector
- `lba_to_chs`: LBA to CHS address conversion
- `disk_read`: BIOS int 13h sector reading with 3-attempt retry
- `disk_reset`: disk controller reset between retries
- Error handling: print message, wait for keypress (int 16h), reboot
- Test read: loads sector LBA 1 to 0x7E00
### Changed
- Restructured project: separate `src/bootloader/` and `src/kernel/`
- Makefile: builds proper FAT12 floppy image (mkfs.fat + mcopy), kernel copied as a file

## [0.1.0] - 2026-07-08
### Added
- Boot sector program (stage-1): loaded by BIOS at 0x7C00
- Segment and stack setup (ds, es, ss, sp)
- `puts` routine - prints null-terminated strings via BIOS `int 0x10`
- Build system: Makefile producing a 1.44 MB floppy image
- Run target: boots the image in QEMU
