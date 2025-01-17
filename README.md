# systemd-boot configuration generator
This project attempts to create the .conf files located in /boot/loader/entries/. It will read two files:

- /etc/os-release - for OS information
- /etc/default/cmdline - kernel parameters

## Configuration
/etc/default/cmdline contains one variable: CMDLINE="", the value of which must be quoted; these are the parameters passed to the kernel at boot.

You must create this file and copy the parameters from grub, or other existing configuration files, before proceeding.

Example:

    CMDLINE="root=UUID=4bd01097-de27-49a3-b6a7-ae60516d1f2c ro rootflags=subvol=root-gentoo resume=UUID=4a6c4856-6dd8-4bab-afcf-a41bdf1c7c33 crypt_root=UUID=c821ecff-229c-4d56-a750-2e1542ea1cdb root_trim=yes intel_iommu=igfx_off keymap=se i915.enable_guc=3 i915.enable_fbc=1 i915.enable_dc=1"

## Installation
    $ cargo install --git https://github.com/rdmartins/systemd-boot-gen

## Dry-Run
You can check the output of the generated files without changing anything on your system using the -d flag:

    $ systemd-boot-gen -d
    
## Running
To generate:

    # systemd-boot-gen

To generate and to remove old or invalid config files, add the -r flag:

    # systemd-boot-gen -r

To generate and include a microcode file, use the -u flag:

    # systemd-boot-gen -u intel-uc.img

The file should be inside **/boot** directory.
