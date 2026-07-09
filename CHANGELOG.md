# Changelog

All notable changes to MyOS will be documented in this file.

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
