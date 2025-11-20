# bl_sbx-WithOptions
## itunesstored & bookassetd Sandbox Escape

This repository contains a proof-of-concept demonstrating how maliciously crafted `downloads.28.sqlitedb` and `BLDatabaseManager.sqlite` databases can escape the sandbox of **itunesstored** and **bookassetd** on iOS. By abusing their download mechanisms, the POC enables writing arbitrary `mobile`-owned files to restricted locations in `/private/var/`, including MobileGestalt cache files—allowing device modifications such as spoofing the device type.

### Key Points
- Compatible with iOS **26.2b1 and below** (tested on iPhone 12, iOS 26.0.1).
- **Stage 1 (itunesstored):** Delivers a crafted `BLDatabaseManager.sqlite` to a writable container.
- **Stage 2 (bookassetd):** Downloads attacker-controlled EPUB payloads to arbitrary file paths.
- Writable paths include:
  - `/private/var/containers/Shared/SystemGroup/.../Library/Caches/`
  - `/private/var/mobile/Library/FairPlay/`
  - `/private/var/mobile/Media/`
- Demonstrates modifying `com.apple.MobileGestalt.plist` to validate successful exploitation.

### Outcome
iOS fails to block crafted download tasks, allowing unauthorized file writes unless the target path requires `root` ownership (or the fileowner is not `mobile`).

**Check the blogpost for more information**

### Disclaimer
This project is for **educational purposes only**.  
Do **not** use it for illegal activities.  
Apple may patch this behavior at any time.
