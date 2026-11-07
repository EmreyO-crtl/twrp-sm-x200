# TWRP for Samsung Galaxy Tab A8 (2021) – SM-X200 (gta8wifi)

Unofficial TWRP recovery builds for the **Galaxy Tab A8 Wi-Fi (SM-X200)**, built from the official
TeamWin source. This repository is the home of the project: **every new version is published as a
new [release](https://github.com/EmreyO-crtl/twrp-sm-x200/releases)** (new TWRP versions and new
Samsung firmware versions).

### ➡️ [Download the latest version](https://github.com/EmreyO-crtl/twrp-sm-x200/releases/latest)

## Why these builds

Other TWRP builds for this tablet often bootloop the stock Samsung OS (modified vbmeta,
multidisabler, forced Format Data). These builds avoid all of that:

- **Stock vbmeta untouched** – no multidisabler, no forced format, stock Android keeps booting.
- **Stays installed** – Samsung's `install-recovery.sh` normally restores stock recovery on every boot.
  The *PERMANENT* package changes one byte in the **unsigned padding** of the stock boot image, so
  the restore script no longer matches. Boot signature and AVB hash stay unchanged.
- **Touch works** – the Samsung kernel disables touch in recovery; the recovery's kernel copy is
  patched so the Novatek touch driver starts.

## Versions

| Release | TWRP | For firmware | Status |
|---|---|---|---|
| [v1.0-X200XXS6DYG6](https://github.com/EmreyO-crtl/twrp-sm-x200/releases/tag/v1.0-X200XXS6DYG6) | 3.7.1_14 (twrp-14.1) | X200XXS6DYG6 (Android 14) | current |

Release names: `v<build>-<firmware>`. A **PERMANENT** package only matches the firmware in its name
(it contains that firmware's boot image).

## What works (current version)

| Feature | Status |
|---|---|
| Boot, touch, display | ✅ |
| Stays installed, stock OS boots | ✅ |
| ADB (root), MTP | ✅ |
| Backup / restore, ZIP flashing, wipe / format | ✅ |
| Decrypting `/data` (FBE + metadata encryption) | ❌ Samsung keymaster `configure` fails (err -970) |
| Vibration | ❌ |

## Files in each release

| File | Use |
|---|---|
| `TWRP_PERMANENT_SM-X200_<firmware>.tar.md5` | Normal install with Odin (AP): TWRP + boot fix. **Only for that firmware.** |
| `TWRP_RECOVERY_ONLY_SM-X200_<firmware>.tar.md5` | TWRP only, touches nothing else (Samsung replaces it on the next Android boot unless the boot fix is installed). |
| `recovery.img` | Raw recovery image. |

SHA256 checksums are listed in each release.

## Install

1. Bootloader must be **unlocked**.
2. Download mode: tablet off, hold **Vol Up + Vol Down**, plug in USB, press **Vol Up**.
3. Odin → **AP** = `TWRP_PERMANENT_SM-X200_<your firmware>.tar.md5` → Start → PASS.
4. Enter TWRP: tablet off, hold **Vol Up + Power**.

## Do NOT

- Flash any vbmeta / "vbmeta disabled" file.
- Run multidisabler.
- Flash a PERMANENT package made for a different firmware.
- After a Samsung firmware update: don't flash the old PERMANENT package. Use RECOVERY_ONLY and wait
  for (or build) the release for the new firmware.

## Back to stock

Flash your stock firmware (or just its `boot.img` + `recovery.img`) with Odin.

## Credits

TeamWin (TWRP), AOSP. Maintained by EmreyO-crtl, built with help from Claude (Anthropic).

*Use at your own risk. Keep a backup of your EFS and your stock firmware.*
