# README Kernel

#### **Repository :** [https://github.com/parabola-x2/Quadrocopter\_Kernel](https://github.com/parabola-x2/Quadrocopter_Kernel)

**Kernel Compiling**

Here you can find the raspberry kernel source code and following is reported the guide about how to compile it.

To differentiate the commands to be run on the computer and the ones on the raspberry, they will be differentiated as:

* `user@host ~/linux$ Computer`
* `pi@raspberry$ Raspberry`

**Download the kernel**

Clone the kernel git repository into the helikopter-kernel directory

```
user@host ~ git clone -b rpi-4.9.y https://github.com/raspberrypi/linux/
```

**Compile**

1.  Define the path where you stored the repository (the tools and the linux folder) in the RPATH variable:

    ```
    user@host ~$ export RPATH_TOOLS=global_path_helikopter-tools
    user@host ~$ export RPATH_LINUX=global_path_helikopter-kernel/linux
    ```
2.  Define then the other path and variable we would need

    if you are using a 64bit computer:

    ```
    user@host ~$ export CROSS_COMPILE=${RPATH_TOOLS}/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf-
    ```

    otherwise:

    ```
    user@host ~$ export CROSS_COMPILE=${RPATH_TOOLS}/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin/arm-linux-gnueabihf-
    ```

    ```
    user@host ~$ export INSTALL_MOD_PATH=${RPATH_LINUX}/../kernel`
    user@host ~$ export ARCH=arm
    user@host ~$ export KERNEL=kernel
    user@host ~$ cd ${RPATH_LINUX}
    user@host ~/linux$ mkdir ../kernel
    ```
3.  Install the patch for the RealTime Kernel

    ```
    user@host ~/linux$ cp ../patch patch-4.9.20-rt16.patch.gz .
    user@host ~/linux$ zcat patch patch-4.9.20-rt16.patch.gz | patch -p1
    ```
4.  Now you can decide whether take the configuration file from the kernel altrady installed in the raspberry or create a new one

    To use an old configuration file you need first to generate it on the raspberry and then copy it in the computer where you want to make the compiling

    ```
    > pi@raspberry$ sudo modprobe configs
    > user@host ~/linux$ scp pi@raspberry:/proc/config.gz ./
    > user@host ~/linux$ zcat config.gz > .config
    > user@host ~/linux$ make oldconfig
    ```

    To create a new the .config file

    ```
    user@host ~/linux$ make bcmrpi_defconfig
    user@host ~/linux$ make menuconfig
    ```
5.  During the configuration of the kernel we need to define a couple of parameters in order to get the Fully Preemptible Kernel. In the menu of the configuration file, modify the following parameters:

    ```
    CONFIG_PREEMPT_RT_FULL: Kernel Features → Preemption Model (Fully Preemptible Kernel (RT)) → Fully Preemptible Kernel (RT)
    Enable HIGH_RES_TIMERS: General setup → Timers subsystem → High Resolution Timer Support (Actually, this should already be enabled in the standard configuration.)
    ```
6.  Now we can compile the kernel, generate the modules and the data tree files and install the modules in the directory we defined before in the INSTALL\_MOD\_PATH variable

    ```
    make zImage modules dtbs modules_install
    ```
7.  At this point we have to collect all the file necessary to be copied in the raspberry

    Create a folder which would contain the files to be copied in the boot partition

    ```
    mkdir $INSTALL_MOD_PATH/boot
    ```

    Generate the kernal image and copy the data tree files

    ```
    ./scripts/mkknlimg ./arch/arm/boot/zImage $INSTALL_MOD_PATH/boot/$KERNEL.img
    cp ./arch/arm/boot/dts/*.dtb $INSTALL_MOD_PATH/boot/
    cp -r ./arch/arm/boot/dts/overlays $INSTALL_MOD_PATH/boot
    ```

    Compress all the generated files and copy them into the raspberry

    ```
    cd $INSTALL_MOD_PATH
    tar czf kernel.tgz *
    scp kernel.tgz pi@raspberry:/tmp
    ```
8.  Finally from the raspberry we need to decompress the tarball to install the new kernel

    ```
    pi@raspberry ~$ tar xzf tmp/kernel.tgz
    ```
9. Reboot your raspberry and you will have the new kernel installed

**Compiler Linux**

CROSS\_COMPILE ARCH INSTALL\_MOD\_PATH

clean menuconfig, xconfig, oldconfig, config dep zImage modules\_install distclean

zImage, bzImage. Both are uncompressed Image and has nothing to do with gzip and bzImages.

depmod

-F System.map

-b / ( base directory where the modules are stored for this architecture ).

```
apt-get install build-essential fakeroot 
apt-get build-dep linux 
apt-get source linux
git clone git://kernel.ubuntu.com/ubuntu/ubuntu-precise.git
apt-get build-dep linux-image-(uname−r)
apt−get install linux−image−(uname -r)
chmod a+x debian/scripts/*
chmod a+x debian/scripts/misc/*
fakeroot debian/rules clean
fakeroot debian/rules editconfigs
fakeroot debian/rules binary-headers binary-generic
```

This takes the current configuration for each architecture/flavour supported and calls menuconfig to edit its config file. The chmod is needed because the way the source package is created, it loses the executable bits on the scripts. In order to make your kernel “newer” than the stock Ubuntu kernel from which you are based you should add a local version modifier. Add something like “+test1” to the end of the first version number in the debian.master/changelog file, before building.

If the build is successful, a set of three .deb binary package files will be produced in the directory above the build root directory. For example after building a kernel with version “2.6.38-7.37” on an amd64 system, these three (or four) .deb packages would be produced:

```
cd ..
ls *.deb
linux-headers-2.6.38-7_2.6.38-7.37_all.deb
linux-headers-2.6.38-7-generic_2.6.38-7.37_amd64.deb
linux-image-2.6.38-7-generic_2.6.38-7.37_amd64.deb
```

Testing the new kernel Install the three-package set (on your build system, or on a different target system) with dpkg -i and then reboot:

```
sudo dpkg -i linux*2.6.38-7.37*.deb
sudo reboot
```

**Patching a kernel**

```
cd /usr/src 
wget http://www.kernel.org/pub/linux/kernel/v2.6/testing/patch-2.6.19-rc4.bz2  
cd /usr/src/linux 
bzip2 -dc /usr/src/patch-2.6.19-rc4.bz2 | patch -p1  –dry-run 
bzip2 -dc /usr/src/patch-2.6.19-rc4.bz2 | patch -p1
```

Purging a PPA means, downgrading the packages in the selected PPA to the version in the official Ubuntu repositories and disabling that PPA. PPA Purge does exactly that. To install PPA Purge run the following command:

```
sudo apt-get install ppa-purge
```

**Debug Symbols**

Sometimes it is useful to have debug symbols built as well. Two additional steps are needed. First pkg-config-dbgsym needs to be installed. Second when executing the binary-\* targets you need to add ‘skipdbg=false’.

```
sudo apt-get install pkg-config-dbgsym
fakeroot debian/rules clean
fakeroot debian/rules binary-headers binary-generic skipdbg=false

sudo  apt-get -o Debug::pkgProblemResolver=yes dist-upgrade 
sudo apt-get -u  dist-upgrade sudo apt-get -f install
sudo apt-get clean
fakeroot, kernel-wedge, gawk
```

Alternatively, before compiling, use the kernel config option “LOCALVERSION” to append a unique suffix to the regular kernel version. LOCALVERSION can be set in the “General Setup” menu.

– In order to boot your new kernel, you’ll need to copy the kernel image (e.g. …/linux/arch/i386/boot/bzImage after compilation) to the place where your regular bootable kernel is found.

Command to install linux source Command to download is

```
apt-get source linux-image-$(uname -r)
svn checkout svn://developer.berlios.de/socketcan/trunk
Git clone git://kernel.ubuntu.com/ubuntu/ubuntu-maverick.git
Fakeroot debian/rules clean Dh_testdir
apt-get source kernel-source-2-4-27
apt-get install kernel-source-2-4-27
apt-get source linux-headers-$(uname -r)
```

**ELDK**

for running for eldk on 64 bit hosts

```
Sudo apt-get install ia32-libs
Ncftp  ftp.sunet.se 
Wget ftp://ftp.sunet.se/pub/linux...
patch -p0 <  u-boot-1.1.3.at91rm9200_mmc.patch
sudo add-apt-repository  ppa:kivy-team/kivy
configure –enable-win64 make make install
```

Traditionally, UNIX platforms called the kernel image /unix. With the development of virtual memory, kernels that supported this feature were given the vm- prefix to differentiate them. The name vmlinux is a mutation of vmunix, while in vmlinuz the letter z at the end denotes that it is compressed.

**Toolchain**

We need tools that would build programs or a kernel that is capable of running on the SoC ( BCM2708 from Broadcom ). The tool chain is called gcc-linaro-arm-linux-gnueabihf-raspbian-x64 ( arch-vendor-(os-)abi ) and can be obtained via the github.com/raspbian/tools.git

* arm-bcm2708-linux-gnueabi
* arm-bcm2708hardfp-linux-gnueabi
* gcc-linaro-arm-linux-gnueabihf-raspbian
* gcc-linaro-arm-linux-gnueabihf-raspbian-x64

**Building the kernel**

* Git clone –-depth=1 https://github.com/raspberrypi/linux
* Please note that for the below two commands, the major, mior and the development version must match. This can be verified by typing make kernelversion after the repository has been downloaded.
* Git clone –-depth=1 https://github.com/raspberrypi/linux.git -b rpi-3.18.y
* Wget https://www.kernel.org/pub/linux/kernel/projects/rt/3.18/older/patch-3.18.16-rt13.patch.xz
* Git clone –depth=1 https://github.com/emlid/linux-rt-rpi.git
* ```
   Since some Kernel module driver has been developed during this project, it was also necessary to compile the custom Kernel drivers for the EMLID-distribution. Therefore, get slightly modified Kernel sources of the EMLID-distribution can be found at \url{https://github.com/emlid/linux-rt-rpi}. To download the sources to the Development Environment VM, the following commands can be used:
  ```
* Raspbian distribution: Wget http://downloads.raspberrypi.org/raspbian\_latest
* xcat “patchname” | patch –p 1 –dry-run
* Xcat “patchname” | patch –p 1
* Directly on the Raspberry : https://www.raspberrypi.org/documentation/linux/kernel/building.md
* Make variables:
* KERNEL=kernel
* ARCH=arm
* CROSS\_COMPILE=arm-linux-gnueabihf- ( arch-vendor-(os-)abi )
* INSTALL\_MOD\_PATH=path-where-you-want-to-output
* EXTRA\_VERSION=
* make Help
* make kernelversion
* make kernelconfig
* make bcmrpi\_defconfig ( using this is preferred, because most required adaption is already available for the raspberry pi, otherwise the user needs to configure a lot of options if he uses make menuconfig )
* make zImage
* make modules
* make dtbs
* make modules\_install
* sudo dd if=”firmwareimage” of=/dev/sdb
* raspi-config Under Advanced Options: Enable I2C Enable SSH Disable Kernel Debug to UART Configure Hostname Change

I2C baud rate for the option i2c\_bcm2708 baudrate in /etc/modprobe.d/i2c.conf to 400000. options i2c\_bcm2708 baudrate=400000. This step would not be needed if the pre configured EMLID image is used. In the pre configured EMLID image, the UART port is configured to the required setup by default. No Kernel debugging messages are put to the serial port. But the default I2C baudrate is set to 1Mhz which is to much. The highest common frequency of the sensors participating on the I2C bus is 400kHz.

```
    If no  i2c.conf exists, create one. Reboot for the changes to take place.
    (1) 8 Advanced Options => A4 SSH => <Enable> => <OK>
    (2) 8 Advanced Options => A7 I2C => <YES> => <OK> => <YES> => <OK>
    (3) 8 Advanced Options => A8 Serial => <NO> => <OK> ( Dont use Kernel debugging on UART ) 
    (4) 8 Advanced Options => A2 Hostname => <OK> => "HElikopterPi" => <OK>
    (5) <FINISH> => <YES>
```

**Kernel Boot**

* scp zImage root@192.168.22.169:/boot/zImage
* rsync –av modules-folder pi@192.168.22.161:/lib/
* edit /boot/config.txt and write kernel=”yourimage”
* sudo reboot
* uname –a should have the new host name
* Linux HElikopterPi 3.18.14-rt10+ #1 PREEMPT RT Mon Jun 15 21:21:16 CEST 2015 armv6l GNU/Linux

**Pre-configured Image**

wget http://www.emlid.com/new-raspbian-with-real-time-kernel-jan-2015/

For a convenient and easy start with the Raspberry Pi, a pre-configured Raspberry Pi Firmware can be found at the SVN repository folder \texttt{/sys/RPi/}. The pre-configured Firmware Image is based on the EMLID-distribution. The EMLID-distribution originates from a open source project for a different Raspberry Pi based Quadcopter. It comprises the RT-Kernel patch as well as several optimizations regarding the system configuration to access peripherals that fit to the needs of this project.

For this project, pick the archive file EMLID\_Preempt\_IP192.168.2.1.zip from the SVN repository. Unzip the file to get the extracted 8GB Firmware Image.

**Debugging**

The debugging happens on the SSH channel i.e the user logs into the raspberry pi via another computer.

####
