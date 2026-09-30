# driverfetch :3

A tiny hardware-checking helper with a little driver-fetching energy. It scans
PCI devices with `lspci` and also lists USB devices when `lsusb` is available.
Then it suggests graphics and firmware packages and can install them after you
give the go-ahead, nya.

## Package Managers

`driverfetch` reads `/etc/os-release` and picks the native package manager for
these distro families:

- Arch-based: `pacman`
- Debian/Ubuntu-based: `apt-get`
- Fedora/RHEL-based: `dnf`
- openSUSE: `zypper`

If the distro ID is not recognized, it looks for an installed supported
package manager. Package names are translated where mappings are available;
packages without a mapping are skipped. Package availability can vary by distro
release and enabled repositories, so give the suggestions a quick look before
installing, please :3

## Getting Started

Install `pciutils` using the command for your distro family if `lspci` is
missing:

```sh
sudo pacman -S pciutils       # Arch-based
sudo apt-get install pciutils # Debian/Ubuntu-based
sudo dnf install pciutils     # Fedora/RHEL-based
sudo zypper install pciutils  # openSUSE
```

`usbutils` is optional; it adds the USB inventory. From this directory, run:

```sh
chmod +x driverfetch
./driverfetch --dry-run
./driverfetch
```

## Options

- `--dry-run`: scan and show package suggestions without installing anything.
- `--all-open-source`: add the open-source graphics bundle, including AMD/ATI,
  Intel, and Nouveau packages where mappings exist. This is inspired by
  Archinstall's graphics options; it does not install proprietary NVIDIA
  drivers.
- `--yes`: skip the confirmation prompts and install without manager prompts.
- `--help`: show command help, nya.

Most device drivers are already provided by the Linux kernel. NVIDIA packages
are not selected automatically because the right choice depends on GPU
generation and kernel. The open-source bundle can include Nouveau; for other
NVIDIA driver choices, check the [ArchWiki NVIDIA page](https://wiki.archlinux.org/title/NVIDIA)
before installing. Stay cute, stay cautious, and check the package list first ♡