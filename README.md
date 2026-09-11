# EvolutionX 17 for Motorola Edge 50 (tank)

Unofficial EvolutionX 17.0 (Android 17) builds and sources for **Motorola Edge 50** (`tank`).

---

## 📱 Device Information

| Attribute | Specification |
| :--- | :--- |
| **Device Model** | Motorola Edge 50 |
| **Codename** | `tank` |
| **SoC** | Qualcomm Snapdragon 7s Gen 2 (SM7450 / 4nm) |
| **CPU** | Octa-core (4x 2.40 GHz Cortex-A78 & 4x 1.95 GHz Cortex-A55) |
| **GPU** | Adreno 710 |
| **Display** | 6.7" Curved pOLED, 1.5K (1220 x 2712), 120Hz, HDR10+, 1900 nits peak |
| **Main Camera** | 50 MP (Sony LYT-700C, OIS) + 10 MP (Telephoto, 3x optical zoom, OIS) + 13 MP (Ultrawide/Macro) |
| **Front Camera** | 32 MP |
| **Battery & Charging** | 5000 mAh, 68W TurboPower wired, 15W wireless |
| **Biometrics** | In-Display Optical Fingerprint Sensor (Goodix UDFPS) |
| **Bluetooth / Audio** | Bluetooth 5.2, LDAC (990kbps), aptX HD / Adaptive, LHDC v5 |
| **Storage & RAM** | 256GB / 512GB UFS 2.2, 8GB / 12GB LPDDR4X |

---

## 🛠️ Highlights & Features in this Build

- **Google Apps**: Built-in official Google Apps (GApps) included.
- **Root Options**:
  - **KernelSU-Next Variant**: Pre-integrated with KernelSU-Next (`CONFIG_KSU=y`) + KernelSU Manager companion APK.
  - **Non-Root Variant**: Standard stock-like unrooted kernel (`CONFIG_KSU=n`).
- **Bluetooth Audio Fidelity**:
  - Fixed audio stutters & buffer drops (AAC VBR frame control jitter resolved).
  - High-resolution / Lossless codecs enabled: **LDAC (990 kbps)**, **aptX Adaptive**, and **LHDC v5**.
  - Direct UI shortcuts in **Settings > Connected Devices > Bluetooth** & **Device Details** for Codec, Sample Rate (96kHz), Bit Depth (24/32-bit), and LDAC Quality.
- **Display & Touch**:
  - Double Tap to Wake (DT2W) hardware support fixed and mapped.
  - Smooth 120Hz refresh rate tuning with low-brightness throttling bypass.
- **Filesystem**: Standard RW ext4 (`--flags 3`, dm-verity disabled).

---

## 📦 Local Manifest (`sm7450.xml`)

Save the following local manifest to `.repo/local_manifests/sm7450.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote name="ajimsjames" fetch="https://github.com/ajimsjames" revision="lineage-24" />

  <!-- device -->
  <project name="android_device_motorola_tank" path="device/motorola/tank" remote="ajimsjames" />
  <project name="android_device_motorola_sm7450-common" path="device/motorola/sm7450-common" remote="ajimsjames" />

  <!-- hardware -->
  <project name="android_hardware_motorola" path="hardware/motorola" remote="ajimsjames" />

  <!-- vendor -->
  <project name="proprietary_vendor_motorola_tank" path="vendor/motorola/tank" remote="ajimsjames" />
  <project name="proprietary_vendor_motorola_sm7450-common" path="vendor/motorola/sm7450-common" remote="ajimsjames" />
  
  <!-- kernel -->
  <project name="android_kernel_motorola_sm7450" path="kernel/motorola/sm7450" remote="ajimsjames" />
  <project name="android_kernel_motorola_sm7450-modules" path="kernel/motorola/sm7450-modules" remote="ajimsjames" />
  <project name="android_kernel_motorola_sm7450-devicetrees" path="kernel/motorola/sm7450-devicetrees" remote="ajimsjames" />
</manifest>
```

---

## 🔨 How to Build EvolutionX 17 for Motorola Edge 50 (tank)

### 1. Initialize EvolutionX Source Tree
```bash
# Create working directory
mkdir -p ~/Android/evox17
cd ~/Android/evox17

# Initialize repo
repo init -u https://github.com/Evolution-X/manifest -b vic --git-lfs
```

### 2. Add Local Manifest & Sync
```bash
# Create local manifests folder
mkdir -p .repo/local_manifests

# Place sm7450.xml into .repo/local_manifests/
# (Paste the XML provided above into .repo/local_manifests/sm7450.xml)

# Sync sources
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

### 3. Build the ROM
```bash
# Set up build environment
source build/envsetup.sh

# Lunch target for tank (userdebug)
lunch lineage_tank-cp2a-userdebug

# Start build
m evolution
```

### 4. Flashing Instructions (Sideload)
1. Reboot device to Recovery:
   ```bash
   adb reboot recovery
   ```
2. In Recovery, navigate to **Apply update > Apply from ADB**.
3. Sideload the generated ROM package:
   ```bash
   adb sideload out/target/product/tank/EvolutionX-17.0-*-tank-*.zip
   ```
4. (Optional for clean flash): Perform **Factory Reset / Format Data** in recovery.
5. Reboot system.

---

### 📄 Credits & Sources
- [Evolution-X](https://github.com/Evolution-X)
- [LineageOS](https://github.com/LineageOS)
- Device Maintainer: [ajimsjames](https://github.com/ajimsjames)
