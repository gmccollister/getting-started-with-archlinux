# Getting Started With Arch Linux Challenge

## Download, Creation, Booting USB Flash Disk - $20
* Open these tabs in the background:
  * https://wiki.archlinux.org/index.php/GRUB#GUID_Partition_Table_(GPT)_specific_instructions

* Open this tab in the foreground and keep it open for the duration of this step: https://wiki.archlinux.org/index.php/Installation_guide

* Use the provided Arch Linux Laptop to follow the link to the download page and download the .iso and .iso.sig files from a mirror in the "HTTP Direct Downloads" section. Follow instructions on the Installation Guide for verifying the image with pacman-key.

* Insert the USB drive.

* Use the `su` command to switch to root.

* Use the `dmesg` command to find the block device name of the USB flash drive.

* Use the dd command to write the .iso file to the USB flash drive. Change "sdX" to the block device shown by dmesg for the USB flash drive (be very careful not to write over the system's disk, usually /dev/sda).
```dd if=/path/to/archlinux-2019.07.01-x86_64.iso of=/dev/sdX```

* Use the `sync` command to make sure all buffers are written to disk.

* Remove the USB flash drive and use it to boot target machine.

* Continue on from "Boot the live environment" on the Arch Linux Installation Guide but in doing so:

  * Create "UEFI with GPT" partioning using `parted`. set/activate the flag bios_grub on the partition.
  * Make 512 MiB EFI system partition.
  * When creating the root partition as /dev/sdX2 (where X matches the systems installed disk) leave 4 GiB for the swap partition.
  * Create a 4 GiB swap partition as /dev/sdX3.
  * If you don't know how to use `vim` use `nano` to create and edit text files. A [simple guide can be found here](https://www.lifewire.com/beginners-guide-to-nano-editor-3859002).
  * We will install the xfce4 Desktop Environment but there are other [choices](https://wiki.archlinux.org/index.php/Desktop_environment).
  * In addtion to base add the follow (seperated by spaces) when performing `pacstrap`: base-devel, xfce4, xfce4-goodies

* Boot loader
Once you reach the "Boot loader" section of the Installation Guide, refer to the tab you opened in the background earlier: https://wiki.archlinux.org/index.php/GRUB#GUID_Partition_Table_(GPT)_specific_instructions
  * Packages can be installed with `pacman` by doing `pacman -S package_name`. Use this to install `grub`.
  * Follow the instructions for "UEFI systems" on the GRUB wiki page for installing the boot loader to the disk using `grub-install`.
  * Do `grub-mkconfig -o /boot/grub/grub.cfg` to create the the grub configuration file.

* Once grub is installed you can `reboot` the system and remove the USB flash disk.

