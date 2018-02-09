Unity's Xbox One Plugins
========================

The Xbox One like many consoles has a number of unique features only found on the Xbox One. Some of these include the Kinect and Xbox Live. 

On the Xbox One Unity now provides support for these platform specific features through a set of plugins. Using plugins allows us to extend the plugins and fix bugs independently from the editor and player. In addition the plugins can be made to span versions of the Editor allowing you to upgrade your editor or the plugins as needed when preparing to ship.

In addition, we have chosen to release full source for the plugins in the hopes of facilitating a dialog with our community on improving these, and empowering you to extend them as needed.

You can obtain these plugins from Unity in the same way you received the Editor and the Add-On for Xbox One.

Plugins ship with an independent set of documentation and are usually shipped in library pairs.

- A native plugin that wraps the Microsoft API.
- A managed native plugin that pulls in the native 
  functionality into CSharp and improves the usability of the native API.

Consuming these involves dropping the set of plugins into your project, specifying the platform these should be built into. Plugins also ship with an independent log plugin that helps with interpreting the HResult error codes returned from platform specific APIs. The plugin should not be included in shipping products but is essential for development.