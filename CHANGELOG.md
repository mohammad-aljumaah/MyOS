# Changelog

All notable changes to MyOS will be documented in this file.

## [Unreleased]
- (nothing yet)

## [0.1.0] - 2026-07-08
### Added
- Boot sector program (stage-1): loaded by BIOS at 0x7C00
- Segment and stack setup (ds, es, ss, sp)
- `puts` routine - prints null-terminated strings via BIOS `int 0x10`
- Build system: Makefile producing a 1.44 MB floppy image
- Run target: boots the image in QEMU
