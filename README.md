# driverfetch

`driverfetch` is a small Arch Linux hardware scan and package helper. It shows
PCI devices and, when `usbutils` is installed, USB devices. Its built-in rules
recommend Mesa/Vulkan packages for Intel and AMD graphics and `linux-firmware`
when a PCI network interface is present. It asks before installing packages.

```sh
chmod +x driverfetch
./driverfetch --dry-run
./driverfetch
./driverfetch --all-open-source --dry-run
```

Use `--yes` to skip the install confirmation. `pciutils` is required for the
PCI scan; install it with `sudo pacman -S pciutils` if needed. USB inventory
requires `usbutils`.

`--all-open-source` adds the same open-source graphics package set used by
Archinstall, including AMD/ATI, Intel, and Nouveau packages. Use it when you
want the full graphics bundle rather than only packages selected from detected
hardware. It does not select proprietary NVIDIA drivers.

This intentionally does not select NVIDIA or third-party kernel drivers
automatically. Their correct package depends on GPU generation and kernel.
Review the detected hardware and consult the [ArchWiki NVIDIA page](https://wiki.archlinux.org/title/NVIDIA)
before installing an NVIDIA driver. Most other device drivers are provided
by the Linux kernel and do not need a separate package.