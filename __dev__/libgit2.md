# libgit2

Home page at [libgit2](https://libgit2.github.com/). GitHub source at [libgit2/libgit2](https://github.com/libgit2/libgit2). Also see [How to Build Libgit2](https://libgit2.github.com/docs/guides/build-and-link/).

- `git clone git@github.com:libgit2/libgit2.git`

Libgit2 is GPLv2 with a linking exception that allows it to be linked to anything without having to release
its source code. This is interesting, I'd never really paid attention, but I suppose this is possible.

## Configure options

The following options are used to configure libgit2 at pre-build time (e.g configure projects/makefiles).

- `BUILD_SHARED_LIBS`: If on, build DLLs, otherwise, build static libraries.
- `BUILD_CLAR`: If on, add unit-test suite. Packages won't have the test suite.
- `THREADSAFE`: If on, uses thread-safe libraries and code paths.
- `STDCALL`: If on and MSVC, then stdcall, otherwise cdecl.
- `STATIC_CRT`: If on and MSVC, then link to static C runtime, otherwise link to DLL C runtime.

The public include file is `git2.h`.

libgit2 dependencies: zlib, libssh2. Also libgssapi (Linux?), iconv (Mac OS X only), openssl (non-Windows),
pthreads (non-Windows). Note that SSPI on Windows is a proprietary variant of GSSAPI.

The Cmake build depends on Python? For what? It looks like a file generate.py is used to generate the files
in the Clar test suite. See [vmg/clar](https://github.com/vmg/clar). This still requires macros, but
requires the user to have less boiler plate. Somehow. Looks like it's C only. Won't affect the package, though.

## Dev log

I build libssh2 first.

```
$ git clone git@github.com:libgit2/libgit2.git
$ cd libgit2
$ mkdir build
$ cd build
$ cmake .. -DBUILD_SHARED_LIBS=OFF -DBUILD_CLAR=OFF -DTHREADSAFE=ON -DSTDCALL=ON -DSTATIC_CRT=ON -DLIBSSH2_INCLUDE_DIRS=..\..\libssh2\include -DLIBSSH2_LIBRARIES=..\..\libssh2\build\src\Debug
-- Building for: Visual Studio 14 2015
-- The C compiler identification is MSVC 19.0.23506.0
-- Check for working C compiler using: Visual Studio 14 2015
-- Check for working C compiler using: Visual Studio 14 2015 -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Could NOT find PkgConfig (missing:  PKG_CONFIG_EXECUTABLE)
-- Performing Test HAVE_STRUCT_STAT_ST_MTIM
-- Performing Test HAVE_STRUCT_STAT_ST_MTIM - Failed
-- Performing Test HAVE_STRUCT_STAT_ST_MTIMESPEC
-- Performing Test HAVE_STRUCT_STAT_ST_MTIMESPEC - Failed
-- Performing Test HAVE_STRUCT_STAT_MTIME_NSEC
-- Performing Test HAVE_STRUCT_STAT_MTIME_NSEC - Failed
-- Could NOT find ZLIB (missing:  ZLIB_LIBRARY ZLIB_INCLUDE_DIR)
-- zlib was not found; using bundled 3rd-party sources.
-- LIBSSH2 not found. Set CMAKE_PREFIX_PATH if it is installed outside of the default search path.
-- Looking for futimens
-- Looking for futimens - not found
-- Looking for qsort_r
-- Looking for qsort_r - not found
-- Looking for qsort_s
-- Looking for qsort_s - not found
-- Looking for clock_gettime in rt
-- Looking for clock_gettime in rt - not found
-- Configuring done
-- Generating done
-- Build files have been written to: {{BASE}}/libgit2/build
```

This generates a LOT of preprocessor symbols for the project

```
WIN32;_WINDOWS;_DEBUG;_DEBUG;
_SCL_SECURE_NO_WARNINGS;_CRT_SECURE_NO_DEPRECATE;_CRT_NONSTDC_NO_DEPRECATE;
GIT_WINHTTP;WIN32_SHA1;NO_VIZ;STDC;NO_GZIP;GIT_THREADS;GIT_USE_NSEC;_FILE_OFFSET_BITS=64;
WIN32;_WIN32_WINNT=0x0501;GIT_ARCH_32;CMAKE_INTDIR="Debug";
%(PreprocessorDefinitions)
```

So it looks like making the package is easy, once we can hook up libssh2 and zlib.

Libgit2 bundles some third-party dependencies to be used as fallbacks if they are not found, in `libgit2/deps/`:

- http-parser: adapted from NGINX src/http/ngx_http_parse.c
- regex: GNU C regex library
- winhttp: wrapper to let MinGW builds access WinHTTP
- zlib: zlib 1.2.8 source

Actually, of these, only zlib is an embedded library and used if an external zlib library is missing. The
rest are adapter libraries used in certain kinds of builds.

There are also iclude paths pointing at the deps folder along with the src and include folder. So nothing crazy
and if we were to make these packages, then that would be handled nicely.

```
{{BASE}}\libgit2\src;
{{BASE}}\libgit2\include;
{{BASE}}\libgit2\deps\http-parser;
{{BASE}}\libgit2\deps\regex;
{{BASE}}\libgit2\deps\zlib;
%(AdditionalIncludeDirectories)
```
