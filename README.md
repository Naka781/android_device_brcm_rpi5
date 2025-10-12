Raspberry Vanilla AOSP 16 device configuration for Raspberry Pi 5.

Establish Android build environment.

Install additional packages:

sudo apt-get install dosfstools e2fsprogs fdisk kpartx mtools rsync
Initialize repo:
repo init -u https://android.googlesource.com/platform/manifest -b android-15.0.0_r32
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-15.0/manifest_brcm_rpi.xml --create-dirs
Or optionally, you can reduce download size by creating a shallow clone and removing unneeded projects:

repo init -u https://android.googlesource.com/platform/manifest -b android-15.0.0_r32 --depth=1
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-15.0/manifest_brcm_rpi.xml --create-dirs
curl -o .repo/local_manifests/remove_projects.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-15.0/remove_projects.xml
Sync source code:
repo sync
Setup Android build environment:
. build/envsetup.sh
Select the device (rpi4 or rpi5) and build target (tablet UI, tv for Android TV, or car for Android Automotive):
lunch aosp_rpi4-bp1a-userdebug
lunch aosp_rpi4_tv-bp1a-userdebug
lunch aosp_rpi4_car-bp1a-userdebug
lunch aosp_rpi5-bp1a-userdebug
lunch aosp_rpi5_tv-bp1a-userdebug
lunch aosp_rpi5_car-bp1a-userdebug
Compile:

Edit file : 
sudo nano device/brcm/rpi5/audio/audio_hw.c
mmm device/brcm/rpi5/audio -j$(nproc)


make bootimage systemimage vendorimage -j$(nproc)
Make flashable image for the device (rpi4 or rpi5):
./rpi4-mkimg.sh
./rpi5-mkimg.sh
Also look into Linux kernel build instructions.

Issues:
Android
Linux kernel
Wiki:
Audio
DSI display
HDMI display
HDMI-CEC
Interfaces
USB boot
Utilities
Video decoding & encoding




  
