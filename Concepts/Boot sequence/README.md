
# Booting sequence
- Booting is a startup sequence that starts the operating system of a computer when it is turned on. A **boot sequence** is the initial set of operations that the computer performs when it is switched on.
- Multiple-stage **bootloaders** are used, in which several small programs of increasing complexity sequentially summon one after the other, until the last of them loads the operating system.

## **`x86`** *boot sequence*
 - **Boot ROM**---**`BIOS`**
	 - The **boot ROM** is a type of ROM that is used for booting a computer system. There are two types: 
		 - **`Mask boot ROM`** that cannot be changed afterwards 
		 - **`EEPROM`** which can contain an UEFI implementation.
	 - Contains the primary bootloader **`BIOS`** [basic input/output system]
		 - Determines whether all of the necessary attachments are in place and operational.
		 - Performs some system integrity
		 - Searches, loads, and executes the boot loader program.
		 - It look for boot loader in CD-ROM, or hard drive.
		 - BIOS loads and executes the **`MBR`** boot loader
 - **Master boot record**---**`MBR`**
	 - It is located in the 1st sector of the bootable disk. Typically **`/dev/had`** or **`/dev/sda`**
	 - Load Second bootloader From **`ROM`** to **`RAM`** 
		> Ex: grub, u-boot
	
	 - Allocate your partition

		> Ex: Partition C , E

 - **GRUB**
	 - Load the **`Kernel`** into the Ram
	 - Give control to the kernel
	 - CPU start to fetch and execute from Kernel application
 - **Kernel**
	 -   Load Device Drivers
		 > Ex: Keyboard, Mouse, printer, …
	-   Memory Initiation
		> Ex: Stack, Heap, …
	-   Mount file system
		> File system are binary file in order for the user can read and write from them it must be mounted.
	-   Run Init process
		> It is the beginning of the User Space, the start of the Linux image.
---
**`Summary`**

```mermaid
graph LR
A(BIOS) --> B(MBR) --> C(GRUB) --> D(Kernel) --> E(Init process)
```
---
## **`Raspberry pi`** *boot sequence*

 - **Boot ROM**
	 - A type of ROM that is used for booting a computer system.
	 - Located on the Raspberry pi boards coming from the vendor
	 - Loads **`Bootcode.bin`** in the L2 cache
		 
 - **Bootcode.bin**
	 - Enables SDRAM
	 - Loads **`loader.bin`**
	
 - **loader.bin**
	 - Execute .elf files
	 - Loads **`Start.elf`**
	
 - **Start.elf**
	 - Loads Kernel.img

 - **Kernel**
	 -   Load Device Drivers
		 > Ex: Keyboard, Mouse, printer, …
	-   Memory Initiation
		> Ex: Stack, Heap, …
	-   Mount file system
		> File system are binary file in order for the user can read and write from them it must be mounted.
	-   Run Init process
		> It is the beginning of the User Space, the start of the Linux image.
---
**`Summary`**

```mermaid
graph LR
A(Bootcode.bin) --> B(Loader.bin) --> C(Start.elf) --> D(Kernel) --> E(Init process)
```
---
## **`Beaglebone`** *boot sequence*

 - **Boot ROM**
	 - A type of ROM that is used for booting a computer system.
	 - Located on the **Beaglebone boards** coming from the vendor.
	 - Loads **`MLO`** in the L2 cache.
		 
 - **MLO---**`X-loader`
	 - Hardware initializations
	 - First stage bootloader
	 - Runs & looks for the zimage	
 - **U-boot**
	 - Second stage bootloader
	 - Load the **`Kernel`** into the Ram
	 - Give control to the kernel	
 - **Kernel**
	 -   Load Device Drivers
		 > Ex: Keyboard, Mouse, printer, …
	-   Memory Initiation
		> Ex: Stack, Heap, …
	-   Mount file system
		> File system are binary file in order for the user can read and write from them it must be mounted.
	-   Run Init process
		> It is the beginning of the User Space, the start of the Linux image.
---
**`Summary`**

```mermaid
graph LR
A(MLO) --> B(U-boot) -->D(Kernel) --> E(Init process)
```
---
		 
		 

