# Android File Transfer For Linux (and Mac OS X!)

[![License](http://img.shields.io/:license-GPLv3-blue.svg)](https://github.com/whoozle/android-file-transfer-linux/blob/master/LICENSE)
[![Version](http://img.shields.io/:version-3.2-green.svg)](https://github.com/whoozle/android-file-transfer-linux)
[![Build Status](https://travis-ci.org/whoozle/android-file-transfer-linux.svg?branch=master)](https://travis-ci.org/whoozle/android-file-transfer-linux)

Android File Transfer for Linux — reliable MTP client with minimalistic UI similar to [Android File Transfer for Mac](https://www.android.com/intl/en_us/filetransfer/).

It just works™.

## Do I need it?

If you're happy with `gmtp`/`gvfs`/`mtpfs` or any other mtp software, you might not need this software (but give it a try!).

If you're suffering from crashes, missing tags and album covers, usb freezes and corrupted files, this software is right for you.

## Features

* Simple Qt UI with progress dialogs.
* FUSE wrapper (If you'd prefer mounting your device), supporting partial read/writes, allowing instant access to your files.
* No file size limits.
* Automatically renames album cover to make it visible from media player.
* No extra dependencies (e.g. `libptp`/`libmtp`).
* Available as static/shared library.
* Command line tool (aft-mtp-cli)

## Support
If you want to help me with development, click on the following badge and follow the instructions. I'm developing AFTL in my spare time and try to fix everything as fast as possible, sometimes adding features in realtime (more than 100 tickes closed by now).
Any amount would help relieving pain of using MTP. :D

[![Click here to lend your support to: Android File Transfer for Linux and make a donation at pledgie.com !](https://pledgie.com/campaigns/32353.png?skin_name=chrome' border='0')](https://pledgie.com/campaigns/32353)

## Building instructions

### Prerequisites

* You will need Qt libraries for building ui program. If you want to use only library (*Qt is not needed*), you could turn the option ```BUILD_QT_UI``` off.
* For ubuntu and other debian-based distros use the following command:

  ```shell
  sudo apt-get install build-essential cmake libqt4-dev ninja-build libfuse-dev libreadline-dev
  ```
* Basically, you need `libqtX-dev` for UI, `libfuse-dev` for FUSE interface, `cmake`, `ninja` or `make` for building the project. You could use libqt5-dev as well.

### Building with ninja

```shell
mkdir build
cd build
cmake -G Ninja ..
ninja

./qt/android-file-transfer
```

### Building with make

```shell
mkdir build
cd build
cmake ..
make

./qt/android-file-transfer
```

### Building dmg package on Mac OS X

```shell
mkdir build
cd build
cmake ..
make package

open ./packages/Android\ File\ Transfer.dmg
```

### Installation

`sudo ninja install` or `sudo make install` will install program into cmake prefix/bin directory (usually /usr/local/bin)


## How to use

### FUSE interface

```shell
mkdir ~/my-device
./aft-mtp-mount ~/my-device
```
Remember, if you want album art to be displayed, it must be named 'albumart.xxx' and placed *first* in the destination folder. Then copy other files.
Also, note that fuse could be 7-8 times slower than ui/cli file transfer.

### Qt user interface

1. Start application, choose destination folder and click any button on toolbar.

2. The options available there are: `Upload Album`, `Upload Directory` and `Upload Files`.
   The latter two are self-explanatory. `Upload album` tries searching source directory for album cover and sets best available cover.

3. You could drop any files or folders right into application window, the transfer will start automatically.

### Known problems

* Samsung removed android extensions from MTP, so fuse will be available readonly, sorry. Feel free to post your complaints to http://developer.samsung.com/forum/en
* Sometimes downloading fails with usb timeout, then phone becomes unresponsive. [Android bug #75259](https://code.google.com/p/android/issues/detail?id=75259)
* Objects created in UI will not show up in FUSE filesystem. [Android bug #169547](https://code.google.com/p/android/issues/detail?id=169547)

The actual list of all known problems and bugs available [here](https://github.com/whoozle/android-file-transfer-linux/issues)

## Contacts
Please do not hesitate to contact me if you have any further questions, my email address is <vladimir.menshakov@gmail.com>.

## Special thanks
* All who filed bugs on github and wrote emails, many features appeared only because of your feedback. Thanks!
* Alexey [gazay](https://github.com/gazay) Gaziev for useful suggestions, support and invaluable help with MacBook and MacOSX port.

## License

Android File Transfer for Linux is released under [GNU GPLv3 License](https://github.com/whoozle/android-file-transfer-linux/blob/master/LICENSE).

Copyright © 2015-2016 Vladimir Menshakov
