# Static & Dynamic libraries 

- A library in C is a collection of objects files exposed for use and build other programs, so instead of re-write sections of code we bring back information that is already existing, this is where it comes to the concept of a library.
- In C there exist two kinds of libraries Static and Dynamic 
  
## #Static libraries 
- A static library is a collection of object files that have been compiled
and linked together to form a single library file that can be linked directly into a program at compile-time it.

- __lib.a__ -- represents static lib

### 1-Create a static library 
----
```bash
#Create static_lib directory
- mkdir static_lib
- cd static_lib
```
```bash
#Create Include & Lib directories inside
- mkdir Include
- mkdir Lib
 ```
 
 ```bash
#Create lib.h Header file in Include directory & add inside it the function prototype
- Create `libsub.h` File 
- Insert 'int sub(int,int);' prototype 
```

```bash
#Create lib.c Source file in Lib directory & add inside it a function definition
- Create `libsub.c` File
- Insert '#include libsub.h'
- Insert 'int sub(int x,int y){return (x - y);}'
```
### 2-Create an application
---
```bash
#Create main.c Sourcefile in static_lib directory & add inside it a main function definition
- Create `main.c` File
- Insert '#include stdio'
- Insert '#include libsub.h'
- Insert 'int main(void){int num1 = 5,num2 = 2,res = 0; res = sub(num1,num2); return 0;}'
```
### 3-Build the application
---
```bash
#Generate the libsub.o including the header library in the symbol table 
- gcc -c libsub.c ..Include 
#Generate the output.a Archive file in Lib directory to compress the libraries in an indexed format that will be used in the linker stage
- ar -rcs output_archive.a libsub.o #arg3.o # arg4.o #...
	[options]
		- r 'Replace or insert file to archive'
		- c 'Create new archive'
		- s 'Add symbol table to archive'
```
```bash
#Generate the main.o including the header library in the symbol table 
- gcc -c main.c -I .Include 
#Generate the executable file 
- gcc -o main.exe main.o Liboutput_archive.a
```
### 4-Run the application
---
```bash
- ./main.exe
#Now it should run with no errors 
```

---

## #Dynamic libraries 
- A Dynamic library is a type of library that is linked to an executable
program at runtime, rather than being linked at compile time.
- lib.so -- represent shared object

### 1-Create a Dynamic library 
---
```bash
#Create dynamic_lib directory
- mkdir dynamic_lib
- cd dynamic_lib 
```

```bash
#Create Include & Lib directories inside
- mkdir Include
- mkdir Lib
 ```
 
 ```bash
#Create lib.h Header file in Include directory & add inside it function prototype
- Create `libsub.h` File 
- Insert 'int sub(int,int);' prototype 
```
```bash
#Create lib.c Source file in Lib directory & add inside it a function definition
- Create `libsub.c` File
- Insert '#include libsub.h'
- Insert 'int sub(int x,int y){return (x - y);}'
```
### 2-Create an application
---
```bash
#Create main.c Sourcefile in dynamic_lib directory & add inside it a main function definition
- Create `main.c` File
- Insert '#include stdio'
- Insert '#include libsub.h'
- Insert 'int main(void){int num1 = 5,num2 = 2,res = 0; res = sub(num1,num2); return 0;}'
```     
### 3-Build the application
---
```bash
#Generate the libsub.o including the header library in the symbol table 
- gcc -c -fPIC libsub.c -I ..Include 
#Generate the output.so Shared file in Lib directory to compress the libraries in an indexed format that will be used in the linker stage
- gcc -shared -o output.so libsub.o #arg3.o # arg4.o #...
```
```bash
#Generate the main.o including the header library in the symbol table 
- gcc -c -fPIC main.c -I .Include 

#Generate the executable file 
- gcc main.c -L .Lib .Liboutput.so -o main.exe -I .Include

#We need to let the system loader knows the location of the linked shared libraries to link them runtime when needed

#Set the variable with the directory path of the lib*.so files
1- `LD_LIBRARY_PATH` 
	- export LD_LIBRARY_PATH=.Lib/
#The default search path
2- `System Path` 
	#Copy the shared location
	1- sudo cp .Liblib.so usrlib 
	#Change the execution mode
	2- sudo chmod 0755 usrliblib.so
	#Flush the cache
	3- sudo ldconfig  
3- `rpath`
	#Remove the LD_LIBRARY_PATH
	1- unset LD_LIBRARY_PATH
	#Compile with rpath option
	2- gcc -L.Lib -Wl,-rpath=.Lib -Wall -o main.exe main.c .Liblib.so -I.include

```
### 4-Run the application
---
```bash
-./main.exe
#Now it should run with no errors 
```
