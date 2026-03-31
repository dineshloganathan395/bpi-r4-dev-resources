# prplOS Build Instructions : prplware-v4.1.0 : BPI-R4

## Overview

This document provides step-by-step instructions to build prplOS image for **Banana Pi R4** using the **prplware-v4.1.0** release.

For detailed instructions on setting up the build environment, refer to the
[Building-prplOS](https://gitlab.com/prpl-foundation/prplos/prplos/-/wikis/Building-prplOS)
page on the official wiki.

Download the patches from:
[prplware-v4.1.0 Patches](https://github.com/dineshloganathan395/bpi-r4-dev-resources/tree/main/prplos/prplware-v4.1.0/patches)
and copy into `~/Downloads/bpi-r4-dev-resources/prplos/prplware-v4.1.0/patches/`.

---

## Step 1 : Initialize prplOS Repository

* Clone prplOS repo and checkout prplware-v4.1.0 release using the below commands

```bash
git clone https://gitlab.com/prpl-foundation/prplos/prplos.git
cd prplos
git checkout prplware-v4.1.0
```

---

## Step 2 : Apply Patches to prplOS

* Apply patches to prplos ToT directory using the below command

```bash
git am ~/Downloads/bpi-r4-dev-resources/prplos/prplware-v4.1.0/patches/prplos/*.patch
```

---

## Step 3 : Configure Target Profile

* Select mtk_filogic target using the below commands respectively

```bash
./scripts/gen_config.py mtk_filogic prpl security
```

---

## Step 4 : Apply Patches to feed_mediatek

* Apply patches to feed_mediatek directory using the below command

```bash
cd feeds/feed_mediatek
git am ~/Downloads/bpi-r4-dev-resources/prplos/prplware-v4.1.0/patches/feed_mediatek/*.patch
cd ../..
```

---

## Step 5 : Build prplOS

* Run the below command to trigger the prplOS build

```bash
make V=e -j$(nproc)
```

---

## Build Artifacts

* **SD Card Image**
  * Image Path - `bin/targets/mediatek/filogic/prplos-mediatek-filogic-bananapi_bpi-r4-sdcard.img.gz`
  * Use this image to flash prplOS onto an SD card and boot BPI-R4 from SD

* **Sysupgrade Image**
  * Image Path - `bin/targets/mediatek/filogic/prplos-mediatek-filogic-bananapi_bpi-r4-squashfs-sysupgrade.itb`
  * Use this image to upgrade an already running prplOS on BPI-R4 via sysupgrade

---

## Upgrade prplOS Image on Banana Pi R4

For instructions on flashing and upgrading the prplOS image on Banana Pi R4, refer to:

[Build and upgrade prplOS on Banana Pi R4](https://dineshloganathan395.github.io/posts/build-and-upgrade-prplos-on-banana-pi-r4/#upgrade-prplos-image-on-banana-pi-r4)
