
# Crosstool-NG
- Crosstool-NG is a versatile **(**cross**)** toolchain generator. It supports many architectures and components and has a simple yet powerful menuconfig-style interface.

## #Toolchain

- Set of software development tools used simultaneously to complete complex software development tasks or to deliver a software product.

## #Native Toolchain

- This toolchain runs on the same type of system, sometimes the same actual system, as the programs it generates. This is the usual case for desktops and servers.

## #Cross Toolchain

 - This toolchain runs on a different type of system than the target, allowing the development to be done on a fast desktop PC and then loaded onto the embedded target for testing.
 - 
## #What's in a toolchain ?
 - Binutils
	 - Is a set of tools to generate and manipulate binaries for a given CPU architecture:
		 - Assembler, that generates binary code from assembler source code.
		 - Linker
		 - ar, ranlib, to generate .a archives, used for libraries.
		 - objdump, readelf, size, nm, strings, to inspect binaries. Very useful analysis tools!
 - Kernal headers
	 - Abstraction for system calls.
	 - Used by C-library to communicate with the kernel.

---
---
### Setup Crosstool-NG
----
### Download Crosstool-NG
```bash
#Clone this repo to your local machine
 -  git clone https://github.com/crosstool-ng/crosstool-ng.git
```
### Build Crosstool-NG
```bash
#To setup the environment
 - ./bootsrap
```
```bash
#To check all dependencies
 - ./configure --enable-local
```
```bash
#To generate the Makefile for croostool-ng
 - make
```
```bash
#To list all microcontrollers supported
 - ./ct-ng list-samples
#For example if you want to configure the tool chain for specific target list the names to find the correct toolchain name 
 - ./ct-ng lidt-samples | grep `target_name`
#We will configure here the cross tool for arm cortex a9 : arm-cortexa9_neon-linux-gnueabihf
```
```bash
#To configure the microcontroller used
 - ./ct-ng arm-cortexa5-linux-uclibcgnueabihf
```
```bash
#To configure toolchain used
 - ./ct-ng menuconfig
	 - `Set C library to glibc/uclibc/musl`
	 - `Make sure to support C++ CC_LANG_CXX`
	 - `Disable all debug facilities except DEBUG_STRACE`

> Hint: 'Use `/` to search in the menuconfig for desired configuration'

```
```bash
#To build the toolchain
 - ./ct-ng build
```
### Check Toolchain output

 - **lib** `Contains the shared objects for the C library and the dynamic 	  linker/loader, ld-linux.`
 - **usr/lib** `The static library archive files for the C library, and any other libraries that may be installed subsequently.`
 - **usr/include** `Contains the headers for all the libraries`
 - **usr/bin** `Contains the utility programs that run on the target, such as the ldd command`
 - **usr/share** `Used for localization and internationalization`
 - **sbin** `Provides the ldconfig utility, used to optimize library loading paths`
