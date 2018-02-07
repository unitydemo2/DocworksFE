VR devices
==========
<!-- https://trello.com/c/Qw7imxOL -->
Unity provides built-in support for a number of virtual reality devices.

Device availability is on a per-platform basis, meaning that not every device is available for every platform. Multiple devices are available on certain platforms, and you can choose which VR devices your app will support from the available list.

At runtime, only one device can be active at any given time. However, it is possible to switch between devices if you have chosen to support multiple devices in your application.

##VR device information

[XRDevice.family](ScriptRef:XR.XRDevice-family.html) is a string corresponding to the current [XRSettings.loadedDeviceName](ScriptRef:XR.XRSettings-loadedDeviceName.html). A family can have multiple models, which have different characteristics. For example, Oculus has DK2, Gear VR, etc. The model can be accessed with [XRDevice.model](ScriptRef:XR.XRDevice-model.html).