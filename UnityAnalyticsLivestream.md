# Livestream page
Visualize your data in real time at critical moments like game launch and during promotions.

The Livestream page samples your Analytics data as it happens without any other data processing. Note that other areas of the Analytics Dashboard do not show data until processing is complete, introducing a delay of a few hours. Livestream requires a Unity Plus or Pro subscription.

The Livestream page has these sections:

* Live Metrics
* Activity Map
* Top Custo Events

## Live Metrics

![Live Metrics](../uploads/Main/UnityAnalyticsLivestream1.png)


The __Live Metrics__ section shows charts of incoming metrics data. The numbers in the display show the current day’s cumulative totals (reset at midnight GMT). The chart portions show activity over the last 5 minutes, starting when you load the Livestream page.

|:---|:---|
|__User Logins__| The number of players who have started a new session.|
|__New Users__ | The number of new players. |
|__Pre-Verified Revenue__ | Reported IAP revenue (before [receipt verification](UnityAnalyticsReceiptVerification) is performed). |

## Activity Map

![Activity Map](../uploads/Main/UnityAnalyticsLivestream2.png)

The __Activity Map__ marks the geographic locations of incoming Analytics API requests with temporary markers.

## Top Custom Events

![Top Custom Events](../uploads/Main/UnityAnalyticsLivestream3.png)

The __Top Custom Events__ section shows the most common __Standard__ and __Custom Events__ dispatched while players use your game. The event counts are cumulative since you loaded the Livestream page. 

Note that the events shown on the Livestream page are sampled for efficiency. This means that not every event is individually counted and, if you open Livestream in two different pages, the numbers and events shown can be slightly different. 

---
* <span class="page-edit">2017-08-29  <!-- include IncludeTextNewPageSomeEdit --></span>
* <span class="page-history">New feature in Unity 2017.1</span>