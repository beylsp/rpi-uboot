This is a fork of the Das U-Boot bootloader for Raspberry Pi.

# Introduction

`U-Boot` is a popular stage-2 bootloader used by many development platforms and supports several architectures including ARM. It is capable of loading a kernel image from the NAND, SD card, USB drive and even the Ethernet via bootp, DHCP and TFTP. The u-boot executable is stored as a file called `u-boot.bin` in a FAT partition.

Once the execution is handed over to `U-Boot`, it offers you a few seconds to interrupt the boot sequence. If you choose not to interrupt, `U-Boot` executes an environment variable called `bootcmd`. `bootcmd` holds the search sequence for a file called `uImage`. This is the kernel image. The kernel image is loaded into the memory, and the execution is finally transferred to the kernel. The search sequence defined in the `bootcmd` variable and the filename (`uImage`) are hard-coded in the `U-Boot` source code. 

We can however override the default search sequence and load the kernel image or an ELF file from a TFTP server. The `bootcmd` script checks for the existence of a file called `uEnv.txt`. If the file is found, the file is loaded into the memory. Then, it is imported to the environment ready to be read or executed. After this, the script checks to see if the variable `uenvcmd` is defined. If it is defined, the script in the variable is executed. In brief, the `uEnv.txt` file is a method for users to insert scripts into the environment.

If the boot sequence is interrupted, you are dropped to the `U-Boot` shell.

# Building

0. Make sure that you have installed the ARM cross-compilation toolchain:  
    `apt-get install gcc-arm-linux-gnueabi`

1. Make the configuration for Raspberry Pi:  
    `make rpi_defconfig`

2. Build U-Boot:  
    `make -j8`

   If you need to use a cross compilation toolchain other than the default (`arm-linux-gnueabi-`),
   just pass it to the make command:    
    `make CROSS_COMPILE=arm-linux-gnueabihf- -j8`

3. Done!


