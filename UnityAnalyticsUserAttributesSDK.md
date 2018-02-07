User Attributes
===============

Unity Analytics offers the ability to track user demographics. This provides you with robust ways to filter your data to look at different user segments. This information is pulled from player information entered at signup or from third-party SDKs.

````
// Reference the Unity Analytics SDK package
  using UnityEngine.Cloud.Analytics;

  // Use this call to designate the user gender
  UnityAnalytics.SetUserGender(Gender gender);

  // Use this call to designate the user birth year
  UnityAnalytics.SetUserBirthYear(int birthYear);
````

|**_Input Parameters_**|||
|**_Name_** |**_Type_** |**_Description_** |
|:---|:---|
|__gender__ |enum |Gender of user can be Gender.Female, Gender.Male or Gender.Unknown. |
|__birthYear__ |int |Birth year of user. Must be 4-digit year format only. |


For example:

````
  Gender gender = Gender.Female;
  UnityAnalytics.SetUserGender(gender);

  int birthYear = 2014;
  UnityAnalytics.SetUserBirthYear(birthYear);
````

Press Play 
----------
To send test User Attribute data to our servers and validate your integration, trigger your User Attribute during Editor Play mode. If integration is successful, your test data will display in the table below.

![](../uploads/Main/AnalyticsPlayGame.gif)

Validate
--------
![](../uploads/Main/AnalyticsValidate.png)
