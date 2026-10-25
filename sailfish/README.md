# Sailfish OS bring-up for lemonadep

This directory contains source-sync groundwork for a Sailfish OS adaptation
based on LineageOS 22.2. The `hybris-22.2` manifest in `mer-hybris/android`
uses the LineageOS `lineage-22.2` branch; the local manifest here pins the
device, common device, kernel, and hardware repositories to that branch.

## Sync Android sources

Initialize the Sailfish Android source tree using the HADK instructions and
the `hybris-22.2` branch:

```sh
repo init -u https://github.com/mer-hybris/android.git -b hybris-22.2
mkdir -p .repo/local_manifests
cp /path/to/android_device_oneplus_sm8350-common/sailfish/local_manifests/lemonadep.xml \
    .repo/local_manifests/lemonadep.xml
repo sync
```

The Android device tree refers to proprietary files from OnePlus 9 Pro firmware
`LE2125_14.0.0.1902(EX01)`. Obtain and extract those files according to the
LineageOS device-tree instructions and the HADK; this manifest does not
download proprietary binaries.

## Port status

This is not yet a bootable Sailfish OS port. The Android device and common
trees provide the hardware-specific Android base, but Sailfish adaptation
repositories and outputs are still needed: a hybris-compatible kernel and boot
image, device-specific Droid HAL and configuration packages, and a Sailfish
root filesystem/image configuration. Those components must be built and
validated on the device following the
[Sailfish OS HADK](https://docs.sailfishos.org/Develop/HADK/) and
[Android hardware adaptation guide](https://github.com/mer-hybris/hadk.sailfishos.org/blob/main/docs/android.md).
In particular, display, touch, audio, modem, Wi-Fi/Bluetooth, camera, sensors,
and suspend/resume require device testing; successful LineageOS builds do not
verify them for Sailfish OS.
