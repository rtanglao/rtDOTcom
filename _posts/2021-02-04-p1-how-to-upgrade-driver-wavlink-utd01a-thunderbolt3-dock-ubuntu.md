---
layout: post
title: "How to upgrade the Wavlink UTD01A Thunderbolt 3 dock Ubuntu driver: switch to insecure boot; download, compile and install firmware from Wavlink's site"
---
* Are you on Ubuntu and you see an  error message like the following when trying to install a driver e.g. for the [UTD01A  Thunderdock SP/Thunderdock SP IV - Thunderbolt™ 3 4K Display Docking Station](https://www.wavlink.com/en_us/product/WL-UTD01_UTD01H.html) : `modprobe: ERROR: could not insert 'r8152': Operation not permitted`
* Steps to fix this: 1. Switch to Insecure Boot as below 2. Download the [driver](https://files2.wavlink.com/drivers/PC-peripherals/RTL8153/RTL8153_Driver_Unix%20(Linux).zip)  from the Wavlink site and `sudo make all`
* The real fix of course is to sign the modules yourself using your own cert or a cert that may already exist for your driver: See [DKMS modules need to be configured to work with UEFI Secure Boot](https://wiki.ubuntu.com/UEFI/SecureBoot/DKMS)

## How to switch to Insecure Boot on Ubuntu

* Found on Ask Ubuntu:[“Operation not permitted” when trying to `modprobe xpad`](https://askubuntu.com/questions/1114867/operation-not-permitted-when-trying-to-modprobe-xpad) 

**QUOTE**

If you are facing this error modprobe: ERROR: could not insert 'rtl8723de': Operation not permitted

  The solution is to disabled the Secure Boot. Firstly check if SecureBoot is enabled on Ubuntu.

  Install mokutil "sudo apt-get install mokutil"

  and check the status of SecureBoot "mokutil --sb-state"

  In case it is enabled run command "sudo mokutil --disable-validation"

  Now enter a temporary password between 8 to 16 digits. We will use this password later. Enter the same password again to confirm. Once it’s done reboot the system and press any key when you see the blue screen (MOK management). Select Change Secure Boot state. Enter the password you had selected before and press Enter. Select Yes to disable 

**END QUOTE**


## Error messages when trying to install the driver on Ubuntu with Secure Boot

```sh
roland@roland-XPS-13-9310:~/Downloads/r8152-2.13.0$ sudo make all
[sudo] password for roland: 
make -C /lib/modules/5.6.0-1042-oem/build M=/home/roland/Downloads/r8152-2.13.0 clean
make[1]: Entering directory '/usr/src/linux-headers-5.6.0-1042-oem'
  CLEAN   /home/roland/Downloads/r8152-2.13.0/Module.symvers
make[1]: Leaving directory '/usr/src/linux-headers-5.6.0-1042-oem'
make -C /lib/modules/5.6.0-1042-oem/build M=/home/roland/Downloads/r8152-2.13.0 modules
make[1]: Entering directory '/usr/src/linux-headers-5.6.0-1042-oem'
  CC [M]  /home/roland/Downloads/r8152-2.13.0/r8152.o
  MODPOST 1 modules
  CC [M]  /home/roland/Downloads/r8152-2.13.0/r8152.mod.o
  LD [M]  /home/roland/Downloads/r8152-2.13.0/r8152.ko
make[1]: Leaving directory '/usr/src/linux-headers-5.6.0-1042-oem'
make -C /lib/modules/5.6.0-1042-oem/build M=/home/roland/Downloads/r8152-2.13.0 INSTALL_MOD_DIR=kernel/drivers/net/usb modules_install
make[1]: Entering directory '/usr/src/linux-headers-5.6.0-1042-oem'
  INSTALL /home/roland/Downloads/r8152-2.13.0/r8152.ko
At main.c:160:
- SSL error:02001002:system library:fopen:No such file or directory: ../crypto/bio/bss_file.c:69
- SSL error:2006D080:BIO routines:BIO_new_file:no such file: ../crypto/bio/bss_file.c:76
sign-file: certs/signing_key.pem: No such file or directory
  DEPMOD  5.6.0-1042-oem
Warning: modules_install: missing 'System.map' file. Skipping depmod.
make[1]: Leaving directory '/usr/src/linux-headers-5.6.0-1042-oem'
modprobe r8152
modprobe: ERROR: could not insert 'r8152': Operation not permitted
make: *** [Makefile:42: install] Error 1
roland@roland-XPS-13-9310:~/Downloads/r8152-2.13.0$
```