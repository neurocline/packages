# curl

Home repository is [curl/curl](https://github.com/curl/curl)

- `git clone git@github.com:curl/curl.git`

Windows builds

```
nmake /f makefile.vc mode=static ENABLE_WINSSL=yes GEN_PDB=yes MACHINE=x86 VC=10 ENABLE_IDN=no RTLIBCFG=static
nmake /f makefile.vc mode=static ENABLE_WINSSL=yes GEN_PDB=yes MACHINE=x86 VC=10 ENABLE_IDN=no DEBUG=yes RTLIBCFG=static
```

Mac build - use c-ares DNS resolver for thread-safety.

```bash
# debug
## c-ares
cd <c-ares source>
CFLAGS="-mmacosx-version-min=10.7 -arch i386" ../configure --enable-shared=no --enable-debug=no --prefix=/usr/local/cares
make
sudo make install

## curl
cd <curl source>
CFLAGS="-mmacosx-version-min=10.7 -arch i386" ../configure --without-ssl --with-darwinssl --disable-ldap --enable-shared=no --enable-debug=no --enable-ares=/usr/local/cares --prefix=/usr/local/curl
make
sudo make install

# release
## c-ares
cd <c-ares source>
CFLAGS="-mmacosx-version-min=10.7 -arch i386" ../configure --enable-shared=no --enable-debug=yes --prefix=/usr/local/cares-debug
make
sudo make install

## curl
cd <curl source>
CFLAGS="-mmacosx-version-min=10.7 -arch i386" ../configure --without-ssl --with-darwinssl --disable-ldap --enable-shared=no --enable-debug=yes --enable-ares=/usr/local/cares-debug --prefix=/usr/local/curl-debug
make
sudo make install
```
