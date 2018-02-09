Getting started
===============

HoloLens applications are Universal Windows Applications, and follow the same general guidelines as other Windows Store applications. The development environment is Visual Studio 2015, and does not require an additional SDK installation.

See Microsoft's documentation on [Holograms](https://dev.windows.com/en-us/holographic/Hologram) for more information.

Major differences
-----------------

HoloLens is an Augmented or Mixed Reality device, and is different to other standalone and mobile platforms. Windows Holographic applications can be just like standard Virtual Reality experiences that take over the user's visual experience, but the strength of Windows Holographic lies in being able to interact with the user's reality. 

Here is a summary of the differences you need to consider when developing Windows Holographic applications:

* **The device is power sensitive.** HoloLens is a mobile device and, much like a phone, applications need to be responsible with power. Ensuring you disable features and optimize for CPU utilization is more important than on other platforms.

* **Holograms do not replace reality.** Unlike a Virtual Reality environment, the HoloLens augments and interacts with your environment. Holograms are additive and drawn over the world.

* **Input paradigms are different.** Gaze (where the user is looking), gesture (hand signals that the device can interpret as commands) and voice (spoken commands) are the primary forms of input. This is a significant shift from conventional input methods.
