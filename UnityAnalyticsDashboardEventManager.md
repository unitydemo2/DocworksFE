# Event Manager 
View a list of all the standard and custom events and parameters you have dispatched from your project. Turn off old, unused events to prevent them from appearing in new reports.


![The Event Manager page showing two disabled events](../uploads/Main/UnityAnalyticsDashboardEventManager1.png)


When you disable an event, the Unity Analytics system ignores that event when processing your data. Because disabled events are ignored during data processing, they do not count toward your account event limits. If you re-enable an event, Unity Analytics includes newly dispatched instances of that event in subsequent reports, but any event instances dispatched while the event was disabled remain unprocessed. 
Note that you can download disabled events through [Raw Data Export](UnityAnalyticsRawDataExport). The Event Manager only controls whether events are aggregated with the rest of your Analytics data. 

---
* <span class="page-edit">2017-08-21  <!-- include IncludeTextNewPageYesEdit --></span>
* <span class="page-history">New feature in Unity 2017.1</span>