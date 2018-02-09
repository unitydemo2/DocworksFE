Setting Up Analytics
====================

Once you have [set up your project for Unity Services](SettingUpProjectServices), you can enable the Analytics service.

To do this, in the Services window, select "Analytics" and then click the "Off" button to toggle it **On**. If you haven't already done so, at this stage you will need to complete the mandatory Age Designation field for your project. (Again, you may have already done this for a different Unity Service, such as Ads). This age designation selection will appear in the Services window.

![Enabling Analytics within your project](../uploads/Main/UnityAnalyticsEnable.png) 

You must then hit **Play** in your project to validate the connection to Unity Analytics.

The Unity Editor acts as a test environment to validate your Analytics integration. With Analytics enabled, when you press the Play button, the Editor sends data (an "App Start" event) to the analytics service. This means you can test your analytics without having to build and publish your game.

Once you have pressed play, you can check that your project was validated by going to the Analytics Dashboard for this project. To get there, in the services window, click Services -> Analytics -> Go To Dashboard.

![The "Go To Dashboard" button in the Analytics section of the Services window](../uploads/Main/UnityAnalyticsGoToDashboard.png)

The dashboard opens in a web browser. You'll see three headings under your project's name: Overview, Basic Integration and Advanced Integration. Click **"Basic Integration"**, then directly underneath, click step 3: **"Play to Validate"**. If your project was set up correctly, you should see a table containing an entry showing an "appStart" event, along with the date and time, as well as your current editor platform and version number. 

![The Validate Test Data Table on the Analytics Project Dashboard](../uploads/Main/UnityAnalyticsValidateTestDataTable.png)



