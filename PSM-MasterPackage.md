Creating a Master Package
===

This document explains how to create a Master Package from the completed Unity for PSM application and how to submit it to SCE.

## Master Package

A Master Package is a group of files that are required to distribute a Unity for PSM application from PlayStation&#174;Store.
The Master Package is also abbreviated and called a "master".
Submit the Unity for PSM application to SCE in this Master Package format.


### Unity for PSM Application Development Guidelines

Unity for PSM Application Development Guidelines (hereafter "guidelines") is a document summarizing the requirements for Unity for PSM applications.
You must comply with these guideline items when distributing Unity for PSM applications from PlayStation&#174;Store.
If you are planning to distribute an application from PS Store, please go over these guidelines before starting application development.
Moreover, confirm that the guideline items are satisfied before submitting the master.


### Creation and Submission Flow

The following is the procedure for creating and submitting a Master Package.

1. After Publisher License obtainment, register bank account information on DevPortal.
    * Note that a Master Package cannot be created before the completion of bank account information processing.
1. Read the guidelines and go over in advance the requirements for Unity for PSM applications.
1. Create a Unity for PSM application.
1. After development completion of this Unity for PSM application, confirm again that the application satisfies all applicable guideline requirements.
1. Create the Master Package following the "Procedure to Create a Master Package".
1. Submit the Master Package to SCE.
1. After submitting the Master Package, make settings for the Unity for PSM application and price/information regarding In-App Purchase on the Publish page of DevPortal.

## Procedure to Create a Master Package

Upon completing application development, create the Master Package as follows.

### Unity Editor Procedure

1. _Specify the platform._ Select [PlayStation&#174;Mobile] from the [Platform] list of [Build Settings] , press the [Switch Platform] button and keep the platform as [PlayStation&#174;Mobile)] .

1. _Create a copyright notice file._ Create a text file of copyright notices and place it on Assets/Plugins/PSM. Use UTF-8 for the character code.

    Example:
    ````
    Assets/Plugins/PSM/copyright.txt\\\
    ````
    copyright.txt contents:

    ````
	Copyright(C) 2014 FooBar Inc All Rights Reserved.
	````

1. _Specify the icon._ When using the Unity Pro version, it is possible to change the icon and splash image.
To change the icon and splash image, select [Build Settings] - [Player Settings...] and specify arbitrary image files for [Icon] and [Splash Image].

    ![Figure 1. Specify the icon](../uploads/Main/psm_icon_setting.png)

### Editing Application Information with the Publishing Utility for Unity

Click the [Open Publishing Utility] button from [Build Settings] and edit application information on the [Metadata] panel of the Publishing Utility for Unity.

### Common Property Tab

![Figure 2. Common Property Tab](../uploads/Main/PublishingUtilityMaster.png)

* **1. Development**
Set features used in the created application.

|**_Item name_** |**_Overview_** |**_Value to be set (Used: True; Not Used: False)_** |
|:---|:---|:---|
|GamePad |Enables/disables the gamepad. |Default value is True |
|Touch |Enables/disables the touch panel. |Default value is True |	
|Motion |Enables/disables the motion sensor. |Default value is False |
|Location |Enables/disables the location sensor. |Default value is False |
|Camera |Enables/disables the camera. |Default value is False |
|PS Vita TV |Enables/disables PS Vita TV. |Default value is False |

_Table 1. _

* **2. Application**

**Application ID**

The Application ID is used to identify applications. This will be used for identifying registered applications on DevPortal.
Set a name that is easy to identify using the [a-z, A-Z, 0-9, \_-] character set.

**Version**

Specify the version of the application. This value should be between 1.00 and 99.99 with two digits after the decimal point.
If there is already a version of the application that is sold in PS Store, the version specified here must be higher.
On the other hand, it is not always necessary to increment the version if the application is being resubmitted for master submission after it has been withdrawn during its first submission or if SCE has returned it after evaluation.

**Default Locale**

Specify the standard language to be used in PS Store. This will only be used when the end user's setting for the PS Store's display language is not defined on the application side. Select "en-Us" wherever possible.

* **3. Genre**

Specify the genre by which the application is to be handled in PS Store. Specification for the Primary genre is required whereas the Secondary genre is optional.

**Primary Genre**

This is used for categorizing and searching the application in PS Store.

**Secondary Genre**

Although this field can be set, it is not currently used. This will be used for searching the application in PS Store.

* **4. Developer**

**Website**

Specify the application/developers website for supporting application. The website specified here will be displayed on PS Store.

**Copyright Short**

Enter a one-line copyright note of the development source to be displayed in PS Store.

**Copyright**

Specify a UTF-8 text file with copyright information (maximum 64 KiB). Provide information of the developer, and the copyright information that should be displayed.
Copyright information related to SCE or PSM SDK will later be added on automatically at the end.

### Application Name Tab

Use the Application Name tab to set the application name for each applicable language.

![Figure 3. Application Name Tab](../uploads/Main/ApplicationName.png)

Input the Long Name and Short Name for each applicable language.

* Long Name is the formal name of the application. This will be displayed, for example, in PS Store.
* Short Name is the name displayed along with the PSM application icon.
* Long Name and Short Name can be the same.

The abbreviations in Locale correspond to the following languages.

|**_Locale_** |**_Language_** |
|:---|:---|
|en-US |English (U.S.) |
|en-GB |English (UK) |
|ja-JP |Japanese |
|fr-FR |French |
|es-ES |Spanish |
|de-DE |German |
|it-IT |Italian |
|nl-NL |Dutch |
|pt-PT |Portuguese |
|pt-BR |Portuguese (Brazil) |
|ru-RU |Russian |
|ko-KR |Korean |
|zh-Hant |Complex Chinese |
|zh-Hans |Simplified Chinese |
|fi-FI |Finnish |
|sv-SE |Swedish |
|da-DK |Danish |
|nb-NO |Norwegian |
|pl-PL |Polish |

``Table 2.``

### Rating Check Tab

Use the Rating Check tab to set the rating of the PSM application.

![Figure 4. Rating Check](../uploads/Main/RatingCheck.png)

Determine the rating using the following three check tools.

* PEGI Express (Pan European Game Information). European rating.
* ESRB Short Form (Entertainment Software Rating Board). North American rating.
* PlayStation&#174;Mobile Age Rating System. SCE Rating System.

If the specified genre for [Common Property] - [3. Genre] is a game, all three of the above rating checks must be performed.
If the specified genre is not a game, only perform a rating check using the PlayStation&#174;Mobile Age Rating System.

Click the URL or button on the tab, and determine the rating on each site.

The determination result with the highest value from among the three is applied as the rating of that PSM application.

After completing determination, enter the determination results in each field.

**Enter the PEGI express rating result**

When the rating check is completed using the PEGI express website, the file ``PEGIlicense_XXX.pdf`` can be obtained.

Age Rating Logo, Registered Number, and Content Descriptors information are described in the obtained file; enter the values in the fields corresponding to that information.

![Figure 5. PEGI](../uploads/Main/PEGI.png)

**Enter the ESRB Short Form rating result**

When the rating check is completed using the ESRB Short Form Web site, the file ``xxx.pdf`` can be obtained.

Rating Category and Certificate Code information are described in the obtained file; enter the values in the fields corresponding to that information.

![Figure 6. ESRB Short Form](../uploads/Main/ESRB.png)


**PlayStation&#174;Mobile Age Rating System**

To perform an SCE Rating System check, click the [Start Rating System] button.

Questions will be displayed in a wizard format. Answer the displayed questions until rating completes; the result will be automatically output to the Result field.

![Figure 7. PlayStation&#174;Mobile Age Rating System](../uploads/Main/PsmAgeRatingSystem.png)

Click the [Save] button once the edit is complete and close Publishing Utility for Unity.

### Building

Once the above settings are complete, select [Master] from [Build Settings] - [Build Type] drop down list of the Unity Editor and click the [Build] button.

![Figure 8. Build Settings](../uploads/Main/PsmBuildSettings.png)

Follow the instructions displayed in the dialog to make your input.
A **psmp** file will be created when the build succeeds.
When the Master Package is created, a dialog box will be displayed to confirm whether or not to submit the Master Package - make selection as appropriate.

## Submitting the Master Package

To manually submit the Master Package, select [Menu] - [File] - [Submit Master Package...] of the Publishing Utility for Unity. Follow the instructions displayed in the dialog to make your input.

### Operations on DevPortal

Once completing master submission, make information/price settings on the Publish page of DevPortal. ``https://psm.playstation.net``

## Master Package Creation Procedure When the Developer and Publisher Differ

When the following conditions apply, create the Master Package as follows.

* The developer and publisher differ.
* The developer does not want to disclose the source code to the publisher.
* The publisher does not want to disclose the SEN account and password to the developer.

### Developer Work

1. Once application development is complete, perform the above operation from [Unity Editor Procedure] to [Specify the icon] .
1. Select [Intermediate] from [Build Settings] - [Build Type] drop down list of the Unity Editor and click the [Build] button.

    ![Figure 9. Build Type - Intermediate](../uploads/Main/BuildSettingsIntermediate.png)

1. A dialog to specify the output destination will be displayed; specify the output destination.
1. When output completes, pass the exported folder to the publisher.

### Publisher Work

1. Receive the exported folder from the developer.
1. The exported folder will be configured as follows. Open Publishing Utility for Unity and edit app.xml inside in the same manner as the above [Editing Application Information with the Publishing Utility for Unity] procedure.

    ````
	(exported_folder/)
		Application-unsigned/
		app.xml    //<--
		copyright.txt
		edata_list.txt
		icon_128x128.png
		icon_256x256.png
		icon_512x512.png
		splash_854x480.png(:codeend:)
    ````
1. Save once the edit process is complete.
1. Select [Menu] - [Create Master Package...] of the Publishing Utility for Unity. A dialog to specify the exported folder will be displayed; specify the exported folder. 
Subsequently, follow the instructions displayed in the dialog and make your input.
1. The Master Package will be created when build succeeds.
