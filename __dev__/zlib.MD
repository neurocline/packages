# zlib

Home repository is [madler/zlib](https://github.com/madler/zlib).

- `git clone git@github.com:madler/zlib.git`

This was originally a configure-based project, but is now using CMake.

## Package source

`source/` folder is all the *.h and *.c files in the zlib repo in the root.

This project has optional assembly language files if the compiler is GCC. To use assembly, define ASMV in the source prefix. GCC can directly build assembly.

- x86: `contrib/asm686/match.S`
- x86_64: `contrib/amd64/amd64-match.S`

There are also assembly language files suitable for masm on Windows with Visual Studio. To use assembly, define ASMV and ASMINF in the source prefix. However, this is outside the remit of the strict package system, because this is not C/C++ at all, masm must be invoked.

- x86: `contrib/masmx86/inffas32.asm`, `contrib/masmx86/match686.asm`
- x86_64: `contrib/masmx64/gvmat64.asm`, `contrib/masmx64/infasx64.asm`

Public headers:

- zlib.h

There are lots of sub-projects in the zlib source. Should these be individual packages, or separate packages, and should there be a hierarchy, and if so, how should that work? E.g.

```
#using "zlib"
#using "minizip"
#using "zlib/blast"
#using "zlib/minizip"

using zlib
using minizip
using zlib.minizip
```

some of the addons are so short that they shouldn't be packages, and some aren't really independent (e.g. the assembly language replacements).

Note that with strings, we can have packages like "UnitTest++" or "Google Protocol Buffers". But length has its own problems. Note that most languages have gone for short names without spaces, controlling case.

## Package options

`_LARGEFILE64_SOURCE=1`: set if off64_t is 64 bits.

HAVE_SYS_TYPES_H: defined if <sys/types.h> exists. Let's make the default be true.

HAVE_STDINT_H: defined if <stdint.h> exists. Let's make the default be true.

HAVE_STDDEF_H: defined if <stddef.h> exists. Let's make the default be true.

HAVE_FSEEKO: defined if the `fseeko` function exists. Should be true on Linux and Mac, not true on Windows.

Z_HAVE_UNISTD_H: defined if <unistd.h> exists. True on Linux/Mac, false on Windows.

Z_PREFIX: If defined, then public zlib functions have `z_` prefixed to them.

## Configuration

On Windows

```
#define _CRT_SECURE_NO_DEPRECATE
#define _CRT_NONSTDC_NO_DEPRECATE
```

## Open questions

Do we want people to be able to make DLLs from packages? Or rather, is this a feature
that packages should support?

What about tests?

## Note

[FEATURE_TEST_MACROS(7)](http://man7.org/linux/man-pages/man7/feature_test_macros.7.html)
