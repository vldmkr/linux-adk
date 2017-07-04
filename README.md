# Linux ADK

This software aims to turn your GNU/Linux machine into an Android Accessory.
It initializes any Android device connected via USB as detailed on Android website:
http://source.android.com/tech/accessories/aoap/aoa.html

# How to build linux-adk
-------------------------
As of today (alpha v0.3), autotools have not been configured.
Therefore the build is done manually as follow:
```
$> make
```

This software requires the use of libusb and libasound.

For cross-compiling, several environment variables must be set manually:

```
$> export ARCH=arm
$> export CROSS_COMPILE=<custom_toolchain>
$> export CFLAGS="-I<path_to_libusb_headers> -I<path_to_libasound_headers>"
$> export LDFLAGS="-L<path_to_libusb> -L<path_to_libasound>"
$> make
```

# Changelog

v0.3: Remove Audio hack as not supposed to be (more on https://code.google.com/p/android/issues/detail?id=56549)
v0.2: Audio exception when launched in no-app
v0.1: Original commit for ABS2013 demo

# Author

[Gary Bisson](https://github.com/gibsson) <bisson.gary@gmail.com>

