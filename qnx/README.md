# Compile the port for QNX

**NOTE**: QNX ports are only supported from a Linux host operating system

- Setup your QNX SDP environment
- From the **project root folder**, type:  
  
    `make -C qnx/build JLEVEL=$(nproc)`  
    `make -C qnx/build install`  

## OpenSSL 3.5.4 Installation Information

This port (**OpenSSL 3.5.4**) will be installed with the **/usr/local** prefix, which allows it to coexist in parallel with the older **OpenSSL 3.0** libraries.

After installation, you will find the artifacts for OpenSSL 3.5.4 at the following locations in the SDP tree:

### Header Files:
$QNX_TARGET/usr/local/include/openssl  

### Libraries and Binaries:

#### for AArch64 (aarch64le)
$QNX_TARGET/aarch64le/usr/local/lib  
$QNX_TARGET/aarch64le/usr/local/bin  

#### for x86_64
$QNX_TARGET/x86_64/usr/local/lib  
$QNX_TARGET/x86_64/usr/local/bin  

## Compiling and Running user applications

QNX recommends using the **OpenSSL 3.5.4** libraries **only with your own applications**.  

When building your applications, you should pass the `-I` and `-L` parameters to the compiler to specify where to find the headers and libraries.

For example, to build **hello_ssl** for the **aarch64** architecture, run:

`qcc -Vgcc_ntoaarch64le hello_ssl.c
-I$QNX_TARGET/usr/local/include
-L$QNX_TARGET/aarch64le/usr/local/lib
-lssl -lcrypto`

After building, copy the **OpenSSL 3.5.4** libraries to a directory on the target that is **different from the system libraries**.  

For example, to run **hello_ssl** with shared libraries located at `~/lib`, run:

`LD_LIBRARY_PATH=~/lib:$LD_LIBRARY_PATH ./hello_ssl`