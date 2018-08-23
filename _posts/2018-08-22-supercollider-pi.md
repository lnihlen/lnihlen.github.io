---
layout: post
title: "Supercollider on Raspberry Pi, cont."
date: 2018-08-22
tags: [ supercollider, i_made_a_thing ]
---

Had a little more time today so followed
[these instructions](https://learn.pimoroni.com/tutorial/pi-lcd/getting-started-with-raspberry-pi-7-touchscreen-lcd)
to rotate the Pi screen so the plastic stand the Pi came with can now support
the screen correctly.

Then it was back to getting a checkout of supercollider and building everything.
I added ```-DCMAKE_INSTALL_PREFIX=~/usr/local``` to the ```cmake``` command
line arguments because I don't like having to invoke ```sudo``` every
compilation cycle, making my cmake command look like:

```
cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF \
  -DNATIVE=ON -DSC_WII=ON -DSC_IDE=ON -DSC_QT=ON -DSC_ED=OFF -DSC_EL=OFF  \
  -DSC_VIM=ON -DCMAKE_INSTALL_PREFIX=~/usr/local ..
```

The ```cmake``` command was failing due to missing QtWebEngine:

```
CMake Error at /usr/lib/arm-linux-gnueabihf/cmake/Qt5/Qt5Config.cmake:26 (find_package):
  Could not find a package configuration file provided by "Qt5WebEngine" with
  any of the following names:

    Qt5WebEngineConfig.cmake
    qt5webengine-config.cmake

  Add the installation prefix of "Qt5WebEngine" to CMAKE_PREFIX_PATH or set
  "Qt5WebEngine_DIR" to a directory containing one of the above files.  If
  "Qt5WebEngine" provides a separate development package or SDK, be sure it
  has been installed.
Call Stack (most recent call first):
  QtCollider/CMakeLists.txt:3 (find_package)
  lang/CMakeLists.txt:155 (include)
```

I noticed that parts of supercollider were already installed so I removed them
using ```sudo apt-get remove supercollider-server libscsynth1```

And then, Googling around, I discover
[a message](http://lists.qt-project.org/pipermail/qtwebengine/2014-November/000115.html)
on the Qtwebengine mail list, from November 2014, stating that QtWebEngine is
only supported on Embedded Linux (including Raspberry Pi) through Qt Enterprise.

Huh. So I guess that means building the help screen in the IDE is a no-go for
Raspberry Pi now? I want the IDE because one of the big attractions of the
Pi is to use that touchscreen sitting on top of my drumset, telling me what's
going on with the software part of my performance. I fired off an email to
the supercollider developers group to see if this is a known issue or if I
should open a ticket and pursue. Setting ```-DSC_IDE=OFF``` also doesn't seem
to help, as I think the dependency is coming from QT and not from the IDE.
This turns out to be because one can make a ```WebView``` object in the language,
as well as a ```HelpView```.

I got a timely response from one of the devs reminding me that the instructions
ask folks to build from the 3.9 branch of the repository, which is still relying
on the old QtWebKit browser. And now the Pi has chugged its way through
compilation successfully. I filed
[Issue 4010](https://github.com/supercollider/supercollider/issues/4010) with
supercollider, at the bare minimum I think it would make sense to bring that
documentation into revision control and update it to indicate the 3.10 is
known broken.

This is particularly interesting because (IIUC) QtWebEngine wraps Chromium for
the web rendering, which comes *preinstalled* on raspbian stretch, so it's not
as if there is a bunch of hard work to do here to get a web browser going on
the platform.

A colleague on the sc-dev team volunteered to try a different distro, Ubuntu
MATE, and we'll see if maybe this is a rasbian issue specifically.

