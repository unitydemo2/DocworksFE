# Getting started with Samsung TV development

Adapting your game for Samsung Smart TV is much like porting your game to any other platform with Unity. The hardware in the TV is very similar to mobile devices (ARM CPU + OpenGLES GPU), so you can expect similar performance metrics.

## Setting up and building your Unity project for Samsung TV

* Open Unity with Samsung TV support.

* In the Unity menu bar, go to __File__ > __Build Settings__ and switch the __Build Target__ to __Samsung TV__.

* Get the IP address of the TV from the TV’s __Unity Launcher__ app.

* In the Unity menu bar, go to __Edit__ > __Project Settings__ > __Player__, open __Publishing Settings__ and type the TV’s IP address into the __Device Address__ field (see image below).

* For multiple TVs, type all IP addresses, separating each one with a forward slash ("/") as shown in the image below.

![](../uploads/Main/samsungtv-gettingstarted-setuptv.png)

* In the Unity menu bar, go to __File__ > __Build and Run__, select __Samsung TV__ and then click the __Build and Run__ button. This builds your project and runs it on all TVs correctly set up in Unity.


## TV models

There are several different Samsung TV models released each year. Unity works on the following models:

###2015 models

* 2015 Standard Series
* 2015 Premium Series (Mali-T760)

###2016 models

* 2016 Standard Series
* 2016 Premium Series

Note that premium models have a faster CPU and higher end GPU.

## Input devices

The input mechanism is different depending on the model of TV.

2015 models have no touchpad. They have an accelerometer in the remote as well as air mouse capabilities.

2016 models have IR-only remotes and instead gamepads are used to provide primary input.

Unity makes dealing with different input devices easier by providing input modes. See the [Samsung TV Input](samsungtv-input) section for more details on input modes.

## Platform-specific code

To selectively compile in code for Samsung TV, use the following:

```
#if UNITY_SAMSUNGTV
    // Samsung TV specific code
#endif
```

Note that this is also active for the editor.

To check at runtime if you are running on Samsung TV, use:

```
if (Application.platform == RuntimePlatform.SamsungTVPlayer)
{
    // Samsung TV specific code
}
```

You can obtain the model like this:

```
SystemInfo.deviceModel
```

Possible return values include:

```
STANDARD_15
STANDARD_16
```

This allows you to differentiate between TV years.

## Samsung documentation

Samsung provides documentation on developing for Samsung Smart TV on [Samsung's developer forum](http://www.samsungdforum.com/). A lot of the information on this site does not apply to Unity users (it mainly supports web/Flash applications), but you might still find some of it useful.

## Submitting your application to the Samsung Apps TV store

In order to distribute your application to Samsung Apps TV store, you need to register your application and it must go through a certification process provided by Samsung or its affiliate at [Seller Office](http://seller.samsungapps.com/) before being launched on the store.

