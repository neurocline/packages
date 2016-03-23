# boost

The Boost home page is [Boost C++ Libraries](http://www.boost.org/). There is a Github mirror at [boostorg/boost](https://github.com/boostorg/boost). Also see [biicode/boost](https://github.com/biicode/boost) for one adapted to Biicode and [pocb/boost](https://github.com/pocb/boost) for one with CMake files.

- `git clone --recursive git@github.com:boostorg/boost.git`

The Boost git project uses submodules heavily. The splitting into submodules seems to have duplicated
history tremendously, it takes 15+ minutes to check out the sub-modules.

## The cliff notes version of building

Windows

~~~
  cd vendor
  call bootstrap.bat
  bjam --toolset=msvc-%VCVersion%.0 architecture=x86 address-model=%ARCH% %BOOST_LIBS% variant=%VARIANT% link=static
  cd ..
~~~

```
.\bootstrap
.\b2 headers
```

Linux/Mac OS X

~~~
  cd vendor
  ./bootstrap.sh --without-icu
  ./bjam dso=on vis=off architecture=x86 address-model=$ARCH $BOOST_LIBS variant=$VARIANT link=static
  cd ..
~~~

```
./bootstrap.sh
./b2 headers
```

~~~ARCH is 64 or 32. VARIANT is release for release builds, empty for debug builds. BOOST_LIBS is the list of Boost libraries to build.~~~

See [Getting Started with Modular Boost](https://svn.boost.org/trac/boost/wiki/TryModBoost).

## Dev log

