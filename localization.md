### **_Localization  Documentation_**

# About Localization

The Localization package provides tools for adding support for multiple langauges and regional variants to your application. For example, supporting text in multiple languages or culture specific assets such as audio or textures.

## Requirements

This Localization version *0.1.0* is compatible with the following versions of the Unity Editor:

* 2018.2 and later (recommended)

## Known Limitations

The Localization version 0.1.0 includes the following known limitations:

* Only supports defining supported locales, no actual text or asset localization support.
* Custom locales are not supported via the inspector.

# Package Contents

The following table provides an alphabetical list of the important files and folders included in this package.

|Folder or Filename|Description|
|---|---|
|Runtime/Public|Folder containing public API for player use.
|Runtime/Public/Locale.cs|Script class that represents a language. It supports regional variations and can be configured with an optional fallback locale.
|Runtime/Public/LocalizationManager.cs|Script class that represents the localization manager for the project. The manager is responsible for handling all localization of the application, it manages the active locale and contains various localization events that can be subscribed to. Only one LocalizationManager should be active at one time and in most cases there will only ever need to be one for the lifetime of the application.
|Runtime/Public/StartupLocaleSelector.cs|Script class that determines the locale to use when the application first starts. Implments the IStartupLocaleSelector interface.
|Runtime/Public/SupportedLocales.cs|Script class that contains the list of Locales that the appliaction supports. Implements the ISupportedLocales interface.
|Runtime/Tests|All playable tests for the localization system. Used to verify no issues are introduced when making changes.
|Editor/Tests|All Editor tests for the localization system. Used to verify no issues/bugs are introduced when making changes.
|Samples/Scripts|Example scripts to demonstrate using the localization system.

# Using Localization

## Localization Settings

The Localization Settings is a Prefab that contains all the components required for localizing the application. Each component can be replaced with a custom version by implmenting the relevent interfaces.

A new Localization Settings asset can be created from the menu *Assets/Create/Localization/Localization Settings*. It is possible to have multiple Localization Settings assets per project although most use cases will only require one. The active Localization Settings asset will be automatically included into the build and so does not need to be referenced through scripts or added to a scene.

*Default Localization Settings*<br/>
![alt text](../uploads/packmanLocalizationSettingsInspector.png)

## Localization Manager

The manager is responsible for handling all localization of the application, it is the core component.

*Localization Manager Editor*<br/>
![alt text](../uploads/packman/LocalizationManagerInspector.png)

|Property                |Description
|:---                    |:---
|Active Settings         |The active settings is the current Localization Manager being used to localizae this project. The assigned manager will automatically be included into a built player during the build process.
|Use External Data       |During a player build various localization data will be generated. The data can either be built into the Resources directory so that it is internal or build externally using the StreamingAssets system. By using external data changes can be made after a build to allow for rapid iteration and even possible modding support for a game. <br/><br/>*Example output when using External data.* ![alt text](../uploads/packman/ExternalDataExample.png)
|Localization Director   |The name of the directory where all localiation data will be stored internally and/or externally.

## Startup Locale Selector

The Startup Locale Selector component is used by the Localization Manager to determine what locale should be used when the application starts.

*Startup Locale Selector Editor*<br/>
![alt text](../uploads/packman/StartupLocaleSelectorInspector.png)

|Property                |Description
|:---                    |:---
|Startup Order           |This is a list of behaviors that can be used to select a locale. When attempting to select a locale each behavior will be tried starting with the top, until one succeeds. The list items can be dragged and reordered in the inspector. <br/><br/>**Command Line:** If a locale is provided to the application using the provided command line argument. If the field is left blank then the behavior will be disabled. <br/><br/>**System Locale:** The locale being used by the users system will be used if it is supported by the current SupportedLocales component.<br/><br/>**Default Locale:** The default locale from the SupportedLocales component will be used.

## Supported Locales

Contains the list of locales supported by the application.

*Supported Locales Editor*<br/>
![alt text](../uploads/packman/SupportedLocalesInspector.png)


|Property                |Description
|:---                    |:---
|Default Locale          |This is the default locale to use by StartupLocaleSelector or if no selector is present.
|Supported Locales       |This mode allows for selecting what locales your application will support. The list of locales is taken directly from the [CultureInfo class](http://msdn.microsoft.com/en-us/library/system.globalization.cultureinfo(v=vs.110).aspx).
|Customize Locales       |This mode allows for modifying the selected locale names.
|Customize Fallbacks     |In this mode it is possible to customize the locale fallbacks. To change the fallback for a locale first select and then drag the locale, drop it onto its new parent to confirm the new fallback.

### Note

* For examples on using the LocalizationSettings see  *Samples/Scripts/LocalizationSettings/*.

# Document Revision History

|Date|Reason|
|---|---|
|Nov 10, 2017|Document created. Matches package version 0.1.0|

