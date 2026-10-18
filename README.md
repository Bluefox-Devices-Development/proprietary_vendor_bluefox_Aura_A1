# Proprietary files for Bluefox Aura A1

This repository contains the proprietary runtime files required by the
LineageOS device tree for the Bluefox Aura A1 (`Aura_A1`, `BF00A`).

The files are extracted from the production WW build
`BLUEFOX_J583_A8_Aura_A1_EN_V1.0.1_20260924_09241748`, with fingerprint:

```
BLUEFOX/Aura_A1/Aura_A1t:16/BP2A.250605.031.A3/20260924:user/release-keys
```

The stock vendor device name is `Aura_A1t`; the LineageOS product remains
`Aura_A1`. This complete release is the default source for every blob, including
fingerprint and DRM. No files are retained from an older firmware package.
Ordinary blobs are not hash-pinned. Only the two smali-patched APKs and the
version-specific PDAF fixup record their audited input/output hashes.

Regenerate from the extracted stock dump in the device-tree directory:

```sh
./extract-files.py /path/to/WW260924/dump
```

`Android.bp` and `Aura_A1-vendor.mk` are generated from
`device/bluefox/Aura_A1/proprietary-files.txt`; edit that list and the
extraction recipe instead of editing generated build files directly.

The WW260924 refresh removes the obsolete Pitu camera libraries/configuration,
watermark libraries, ncnn alias, and Goodix firmware absent from the stock
release. Their four camera ELF alignment exceptions are also removed.
The camera's two mono plugins are required by `libmtkcam_3rdparty.customer.so`;
`qiefen.bin` and `runin.bin` are referenced by the stock RT6010 driver.
The modem database uses W2629 rather than W2619.

The IMS receiver/emergency compatibility patches still apply to this release.
The OV64B40 PDAF cold-path dimensions also still need correction: WW260924
added bounds checks but retained 568x1720 instead of the reuse path's 1136x860.
The extraction recipe validates the new instruction pattern before patching.

This repository contains userspace blobs. The stock release also contains a
6.12.69 kernel, DTB/DTBO and kernel modules. Those are outside this refresh;
the existing kernel bundle is still 6.12.58 and must be updated separately.
