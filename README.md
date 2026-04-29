# Poco-F1-Dual-Boot-Nethunter-Pro-Android-13 🛡️
This repo helps you to install Nethunter Pro on Poco F1 alongside Android 13 in dual boot mode.
This project is part of a video series on running a full Kali NetHunter Pro environment on the Poco F1.
### ⚡ Phase 1: Installation & Setup
In this phase, we focus on:
 * Lab Setup
 * Identifying hardware (Display Panel).
 * Backing up critical partitions (Boot, DTBO).
 * Preparing the SD Card for RootFS.
 * Final Touch to Boot to Nethunter Pro.
 * Back to Android.
### 📋 Commands for Phase 1:
```bash
# --- 1. Lab Setup ---
>> sudo apt update
>> sudo apt install adb fastboot -y       # install adb and fastboot drivers
>> sudo apt install 7zip                  # install 7zip
>> sudo apt install make gcc zlib1g-dev   # install simg2img dependencies
>> git clone https://github.com/anestisb/android-simg2img.git
>> cd android-simg2img
>> make
>> sudo cp simg2img /usr/local/bin/
>> sudo cp img2simg /usr/local/bin/

# --- 2. Identifying hardware (Display Panel) ---
>> adb shell su -c "cat /proc/cmdline | grep -i 'dsi'"

# --- 3. Backing up critical partitions (Boot, DTBO) ---
Turn on USB Debugging and Connect PC
>> adb devices
>> adb shell "ls -l /dev/block/by-name | grep -E 'boot|dtbo'"
>> adb shell
>>(beryllium $) su
(Inside Phone)                          # grant superuser request on phone using Magisk
(Back to PC)
>>(beryllium #) dd if=/dev/block/by-name(e.g. sde45) of=/sdcard/boot.img 
>>(beryllium #) dd if=/dev/block/by-name(e.g. sde37) of=/sdcard/dtbo.img 
>>(beryllium #) exit
>>(beryllium $) exit
>> adb pull /sdcard/boot.img ~/Desktop/
>> adb pull /sdcard/dtbo.img ~/Desktop/

# --- 4. Preparing the SD Card for RootFS ---
Download SDM845 file from official site
>> cd Downloads
>> 7z x kali-nethunterpro-2026.1-sdm845.tar.xz
>> 7z x kali-nethunterpro-2026.1-sdm845.tar
>> file nethunterpro-20260320-sdm845-phosh.rootfs.img (Spare Android for EMMC, convert ext4 using simg2img)
>> simg2img nethunterpro-20260320-sdm845-phosh.rootfs.img rootfs_ext4.img
>> lsblk (e.g. sdc)                     # identify the external SDcard 
>> sudo dd if=rootfs_ext4.img of=/dev/sdc bs=1M oflag=sync status=progress
>> sync
# *unplug the SD Card from PC*

# --- 5. Final Touch to boot Nethunter Pro ---
reboot fastboot                           # (Volume Down + Power)
>> fastboot devices
>> fastboot flash boot nethunterpro-20260320-sdm845-phosh.boot-beryllium-tianma.img
>> fastboot erase dtbo (insert rootfs flashed SD Card into ur phone)
>> fastboot reboot

# --- Back to Android ---
Reboot to fastboot                      # (Volume Down + Power)
>> fastboot flash boot boot.img
>> fastboot flash dtbo dtbo.img
>> fastboot reboot
```
**🚀 Coming Soon:** Phase 2 - Automated OS Switching Scripts (No Laptop Needed). Stay tuned for the update!
 
