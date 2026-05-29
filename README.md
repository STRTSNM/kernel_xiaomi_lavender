## MPTCP enabled kernel for redmi note 7S (lavender), kernel version 4.4.205
> Source from android 13.0 branch of PixelExperience

### Compiling
```bash
$ sudo apt install clang llvm lld gcc-aarch64-linux-gnu gcc-arm-none-eabi
$ make O=out ARCH=arm64 CC=clang lavender_defconfig
$ make O=out ARCH=arm64 CC=clang LLVM=1 LLVM_IAS=1 \
    CROSS_COMPILE=aarch64-linux-gnu- \
    CROSS_COMPILE_ARM32=arm-none-eabi- \
    KCFLAGS="-Wno-error=default-const-init-field-unsafe -Wno-error=default-const-init-var-unsafe -Wno-error=strict-prototypes -Wno-error=implicit-enum-enum-cast -Wno-error=array-parameter" \
    -j$(nproc)
```

### Flashing it
The easiest method i found was to use AIK-Linux to unpack a magisk patched boot.img (The ROM's boot.img did not have a ramdisk so...), replace `split_img/boot.img-kernel` with `Image.gz-dtb` you just compiled.
Repack it with AIK-Linux and use fastboot to flash it : `fastboot flash boot image-new.img`

### Word of Caution
Please have a backup of your working boot.img. If this process fails anywhere, simply boot into fastboot mode and flash your working boot.img with
`fastboot flash boot boot.img`
