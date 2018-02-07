# Creating and changing Remote Settings

Before using Remote Settings, you must first enable [Unity Services](SettingUpProjectServices) and the [Unity Analytics Service](UnityAnalyticsOverview) for your Unity project. Once you have enabled Analytics, open the Analytics Dashboard and go to the __Remote Settings__ tab to create and change the Remote Settings values. See [Using Remote Settings in a Unity project](UnityAnalyticsRemoteSettingsUsing) to learn how to access these Remote Settings values in your game or application.

The Analytics Service provides two Remote Settings configurations:

1. The Analytics Service sends Release configuration settings to computers and devices running regular, non-development builds of your application.

2. The Analytics Service sends Development configuration settings to computers and devices running development builds (that is, builds created with the Development Build flag checked on the [Build Settings window](BuildSettings)). Play mode in the Unity Editor counts as a development build.

![The Remote Settings tab on the Analytics Dashboard for a game called Raging Bots](../uploads/Main/AnalyticsRemoteSettingsTab.png)

Each Remote Setting consists of a key, a default value, and, optionally, segmented values. When a setting contains segmented values, the segments that the current player is in determine which values are included in the configuration. If more than one segment applies, the configuration includes the value from the highest priority segment.

You can create 200 values per configuration. A setting with one segment, uses one value; a setting with two segments uses two; and so on.

## Setting names and value rules

An individual remote setting is a key-value pair. The rules for key names are:

* Key names must be unique within the same configuration.

* Key names must start with a letter.

* Key names may contain only letters, digits, and the characters: ".", "_", and "-".

A setting value can be any of the following primitive types: __Int__, __Float__, __String__, or __Bool__. The rules for setting values are:

* Int values are 32-bit integers (-2147483648 to 2147483647).

* Float values are single-precision, 32-bit floating-point numbers (about -3.4x10^38 to 3.4x10^38).

* Strings are limited to 1024 characters.

* You must specify boolean values with the strings "true" or “false”.

## Adding Remote Settings

To add a Remote Setting:

1. In your [Analytics Dashboard](https://analytics.cloud.unity3d.com/), open the __Remote Settings__ tab.

2. Set __Configuration__ to __Release__ or __Development__ for the setting.

3. Click __ADD NEW KEY-VALUE__ (at the top of the settings list). 

3. Enter a name for the key.

4. Set the type for the value.

5. Enter the default value.

6. Click the __Save__ button.

7. Click the __Sync__ button to publish your changes. (You do not need to click the __Sync__ button after creating each individual setting; you can wait to synchronize your settings until you finish making all changes to the current configuration.)

__Note:__ To add values targeted to different segments, save the default key-value setting and then edit it. The segment options only appear when you edit a setting, not when you first create one.

## Editing Remote Settings

To edit a Remote Setting:

1. Open the __Remote Settings__ tab in your Analytics Dashboard.

2. Choose the __Release__ or __Development__ __Configuration__.

3. Click the edit icon next to the setting you want to change.

    ![](../uploads/Main/RemoteSettingsEditSetting.png)

4. Make your changes. Note that changing a key name has the same effect as deleting the old key and creating a new one.

5. Click the __Save__ button. 

6. Click the __Sync__ button to publish your changes. Unity reads the updated settings the next time players start a session.  


## Resolving simultaneous edits

If two people on your team edit the Remote Settings on a project at the same time, you can get a conflict when trying to synchronize the modified settings with the service.


![Warning that someone else has changed the settings while you were editing the same project](../uploads/Main/RemoteSettingsEditConflict.png)

When a conflict occurs, you have the following options:

__OVERWRITE__

Discards all changes on the service since you last synced and pushes your settings to the service. When you choose overwrite, the settings on the service will match your current settings exactly.

__MERGE__

Combines your current settings with the modified settings from the service and gives you the opportunity to make changes before completing the synchronization operation. 

If you edit the same setting value, your changes overwrite the version from the service. In addition, values and settings deleted on the service are restored (since they still exist in your version). Otherwise, changes from the service since you last synced are retained.

After merging, your Remote Settings page is updated to reflect the merger, but the combined settings are not pushed to the server. You can review the updated changes and click the __Sync__ button again when you are ready.

__CANCEL__

Cancels the synchronization operation and closes the conflict dialog without making any changes. Your settings are not saved to the service.


## Adding different values for different segments

You can assign multiple segmented values to a single Remote Settings key. When a player is a member one of the segments for which a specific value exists, Unity sends that value to the player instead of the default, __All Users__ value. (If a player qualifies for several segmented values, Unity sends the value from the highest priority segment.)

To set a value specific to a given segment:

1. Open the __Remote Settings__ tab in your Analytics Dashboard.

2. Choose the __Release__ or __Development__ Configuration.

3. Add the Remote Setting if it does not already exist.

4. Click the edit icon at the far right of the setting.

5. Click __ADD EXISTING SEGMENT__.  

6. In the new row, choose the segment from the drop-down list and enter a value.

7. Click the __Save__ button.

## Deleting Remote Settings

To delete a Remote Setting, first open the edit view for the setting:

1. Open the __Remote Settings__ tab in your Analytics dashboard.

2. Set __Configuration__ to __Release__ or __Development__ for the setting.

3. Click the edit icon next to the setting you want to delete to open the edit view:

    ![](../uploads/Main/RemoteSettingsDelete.png)
    
4. To delete a value for a particular segment, click the __minus__ button to the right of the edit view and then click __Save__. (You cannot delete the default __All Users__ value.)

5. To delete the entire setting, click the delete icon at the bottom of the edit view and then confirm you want to delete the setting.

6. Click the __Sync__ button to publish your changes.


## Setting segment priority

When a player is a member of more than one segment, Unity sends the value assigned for highest priority segment. (If a setting doesn’t have any segmented values, or the player isn’t a member of the segments that do have different values for a key, then Unity sends the All Users value.) You can set the order of your segments to specify which segmented values should take precedence when there is an overlap. 

To set the segment priority:

1. Open the __Remote Settings__ tab in your Analytics dashboard.

2. Choose the __Release__ or __Development__ Configuration.

3. Click the segment priority icon.
    
    ![](../uploads/Main/RemoteSettingsPriorityIcon.png)


4. The __Segment Priority__ window opens, showing your current order. Only segments already assigned values for any Remote Settings appear in the window.

5. Reorder the segments by clicking and dragging the items into place.


    ![](../uploads/Main/RemoteSettingsSegmentOrder.png)

6. When the order is correct, click __Save__.  

7. Click the __Sync__ button to publish your changes.

The segment priority applies to all settings within a configuration, but you can have a different priority for the Development and Release configurations.

## Importing and Exporting Settings

You can import and export settings using  comma-separated-value (CSV) format files.

__To export your current settings:__

1. Navigate to the Remote Settings page on your Unity Analytics Dashboard.
2. Choose the configuration, either __Release__ or __Development__ that you want to export.
3. Click the menu icon at the right side of the list header:
 
    ![](../uploads/Main/AnalyticsRSMenuIcon.png)

4. Choose __Download CSV__ to export the current settings to your computer.

   The Analytics Service downloads your current settings as a CSV file.
   
Note that if you download the CSV file before creating any setting, the file is completely empty. A valid file for uploading must contain the header row. See [Remote Settings CSV Format](#csvformat).
   
__To import settings into your project:__

1. Navigate to the Remote Settings page on your Unity Analytics Dashboard.
2. Choose the configuration, either __Release__ or __Development__ that you want to overwrite with the imported settings.
3. Click the menu icon at the right side of the list header.
4. Choose __Upload CSV__ to import a new settings file to the project.
5. Choose the CSV file containing the new settings. 
6. Click __Open__.

    The Analytics Service uploads the settings file and replaces all the current settings in the selected configuration, but does not commit the values yet.
    
    If a format or value error exists in the file, the service gives you an option to download a CSV file detailing the errors. No changes are made to the settings when an error occurs.
   
7. Click __Sync__ to commit the setting changes and make them live. (Refresh the page or navigate away without synchronizing to discard any uploaded settings.)

When you import settings, **ALL** the keys and values are changed to match the uploaded file. If an existing setting or segment value does not appear in the file, that setting is deleted.

### Creating and Deleting Settings during Import

In addition to editing setting values, you can create and delete settings when you upload a CSV file to for a configuration.

First, download the current setting CSV file for the configuration. You can then edit this file to make your changes. (See [Working with Spreadsheets](#spreadsheets)) if you use a Spreadsheet application to edit the file.)

__To create a new setting:__

1. Add a new row in the file. 
2. Specify a unique key name.
3. Define the data type (int, float, string, or bool).
4. Enter "All Current Users" as the segment.
5. Leave the last field blank (for the default segment).

A new setting will look like:

```
a_bool_value,bool,TRUE,All Current Users,
```

__To add a new segmented value for a setting:__

1. Add a row to the file.
2. Repeat the key name and data type of the setting.
4. Enter the value for the segment.
5. Enter the segment name. The segment name must already be defined for the project before you import the settings. Use the [Segment Builder](UnityAnalyticsSegmentBuilder) page to view the existing segments as well as define new ones.
6. Set the segment priority. 
    
    The priorities for all segments in the file must be consecutive integers starting with 1. For example, if you use five segments in your CSV file, the only priorities that are allowed are the numbers 1-5. The same priority must be assigned wherever in the file that a segment is used. For example, if you use the Japan segment for a dozen values in your CSV file, the same priority value must be used in each row.

A setting with segmented values will look like:

```
a_bool_value,bool,false,All Current Users,
a_bool_value,bool,true,1-3 Days,1
a_bool_value,bool,false,4-7 Days,2
```

__To delete a setting:__

Simple delete the row defining the setting from the file. If you delete the row containing the default, "All Current Users" segment, you must also delete any rows defining segmented values. Note that if you delete segmented values you might also need to renumber the segment priorities to maintain the consecutive integer sequence.

Finally, uploaded the modified CSV file and press the __Sync__ button on the Remote Settings page to save the changes and publish the changes.

<a name="csvformat"></a>
### Remote Settings CSV File Format

The Remote Settings CSV format conforms to [ISO rfc4180](https://tools.ietf.org/html/rfc4180). The exported file is encoded as UTF-8.

The settings file has five fields. You must include the header row as the first line in the file:

```
key,type,value,segment,priority
```

The fields in the file are: 

* __key__ -- The name of a Remote Settings key.
* __type__ -- the setting data type: int, float, string, or bool.
* __value__ -- the setting value.
* __segment__ -- the name of the segment for a setting value. 
* __priority__ -- the priority of the segment for a setting value.

**Rules for entries in the CSV file:**

* Each row must contain a unique combination of key and segment.
* All segments in the CSV file must already exist. New segments must be created using the [Segment Builder](UnityAnalyticsSegmentBuilder) page of the Analytics Dashboard.
* Use the string, "All Current Users" for the default segment.
* The default "All Current Users" segment must be associated with each key exactly once in the file.
* Do not assign a priority to the "All Current Users" segment (leave the field blank). 
* Priorities for all other segments must be assigned.
* A segment priority must be the same for all keys that segment is used in. 
* The segment priorities assigned across all segments must be consecutive integers (starting with 1).
* Use TRUE and FALSE for Boolean values.
* Strings containing commas, double quotes, and line breaks must be enclosed with double-quote characters.
* Double quote characters in a string must be escaped by repeating the double quote. For example:

    ```
    "Hello World!"            -> """Hello World!"""
    He said, "How do you do?" -> "He said, ""How do you do?"""
    ```
    
* The file can contain up to 201 rows (including header).

**Tip:** Create sample Remote Settings values on the dashboard and download to generate a sample file. 

<a name="spreadsheets"></a>
### Working with Spreadsheets

The CSV file format is not rigorously standardized, so you may experience variations when opening or saving CSV files in different spreadsheet applications. Always test that the fields in your Remote Settings file are properly preserved after making the round trip from the Remote Settings page, to your editing application, and back. Especially check that Unicode characters (Emoji, symbols, characters outside the basic ASCII range, etc) are not altered and that floating point numbers are not truncated.

Usually when importing a CSV file, spreadsheet applications interpret strings starting with `'`, `+`, `-`, or `=` characters as expressions rather than plain strings. You can try enclosing such strings in double quotes and adjusting the import options of the spreadsheet you are using. For example, in Google Sheets you can turn off the "Convert strings to numbers and dates" option; while in LibreOffice you can turn on, "Quoted Strings As Text".

For settings of type float, make sure that all significant digits of the setting value are displayed in the spreadsheet cell. Otherwise, the spreadsheet application truncates the value and you lose precision when you export the spreadsheet to a CSV file. 

---

* <span class="page-edit">2017-12-12 <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-edit">2017-08-28 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>

* <span class="page-edit">2017-06-30 - Added: Allow the characters ".", "_", and "-" in key names.</span>

* <span class="page-edit">2017-06-30 - Added: CSV import and export.</span>

* <span class="page-history">New feature in 2017.1</span> 

* <span class="page-history">2017-08-28 - Added segmented Remote Settings: set different values for different segments in 2017.1</span>
