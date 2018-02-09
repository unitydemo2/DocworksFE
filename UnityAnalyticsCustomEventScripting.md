Custom Event Scripting
=============

As an alternative to using the [AnalyticsTracker](UnityAnalyticsAnalyticsTracker) component, you can send custom events directly via script by calling [Analytics.CustomEvent](ScriptRef:Analytics.Analytics.CustomEvent). See the following example:


````
// Reference the Unity Analytics namespace
using UnityEngine.Analytics;

//  Use this call for wherever a player triggers a custom event
Analytics.CustomEvent(string customEventName,
IDictionary<string, object> eventData);
````

|**_Analytics.CustomEvent Input Parameters_**|||
|**_Name_** |**_Type_** |**_Description_** |
|:---|:---|
|__customEventName__ |string |Name of custom event. Name cannot include the prefix "unity." --- This is a reserved keyword. |
|__eventData__ |dictionary |Additional parameters sent to Unity Analytics at the time the custom event was triggered. eventData key cannot include the prefix "unity." --- This is a reserved keyword.|

A few considerations with regards to the custom events:

* Be consistent! Maintain consistent data types for each parameter in your event data. For example, don't send a level parameter as a number, then change it to be a string. Doing so can lead to erroneous behavior, making your data difficult to interpret.
    * Boolean (true/false)
    * String (characters)
    * Numbers (int, float, etc.)

* Default limit of 10 parameters per custom event.
    * If there are more parameters passed, the call will fail with a return value of AnalyticsResult.TooManyItems
* Default limit of 500 characters for the dictionary content.  
    * If more than 500 characters are passed, the call will fail with return value of AnalyticsResult.SizeLimitReached
* Default limit of 100 custom events per hour, per user.
    * If more than 100 events per hour are called, the call will fail with return value of AnalyticsResult.TooManyRequests
* Consider how parameters are parsed by the Analytics system.
    * All numbers, ints, floats, etc., even if sent as strings, are parsed as numbers.
    * Only strings and Booleans are considered 'categorizable'.
    * Consequently, if you want something to be summed or averaged, send it as a number (e.g., 51 or '51'). If you want it to be categorized, as you would with a level or option, make sure it will parse as a string (e.g., 'Level51').

In the example below we are interested in knowing what our user had in their inventory at the time the game ended. 


````
// Reference the Collections Generic namespace
  using System.Collections.Generic;

  int totalPotions = 5;
  int totalCoins = 100;
  string weaponID = "Weapon_102";
  Analytics.CustomEvent("gameOver", new Dictionary<string, object>
  {
    { "potions", totalPotions },
    { "coins", totalCoins },
    { "activeWeapon", weaponID }
  });
````

Press Play 
----------
To send test Custom Event data to our servers and validate your integration, trigger your Custom Event during Editor Play mode. 
![](../uploads/Main/AnalyticsPlayGame.gif)

If integration is successful, your test data will display in the table below.


Validate
--------
![](../uploads/Main/AnalyticsValidate.png)

