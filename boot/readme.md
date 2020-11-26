Modifying the installation medium to boot on 32-bit UEFI

Yes, some genius came up with the idea to put a 32-bit UEFI on a 64-bit device. The Linux kernel shipped with Ubuntu 14.10 supports mixed-mode, so kernel-wise it is no longer a problem. But the Ubuntu 14.10 (Vivid Vervid) ISO does not contain a 32-bit bootloader. Luckily this can be easily fixed.

    Get a bootia32.efi file, I used this one from John Wells.
    Copy the file into the EFI/BOOT/ folder on the boot medium.


32-bit efi for Asus T100
========================

To generate this file yourself, do the following on any computer:

$ sudo apt-get install git bison libopts25 libselinux1-dev autogen m4 autoconf help2man libopts25-dev flex libfont-freetype-perl automake autotools-dev libfreetype6-dev texinfo

$ git clone git://git.savannah.gnu.org/grub.git

$ cd grub

$ ./autogen.sh

$ export EFI_ARCH=i386

$ ./configure --with-platform=efi --target=${EFI_ARCH} --program-prefix=""

$ make

$ cd grub-core

$ ../grub-mkimage -d . -o bootia32.efi -O i386-efi -p /boot/grub ntfs hfs appleldr boot cat efi_gop efi_uga elf fat hfsplus iso9660 linux keylayouts memdisk minicmd part_apple ext2 extcmd xfs xnu part_bsd part_gpt search search_fs_file chain btrfs loadbios loadenv lvm minix minix2 reiserfs memrw mmap msdospart scsi loopback normal configfile gzio all_video efi_gop efi_uga  gfxterm gettext echo boot chain eval

