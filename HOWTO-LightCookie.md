How do I make a Spot Light Cookie?
==================================


Unity ships with a few __Light Cookies__ in the [Standard Assets](HOWTO-InstallStandardAssets). When the Standard Assets are imported to your project, they can be found in __Standard Assets-&gt;Light Cookies__. This page shows you how to create your own.

A great way to add a lot of visual detail to your scenes is to use cookies - grayscale textures you use to control the precise look of in-game lighting. This is fantastic for making moving clouds and giving an impression of dense foliage. The [Light Component Reference page](class-Light) has more info on all this, but the main thing is that for textures to be usable for cookies, the following properties need to be set:

To create a light cookie for a spot light:


1. Paint a cookie texture in Photoshop. The image should be greyscale. White pixels means full lighting intensity, black pixels mean no lighting. The borders of the texture need to be completely black, otherwise the light will appear to leak outside of the spotlight.
1. In the __Texture Inspector__ change the __Texture Type__ to __Cookie__
1. Enable __Alpha From Grayscale__ (this way you can make a grayscale cookie and Unity converts it to an alpha map automatically)


![](../uploads/Main/SpotlightCookie.png) 
