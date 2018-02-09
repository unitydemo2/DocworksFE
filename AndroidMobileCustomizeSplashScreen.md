#Customizing an Android Splash Screen

If you use Unity Personal Edition to make your project, a default splash screen displays while your game loads. It is oriented according to the __Default Screen Orientation__ option in the [Player Settings](class-PlayerSettings). You cannot change this splash screen.

Unity Professional Edition users can change the splash screen. You can use any texture in the project as a splash screen. You can set the texture from the Splash Image section of the Android [Player Settings](class-PlayerSettings). You should also select the __Splash scaling__ method from the following options:-

* __Center (only scale down)__ draws your image at its natural size unless it is too large, in which case it is scaled down to fit.
* __Scale to fit (letter-boxed)__ draws your image so that the longer dimension fits the screen size exactly. Empty space around the sides in the shorter dimension is filled in black.
* __Scale to fill (cropped)__ scales your image so that the shorter dimension fits the screen size exactly. The image is cropped in the longer dimension.

