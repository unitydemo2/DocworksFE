Upgrade Unity Analytics 5.1 to 5.2 onwards
==================================

Re-integration of Unity Analytics
---------------------------------

Follow the instructions in [Setting Up Analytics](UnityAnalyticsOverview) which consists of these steps:

1. Confirm your Project IDs match
2. Enable Analytics
3. Play to Validate

You can determine that you successfully completed the upgrade by checking the SDK version in Play to Validate step and confirming the correct Editor version (ie: u5.2 or u5.3) is displayed in Validator. 

![](../uploads/Main/AnalyticsValidate52.png)

Updating Advanced Integration events
------------------------------------
If you did any existing Advanced Integration previously, you will also need to update the namespace and the calls to use the 5.2 and up syntax. Follow [5.2 onwards Advanced Integration instructions](UnityAnalyticsAdvancedSDK) to update.
