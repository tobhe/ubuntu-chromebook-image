# Ubuntu Images for arm64 Chromebooks

**Warning:** All of this is in a very experimental state and not at all
officially supported by Ubuntu.

## Tested Devices

The following chromebooks are known to work:

- ASUS Chromebook CM14
- Lenovo IdeaPad 3 Slim

## Dependencies

The following packages need to be installed:
```
# apt install make gdisk wget

# snap install --classic ubuntu-image
```

Finally we also need to fetch or build the bootloader binary.
The easiest way to get it is:

```
$ wget -P gadget https://tobhe.de/ubuntu/submarine-a64.kpart
```

## Building

If all the dependencies are in place running the build is as easy as:

```
# ubuntu-image classic -i 8G chromebook-corsola-desktop.yaml
```

In order to make the image bootable on a Chromebook with depthcharge bootloader we
need to set the correct GPT attributes on our kernel boot partition.
This is explained in detail in
[ChromiumOS > Reference > Disk Format](https://www.chromium.org/chromium-os/developer-library/reference/device/disk-format/).

```
# sgdisk -A 1:or:11f000000000000 ubuntu-24.10-preinstalled-desktop-arm64+corsola.img
```
