# Mixed Reality Devices

Unity provides built-in support for a number of Mixed Reality (MR) devices.

Device availability is on a per-platform basis, meaning that not every device is available for every platform. Multiple devices are available on certain platforms, and you can choose which MR devices your app will support from the available list.

At runtime, only one device can be active at any given time. However, it is possible to switch between devices if you have chosen to support multiple devices in your application.

##MR device information

XRDevice.family is a string corresponding to the current XRSettings.loadedDeviceName. A family can have multiple models, which have different characteristics. The model can be accessed with XRDevice.model.