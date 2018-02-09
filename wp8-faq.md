Windows Phone 8: FAQ
====================


Why am I getting errors like "type `Foo.Bar` doesn't exist in target framework"?
--------------------------------------------------------------------------------


It's because Windows Phone 8 uses a different flavor of .NET called [.NET for Windows Phone](http://goo.gl/rvbZv) which is missing some of the types available on other platforms. You'll have to either replace these types with different ones or implement them yourself.


If you aren't using them, one of the scripting assemblies you're using is. Remove them one by one to find out which one it is.

Is there a platform define for Windows Phone 8?
-----------------------------------------------


Yes, it's UNITY_WP8.

How do I change screen orientation?
-----------------------------------


It has to be changed both in Unity Player Settings and Visual Studio MainPage.xaml file.

What are graphic capabilities of Windows Phone 8 devices?
---------------------------------------------------------


All Windows Phone 8 devices have GPUs that support feature level 9_3 of Microsoft Direct3D 11. Higher or lower feature levels are not available.

Is Windows Phone 7.5 supported?
-------------------------------


No.

How do I make "Development build" watermark go away?
----------------------------------------------------


For that watermark you go away, you have to build the project in Master configuration in Visual Studio.
