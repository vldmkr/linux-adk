# Linux ADK

This software aims to turn your GNU/Linux machine into an Android Accessory.
It initializes any Android device connected via USB as detailed on Android website:
http://source.android.com/tech/accessories/aoap/aoa.html

## How to build linux-adk

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

## Usage example
Before connecting the device execute next command to remember the current list of USB devices:
```
$> ADK_DEVICE=$(lsusb)
```
Then, plug in your Android device and **make sure it is unlocked**.

The following command will compare two lists of USB devices and show the difference:
```
$> diff <(echo $ADK_DEVICE) <(lsusb)
```
Take product and vendor IDs of your USB device from the output as `<vendor:product>` like this one `"18d1:4e42"`.

Run linux-adk as FTDI GPIO accessory:
```
$> ./linux-adk -d <vendor:product> -M "FTDIGPIODemo" -m "FTDI" -n 1.0 
```
In the standard output you will see all the data received from the Android device.

Android app and more detailed information about this example you can find in [android-accessory-bootstrap](https://github.com/vldmkr/android-accessory-bootstrap) repository.

## Changelog

v0.3: Remove Audio hack as not supposed to be (more on https://code.google.com/p/android/issues/detail?id=56549)
v0.2: Audio exception when launched in no-app
v0.1: Original commit for ABS2013 demo

## Author

[Gary Bisson](https://github.com/gibsson) <bisson.gary@gmail.com>

