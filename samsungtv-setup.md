#Samsung TV Setup

## What you need
1. 2015 or 2016 Samsung Smart TV (see [Getting Started](samsungtv-gettingstarted))
1. USB drive formatted FAT32 with enough space to store your games, inserted into TV
1. TV must be on same network as development computer (accessible via IP address)

## Install Unity Launcher
Unity Launcher is an app that runs on your Samsung TV which allows you to install, manage and run Unity Games.

Your TV must be connected to the internet in order to access the Samsung App Store.  The Unity Launcher application can be found in the Information section of the Samsung App Store.  Please install this application and launch it.

### 2015 and 2016 TVs

1. Turn on the TV.
2. Press the __Smart TV__ button on the remote to launch the Smart Hub.
2. Navigate to the __Apps__ screen and select the __Information__ category.
4. Find __Unity Launcher__ in the list and install it.
5. Launch __Unity Launcher__ from the Smart TV Hub app list.

## Unity Setup
* Open Unity with Samsung TV support.
* In __File__ > __Build Settings__, switch the __Build Target__ to __Samsung TV__.
* Get the IP address of the TV from __Unity Launcher__.
* Insert the TV's IP address into __PlayerSettings__ > __Publishing Settings__ > __Device Address__.

![](../uploads/Main/samsungtv-deviceaddress1.png)

![](../uploads/Main/samsungtv-deviceaddress2.png)

* Select __Build and Run__ to run the project on the TV.

