# libssh2

Home page is [Libssh2](https://www.libssh2.org/). Github source [libssh2/libssh2](https://github.com/libssh2/libssh2).

- `git clone git@github.com:libssh2/libssh2.git`

## Configure options

The following options are used to configure libgit2 at pre-build time (e.g configure projects/makefiles).
The default is shown

- `BUILD_SHARED_LIBS=OFF`: If OFF, build static library, otherwise build shared library.
- `CRYPTO_BACKEND=`: one of OpenSSL, Libgcrypt, WinCNG. If blank, picks first available.
- `ENABLE_ZLIB_COMPRESSION=OFF`: If ON, will use zlib for payload compression. Typically not desired.
- `ENABLE_CRYPT_NONE=OFF`: If ON, allows the None cipher. Generally a bad idea to have this.
- `ENABLE_MAC_NONE=OFF`: If ON, allows both sides to negotiate to no MAC. Probably don't want this.
- `ENABLE_GEX_NEW=ON`: Improved diffie-hellman exchange. Turn off for compatibility with old servers.
- `ENABLE_DEBUG_LOGGING=ON`: debug traces. want ON in Debug, OFF in Release

Dependencies: need one of OpenSSL, Libgcrypt, WinCNG (built-in wrapper to Windows CryptoAPI?)

## Dev log

```
$ git clone git@github.com:libssh2/libssh2.git
$ cd libssh2
$ mkdir build
$ cd build
$ cmake .. -DCRYPTO_BACKEND=WinCNG
-- Building for: Visual Studio 14 2015
-- The C compiler identification is MSVC 19.0.23506.0
-- Check for working C compiler using: Visual Studio 14 2015
-- Check for working C compiler using: Visual Studio 14 2015 -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Looking for include files windows.h, bcrypt.h
-- Looking for include files windows.h, bcrypt.h - found
-- Looking for include file ntdef.h
-- Looking for include file ntdef.h - not found
-- Looking for include file ntstatus.h
-- Looking for include file ntstatus.h - found
-- Looking for include files windows.h, wincrypt.h
-- Looking for include files windows.h, wincrypt.h - found
-- Looking for include file unistd.h
-- Looking for include file unistd.h - not found
-- Looking for include file inttypes.h
-- Looking for include file inttypes.h - found
-- Looking for include file stdlib.h
-- Looking for include file stdlib.h - found
-- Looking for include file sys/select.h
-- Looking for include file sys/select.h - not found
-- Looking for include file sys/uio.h
-- Looking for include file sys/uio.h - not found
-- Looking for include file sys/socket.h
-- Looking for include file sys/socket.h - not found
-- Looking for include file sys/ioctl.h
-- Looking for include file sys/ioctl.h - not found
-- Looking for include file sys/time.h
-- Looking for include file sys/time.h - not found
-- Looking for include file sys/un.h
-- Looking for include file sys/un.h - not found
-- Looking for include file windows.h
-- Looking for include file windows.h - found
-- Looking for include file ws2tcpip.h
-- Looking for include file ws2tcpip.h - found
-- Looking for include file winsock2.h
-- Looking for include file winsock2.h - found
-- Looking for sys/types.h
-- Looking for sys/types.h - found
-- Looking for stdint.h
-- Looking for stdint.h - found
-- Looking for stddef.h
-- Looking for stddef.h - found
-- Check size of long long
-- Check size of long long - done
-- Looking for gettimeofday
-- Looking for gettimeofday - not found
-- Looking for strtoll
-- Looking for strtoll - found
-- Looking for snprintf
-- Looking for snprintf - found
-- Looking for poll
-- Looking for poll - not found
-- Performing Test HAVE_O_NONBLOCK
-- Performing Test HAVE_O_NONBLOCK - Failed
-- Performing Test HAVE_FIONBIO
-- Performing Test HAVE_FIONBIO - Failed
-- Performing Test HAVE_IOCTLSOCKET
-- Performing Test HAVE_IOCTLSOCKET - Success
-- Looking for include file arpa/inet.h
-- Looking for include file arpa/inet.h - not found
-- Looking for include file netinet/in.h
-- Looking for include file netinet/in.h - not found
-- Looking for strcasecmp
-- Looking for strcasecmp - not found
-- Looking for _stricmp
-- Looking for _stricmp - found
-- Looking for _snprintf
-- Looking for _snprintf - found
-- Looking for __func__
-- Looking for __func__ - found
-- Looking for __FUNCTION__
-- Looking for __FUNCTION__ - found
--
-- The following features have been enabled:

 * diffie-hellman-group-exchange-sha1 , "new" diffie-hellman-group-exchange-sha1 method

-- The following features have been disabled:

 * Shared library , creating libssh2 as a shared library (.so/.dll)
 * Compression , using zlib for compression
 * "none" cipher
 * "none" MAC
 * Logging , Logging of execution with debug trace

-- Configuring done
-- Generating done
-- Build files have been written to: {{BASE}}/libssh2/build
```
