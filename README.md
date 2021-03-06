# Boot to Gecko (B2G)

Boot to Gecko aims to create a complete, standalone operating system for the open web.

You can read more about B2G here:

  http://wiki.mozilla.org/B2G

follow us on twitter: @Boot2Gecko

  http://twitter.com/Boot2Gecko

join the Mozilla Platform mailing list:

  http://groups.google.com/group/mozilla.dev.platform

and talk to us on IRC:

  #B2G on irc.mozilla.org

## Prerequisites

### Linux

* A 64 bit linux distro
  * See http://source.android.com/source/initializing.html on configuring USB access.
* 20GB of free disk space
* autoconf-2.13
* git
* ccache
* gcc/g++
* bison
* flex
* 32bit ncurses
* 32bit zlib
* make

### OSX

* XCode
* 20GB of free space
* homebrew
  * git (if not using XCode 4)
  * gpg
  * ccache
  * autoconf-2.13 - brew install https://raw.github.com/Homebrew/homebrew-versions/master/autoconf213.rb

## Configure

Run config.sh to get a list of supported devices:

    ./config.sh

And then run config.sh for the device you want to build for:

    ./config.sh [device name]

### Building against a custom Gecko

It can sometimes be useful to build against a different Gecko than the one specified in the manifest, e.g. a mozilla-central checkout that has some patches applied. To do so, edit .userconfig:

    GECKO_PATH=/path/to/mozilla-central
    GECKO_OBJDIR=/path/to/mozilla-central/objdir-gonk

## Build

Run build.sh or bld.sh to build B2G.

    ./build.sh

If you want to just build gecko or some other project, just specify it:

    ./build.sh gecko

## Flash/Install

Make sure your phone is plugged in with usb debugging enabled.

To flash everything on your phone:

    ./flash.sh

To flash system/userdata/boot partitions on fastboot phones:

    ./flash.sh system
    ./flash.sh boot
    ./flash.sh user

To update gecko:

    ./flash.sh gecko

To update gaia:

    ./flash.sh gaia

## Update Repos

To update all repos:

    git pull
    ./repo sync

To update a specific repo (eg, gaia):

    ./repo sync gaia

## Debug

To restart B2G and run B2G under gdb:

    ./run-gdb.sh

To attach gdb to a running B2G process:

    ./run-gdb.sh attach

## Test

To run the Marionette test suite on the emulator:

    ./test.sh

To run specific tests (individual files, directories, or ini files):

    ./test.sh gecko/dom/sms gecko/dom/battery/test/marionette/test_battery.py

Specify the full path if you're using a different Gecko repo:

    ./test.sh /path/to/mozilla-central/dom/battery/test/marionette/test_battery.py
