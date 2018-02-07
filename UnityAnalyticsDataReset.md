# Data reset

Unity Analytics allows you to permanently clear all data from your Analytics dashboard by performing a data reset. This action **cannot be undone**, so read this documentation and the confirmation message in the Analytics dashboard carefully before carrying out this action. 

This page describes when data reset might be useful, and what impact it has on the data in your Analytics project.

## When to perform a data reset

The main scenario that calls for resetting data in an Analytics project is to wipe data from your dashboard immediately prior to launching (or re-releasing) your game. This ensures that the data you collect after the reset is clean and not mixed with previously collected data, which may skew your analyses.


Other common scenarios:

* Wiping data collected during development and testing prior to launching your game.

* Wiping data from a pre-release or beta version.

* Wiping data prior to launching your game in a store.

* Wiping data prior to a product re-launch.

Please note that performing a data reset is optional - you may never need to use this feature.

## How this impacts your data

Due to Unity Technologies' data processing cycles, all data resets occur at 00:00 UTC the following day. See the Configure page for the exact time (in your timezone) your data is due to be reset.

![](../uploads/Main/AnalyticsDataReset1.png)

Data is collected from the time the reset occurs, but might take up to 4 hours to populate in your dashboard. You cannot specify another date to reset your data on.

Resetting your data affects these Analytics elements as follows:

* **Dashboard:** This is permanently wiped of all visible data, including data in charts.

* **Custom event data:** This is permanently wiped from the dashboard. Note that custom events you have instrumented in your project don’t need to be re-validated.

* **Reports, Funnels, Segments:** All data associated with these configurations (that you have created in your project) is permanently wiped from the dashboard. However, the configurations themselves are not deleted. For example, if you create a three-step funnel, populate it with data, and then perform a data reset, the three-step funnel is still present in your dashboard but is no longer populated with the data.

* **Livestream:** This is not affected by performing a data reset.

* **Raw Data Export:** This is not affected by performing a data reset. You can still perform an export to access historical data, and all previous exports you have run are still present in the Activity table on the Raw Data Export page.

## How to perform a data reset

To perform a data reset, open the Unity Services Dashboard for the Analytics project that you want to reset, go to __Configure__, and click on __Reset Data__. Make sure to read the confirmation message carefully. Type the name of your project into the text box and click __Reset__. The data reset occurs immediately.

![](../uploads/Main/UnityAnalyticsDataReset55.png)

When the data is reset, the following details are provided about the last reset in the __Configure__ page:

* Date and time the reset occurred.

* User who performed the reset.

**Note:** Only Project Owners and Managers can perform this action. Project Users do not have permission to perform a reset.

