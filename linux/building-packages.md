# Building Packages from Source on Linux
Packages can be installed in two ways:
- From source using ```make```
- Using a package manager such as rpm or apt
RPM and APT distribute .rpm or .deb files, which are self-installing, prepackaged binaries. In addition to convenience, RPM and APT track dependencies, relieving a major pain point associated with managing those manually.

However, building packages from source has several advantages:
- can be done on any system, regardless of distro/package manager
- source code is typically available before the .rpms and .debs are.
- can be considered more secure since the code can be easily audited, and are not necessarily installed as root.

## Make
- Make is a program to automate the process of compiling source code for the target system. 
- A "Makefile" defines the necessary steps to build the application. 
- There is no central database to track applications installed with make. 
- Removal of applications may or may not be supported by the makefile
- Makefiles may contain errors, due to being out of date etc...
- makefiles can be edited

## General Process
1. Source code distributed as "gzipped tarballs"
2. after unpacking the code you must check the README for specific instructions
3. Usually the following commands in order
    ```
    $ configure
    $ make
    $ make install
    ```
Configure runs a shell script downloaded with the source code that checks what compiler you have, and if the necessary dependencies are installed.

Make actually compiles the source code. 

 (sudo) make install copies the newly compiled binaries to the appropriate directories so that it can be used. It may require elevated privileges.
 