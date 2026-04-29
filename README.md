# Poco-F1-Dual-Boot-Nethunter-Pro-Android-13
This repo helps you to install Nethunter Pro on Poco F1 alongside Android 13 in dual boot mode.
# Poco F1: Kali NetHunter Pro Installation Guide (Android 13) 🛡️

This project is part of a video series on running a full Kali NetHunter Pro environment on the Poco F1. 

### ⚡ Phase 1: Installation & Setup
In this phase, we focus on:
- Identifying hardware (Display Panel).
- Backing up critical partitions (Boot, DTBO).
- Preparing the SD Card for RootFS.
- First-time boot via TWRP.

### 📋 Commands for Phase 1:

**1. Display Check:**
`cat /proc/cmdline | grep -i "dsi"`

**2. Backup Current OS:**
`dd if=/dev/block/by-name/boot of=/sdcard/android_boot.img`
`dd if=/dev/block/by-name/dtbo of=/sdcard/android_dtbo.img`

---
**🚀 Coming Soon:** Phase 2 - Automated OS Switching Scripts (No Laptop Needed). Stay tuned for the update!
