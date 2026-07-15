# Android Reverse Engineering - ADB Discovery Cheatsheet

This repository contains the ADB commands I use to perform the initial inspection of an Android device before attempting any reverse engineering.

> ⚠️ Run these commands at your own risk - read the [disclaimer](../README.md#️-disclaimer--read-this-first) first.

These commands are **read-only**. They shoud **do not modify the device**.

The goal is to gather information such as:

- Device model
- Manufacturer
- SoC
- Kernel version
- Android build
- Bootloader status
- Verified Boot status
- Root availability
- Debug capabilities

---

# Requirements

- Android SDK Platform Tools
- USB Debugging enabled
- ADB authorized on the device

Check the connection:

```bash
adb devices
```

Expected output:

```text
List of devices attached
ABC123456789    device
```

---

# 1. Device Identification

## Model

```bash
adb shell getprop ro.product.model
```

Example:

```text
TK701_EEA
```

---

## Manufacturer

```bash
adb shell getprop ro.product.manufacturer
```

Example:

```text
worldchip
```

---

## Brand

```bash
adb shell getprop ro.product.brand
```

Example:

```text
AEEZO
```

---

## Device Codename

```bash
adb shell getprop ro.product.device
```

Example:

```text
TK701_EEA
```

Useful when searching for:

- GitHub
- Kernel source
- Custom ROMs

---

## Board Name

```bash
adb shell getprop ro.product.board
```

---

## Hardware Platform

```bash
adb shell getprop ro.hardware
```

---

## SoC Platform

Probably the most useful property.

```bash
adb shell getprop ro.board.platform
```

Example:

```text
rk3566
```

Search Google for:

```
rk3566 linux
rk3566 github
rk3566 device tree
rk3566 kernel
rk3566 postmarketos
rk3566 armbian
```

---

# 2. Android Build Information

## Build Fingerprint

```bash
adb shell getprop ro.build.fingerprint
```

Useful for identifying:

- OEM
- Android version
- Firmware

---

## Build ID

```bash
adb shell getprop ro.build.display.id
```

---

## Android Version

```bash
adb shell getprop ro.build.version.release
```

---

## SDK Version

```bash
adb shell getprop ro.build.version.sdk
```

---

# 3. CPU Information

```bash
adb shell cat /proc/cpuinfo
```

Useful for identifying:

- CPU architecture
- cores
- implementer

---

# 4. Kernel Information

```bash
adb shell uname -a
```

Example:

```text
Linux localhost 4.9.170 #1 SMP PREEMPT Tue Nov 23 14:54:27 CST 2021 armv8l
```

---

# 5. Root Detection

## Current User

```bash
adb shell id
```

Example:

```text
uid=2000(shell)
```

Meaning:

Normal ADB shell.

---

## Check for su

```bash
adb shell which su
```

Possible outputs:

```
/system/bin/su
```

or

```
not found
```

---

## Test Root

```bash
adb shell su -c id
```

Expected if rooted:

```text
uid=0(root)
```

If it fails:

The device is probably not rooted.

---

# 6. Security Properties

## Production Build

```bash
adb shell getprop ro.secure
```

Values:

```
1 = production build
0 = engineering build
```

---

## Debuggable Build

```bash
adb shell getprop ro.debuggable
```

Values:

```
0 = normal retail build
1 = engineering/userdebug build
```

---

## Verified Boot

```bash
adb shell getprop ro.boot.verifiedbootstate
```

Possible values:

```
green
yellow
orange
red
```

Meaning:

| Value | Meaning |
|---------|------------------------------|
| green | Verified Boot passed |
| orange | Bootloader unlocked |
| yellow | Verification warning |
| red | Verification failed |

---

## Bootloader Lock State

```bash
adb shell getprop ro.boot.flash.locked
```

Values:

```
1 = locked
0 = unlocked
```

---

# 7. Bootloader Information

Some devices support:

```bash
adb reboot bootloader
```

Once in Fastboot:

```bash
fastboot getvar all
```

or

```bash
fastboot flashing get_unlock_ability
```

**Note**

Some OEMs disable these commands.

---

# 8. Recommended Google Searches

Once you know the SoC:

```
<SoC> linux

<SoC> github

<SoC> kernel

<SoC> device tree

<SoC> uart

<SoC> postmarketos

<SoC> armbian
```

Example:

```
rk3566 github
rk3566 linux
rk3566 uart
```

---

# 9. Firmware Search

Search for:

```
<Model> firmware

<Model> stock ROM

<Model> boot.img

<Model> update.zip

<Model> scatter

<Model> factory image
```

---

# 10. Kernel Source Search

```
<Model> GPL source

<Model> kernel source

<SoC> kernel source
```

Also search GitHub:

```
site:github.com <model>

site:github.com <soc>

site:github.com device_tree
```

---

# Reverse Engineering Workflow

```text
Buy device
        │
        ▼
Identify SoC
        │
        ▼
Check firmware availability
        │
        ▼
Check kernel source
        │
        ▼
Check bootloader
        │
        ▼
Collect ADB clues
        │
        ▼
Search community resources
        │
        ▼
Only then start modifying the device
```

---

# Philosophy

The goal is **not** to immediately root or flash the device.

The goal is to understand what you're working with first.

> Observe first. Modify later.

---

If you found this useful, consider subscribing to my YouTube channel:

**Hack Around**
