Getting started with v4l4j is easy. The next set of pages will walk you through the steps to install and test v4l4j. After that, read about the v4l4j API and start using it !

### Install on Intel platforms ###
You have two options:
  * You can take the easy route and install the Debian/Ubuntu v4l4j packages in just a few commands. [This page](DebianInstall.md) shows you how.
  * The less-easy option: manually download the source code, build it and install it. Instructions are on [this page](SourceInstall.md).


### Install on ARM platforms ###
**v4l4j support for ARM platforms is still experimental** and currently limited to the two ARM devices I own: a [RaspberryPi](http://raspberrypi.org) and a [BeagleBoard XM](http://beagleboard.org). Here again, you have two options:
  * Build v4l4j on the target itself. Instructions for the RPi can be found [here](GettingStartedOnRPi.md).
  * Cross-compile v4l4j and copy it to the target. Instructions for cross-compiling for RPi and BeagleBoard XM can be found [here](CrossCompilingForARM.md)

### Testing ###
Once you have successfully installed v4l4j, you can test it as explained [on this page](TestingV4l4j.md).

### v4l4j API ###
You can read about the main v4l4j classes are presented on [this page](Examples.md), and have a look at the many example applications that come with v4l4j (listed [here](TestingV4l4j.md)). The javadoc can be found [here](http://v4l4j.googlecode.com/svn/www/v4l4j-api/index.html).