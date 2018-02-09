# Splash Screen

The Unity Editor allows you to configure a Splash Screen for your project. The level to which you can customize the Unity Splash Screen depends on your Unity license; depending on which licence you have, you can disable the Unity Splash Screen entirely, disable the Unity logo, and add your own logos, among other options. 

You can also make your own introductory screens or animations to introduce your project in your first [Scene](CreatingScenes), using the the Unity [UI System](UISystem). These can be in addition to or instead of using the Unity Splash Screen, depending on your license.

The Unity Splash Screen is uniform across all platforms. It displays promptly, displaying while the first Scene loads asynchronously in the background. This is different to your own introductory screens or animations which can take time to appear; this is due to Unity having to  load the entire engine and first Scene before displaying them. 


##License limitations

The Unity Pro Edition and Plus Editions licenses have no limitations to customisation of the Unity Splash Screen.

The Unity Personal Edition license has the following limitations:

* The Unity Splash Screen cannot be disabled.
* The Unity logo cannot be disabled.
* The opacity level can be set to a minimum value of 0.5.

## Unity Splash Screen settings

To access the Unity Splash Screen settings, go to __Edit__ > __Project Settings__ > __Player__. In the Inspector window, navigate to __Splash Image__ > __Splash Screen__.


![Splash Screen settings](../uploads/Main/SplashScreenSettings.png)

|**Property** | **Function**|
|:---|:---|
|__Show Splash Screen__ | Tick the __Show Splash Screen __checkbox to enable the Splash Screen at the start of the game. In the Unity Personal Edition you cannot disable this option; the checkbox is always ticked. |
|__Preview__ | Use the __Preview__ button to see a preview of the Splash Screen in the Game view. The preview reflects the resolution and aspect ratio of the Game view. Use multiple Game views to preview multiple different resolutions and aspect ratios simultaneously. This is particularly useful for simulating the Splash Screen’s appearance on multiple different devices.<br/><br/>See _Image A_, below, for an example.|
|__Splash Style__|__Splash Style__ controls the style of the Unity branding. There are two options available: Light on Dark, or Dark on White. See these in _Image B_, below.|
|__Animation__|The Splash Screen has 3 possible animation modes, which define how it appears and disappears from the screen.
|&nbsp;&nbsp;&nbsp;&nbsp;Static| The Splash Screen has no animation. |
|&nbsp;&nbsp;&nbsp;&nbsp;Dolly| The logo and background zoom to create a visual dolly effect. |
|&nbsp;&nbsp;&nbsp;&nbsp;Custom| Configure the background and logo zoom amounts to allow for a modified dolly effect. |
|Show Unity logo|Tick the __Show Unity Logo__ checkbox to enable Unity co-branding. In the Unity Personal Edition you cannot disable this option; the checkbox is always ticked.|
|__Draw Mode__| __Draw Mode__ controls how Unity co-branding is shown (if Unity co-branding is enabled).|
|&nbsp;&nbsp;&nbsp;&nbsp;Unity Logo Below| Draws the co-branding Unity logo beneath all logos that are shown. |
|&nbsp;&nbsp;&nbsp;&nbsp;All Sequential| Inserts the co-branding Unity logo as a logo into the __Logos__ list. |
|__Logos__ |This is the customisable list of logos to be drawn during the duration of the Splash Screen. See the Logo list in _Image C_, below.<br/><br/>Add and remove logos using the plus (+) and minus (-) buttons, and reorder logos in the list by dragging and dropping. Each logo must be a Sprite Asset. To change the aspect ratio of the logo, change the dimensions of the Sprite using the [Sprite Editor](http://spriteeditor), with __Sprite Mode__ set to __Multiple__.<br/><br/>The __Logo Duration__ of the Sprite Asset is the length of time the logo appears for. This can be set to between a minimum of 2 seconds and a maximum of 10 seconds.<br/><br/>If an entry in the Logos list has no logo Sprite Asset assigned, no logo is shown for the duration of that entry. You can use this to create delays between logos.<br/><br/>The entire duration of the Splash Screen is the total of all logos plus 0.5 seconds for fading out. This might be longer if the first Scene is not ready to play, in which case the Splash Screen shows only the background image or color and then fades out when the first Scene is ready to play.|
|__Overlay Opacity__|Adjust the strength of the __Overlay Opacity__ to make the logos stand out; this affects the background color and/or image color,  based on the __Splash Style__.<br/>Set __Overlay Opacity__ to a lower number to reduce this effect, or set it to 0 to disable the effect completely. For example, if the Splash Screen style is __Light on Dark,__ with a white background, the background becomes gray when __Overlay Opacity__ is set to 1, and white when __Overlay Opacity__ is set to 0.<br/><br/>In the Unity Personal Edition, this option has a minimum value of 0.5.|
|__Background Color__|Use this to set the background color when no background image is set. Note that the actual background color may be affected by the __Overlay Opacity__ (see section above), and might not match the assigned color. |
|__Background Image__|Use this to set a background Sprite image instead of using a color background. Unity adjusts the background image so that it fills the screen; the image is uniformly scaled until it fits both the width and height of the screen. This means that parts of the image might extend beyond the screen edges in some aspect ratios. To adjust the background image’s response to aspect ratio, change the Sprite’s __Position__ values in the Sprite Editor.<br/><br/>Use __Alternate Portrait Image__ to set an image with portrait aspect ratios (for example, a mobile device in portrait mode). If there is no __Alternate Portrait Image__ Sprite assigned, the Unity Editor uses the Sprite assigned as the __Background Image__ for both portrait and landscape mode.<br/><br/>Adjust the __Position__ and dimensions of the Sprite in the Sprite Editor to control the aspect ratio and position of the background image on the Splash Screen. In _Image D_, below, the same image is being used for both landscape and portrait; however, the portrait position has been adjusted.|




![Image A: __Preview__ - Multiple previews](../uploads/Main/SplashScreenPreviews.png)

![Image B: __Splash Style__ - On the left, Light on Dark style. On the right, Dark on Light style.](../uploads/Main/LogoStylesSideBySide.png)

![Image C: __Logos__ - The Logo list and __Logo Duration__](../uploads/Main/SplashScreenLogos.png)

![Image D: __Background Image__ - The same  is being used here for both landscape and portrait](../uploads/Main/SplashScreenSpriteEdit.png)