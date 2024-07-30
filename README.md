# Ubuntu Images for Mediatek MT8186 Chromebooks

### Warning

All of this is in a very experimental state and not at all
officially supported by Ubuntu.

## Tested Devices

The following chromebooks are known to work:

- ASUS Chromebook CM14
- Lenovo IdeaPad 3 Slim

## Dependencies

The following packages need to be installed:
```
# apt install make sgdisk wget

# snap install --classic ubuntu-image
```

Finally we also need to fetch or build the bootloader binary.
The easiest way to get it is:

```
$ wget -P gadget https://tobhe.de/ubuntu/submarine-a64.kpart -O gadget/
```

## Building

If all the dependencies are in place running the build is as easy as:

```
# ubuntu-image -i 8G chromebook-corsola.yaml
```

In order to make the image bootable on a Chromebook with depthcharge bootloader we
need to set the correct GPT attributes on our kernel boot partition.
This is explained in detail in
[ChromiumOS > Reference > Disk Format](https://www.chromium.org/chromium-os/developer-library/reference/device/disk-format/).

```
# sgdisk -A 1:or:11f000000000000 ubuntu-24.10-preinstall-desktop-arm64+corsola.img
```
