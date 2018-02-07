# Unity Analytics Overview

Unity Analytics provides the data you need to manage your relationship with your players. 


![The Unity Analytics Dashboard](../uploads/Main/AnalyticsOverview1.png)

Understand your players; understand why they play your games; understand why they stop playing your games. Make decisions based on data, not guesses.

By simply enabling Unity Analytics in your project, you can get data about how many people first start playing your game, how many play every day, how many play in a given month, and other session-based usage data. If you also use the Unity Ads and IAP Services, your analytics data automatically includes the revenue from these sources. This sort of session data paints a valuable picture of the health of your game. It answers question such as: “Am I getting new players?” “How often and how long do they play?” “Do they play again the next day? The next week? The next month?” “How much revenue am I making per player on a given day?” 

By dispatching Standard Analytics Events when players perform key actions in your game, you can extend the analytics data available so that it reveals what your players are actually doing when they play. Do they make it through your onboarding tutorial? Do they visit your IAP store? Do they progress through your game levels as you expect? 

Analytics data can help you focus on the most fruitful areas to improve your application to better serve your players. You can make these changes by releasing updates, but you can also create __Remote Settings__ that allow you to adapt and tune your game without an update. 

By understanding your players and how they play your games, you can make your games better. And when the data shows that your players are changing, you can react and adapt.

See [Analytics Metrics, Segments, and Terminology](UnityAnalyticsTerminology) for definitions of specific terms used throughout the Analytics documentation.

## Core usage data
When you enable Analytics, Unity tracks core usage metrics on [supported platforms](#SupportedPlatforms) without any effort or implementation on your part. These [core metrics](UnityAnalyticsTerminology) include:

* New installs
* Daily active users (DAU)
* Monthly active users (MAU)
* Total sessions
* Sessions per user
* Time spent in app
* User Segments for Country and Platform

These are all good metrics to use to monitor the health of your game. They tell you how many people are installing your game, how often they play, and how long they stick with it. Many external factors also influence these numbers, but you should watch them for signs of problems that you can correct.

The following chart, displayed on the Overview tab of your [Analytics Dashboard](UnityAnalyticsDashboard) shows three data plots: __New Users__, __DAU__ (Daily Active Users), and __MAU__ (Monthly Active Users):

![DAU, MAU, New Users chart](../uploads/Main/AnalyticsOverview2.png)

The __New Users__ plot shows how many people play your game for the first time on a given day. Since new players won’t have had much, if any, exposure to your game, this chart generally reflects external factors. If you launch a marketing campaign or other promotion to attract new players, you would hope to see a bump in the __New Users__ plot. 

The __DAU__ plot shows how many of your players played on a given day. Similar to the __DAU__ plot, the __MAU__ plot shows how many of your players played in a given 30-day period. 

![Sticky Factor chart](../uploads/Main/AnalyticsOverview3.png)

The __Sticky Factor__ chart plots the percentage of your monthly players who played on a given day (DAU/MAU). The general idea behind this metric is that it shows how often your players return to play day-after-day. (In other words, how likely players are to “stick” with your game.)      

High active player numbers can indicate popularity, but can be tricky to interpret in isolation. In particular, these metrics don’t separate the influence of new versus returning users. For example, an influx of new players could mask the loss of more established players. (The loss of players is called “churn” in common analytics jargon.) __DAU__, __MAU__, and __Sticky Factor__ metrics are often used in the Games industry because DAU and MAU have historically been the most widespread publically-available data with which to compare different games. 

See  [Analytics Dashboard](UnityAnalyticsDashboard) for information on how to view your analytics data. 

## Player behavior data
To learn about game-specific player behavior, you can send analytics events from your game at the appropriate times. Unity provides easy-to-use APIs for sending both standardized and fully-customized events. You can use these events to instrument your games to monitor player behavior, particularly in the following areas:

* Onboarding — are players making it through your onboarding mechanics such as tutorials or starting levels?
* Progression — are players progressing through your levels?
* Economy — are your game economies working out as expected?
* Design validation — are your game design choices working out as you thought they would?
* Application validation — are all areas of your application being utilized as you expect? Are there parts that players ignore or don’t notice?
* Monetization — are your monetization strategies optimal? Are there impediments to players carrying out purchases? 

See [Analytics Events](UnityAnalyticsCustomEvents) for information on gathering player behavior data. 

To help you analyze player behavior, the Analytics Dashboard includes a funnel builder. A funnel is a display that shows how your players progress through a linear sequence of steps. For example, you could create a funnel for a tutorial that showed what percentage of your users made it through the tutorial steps. Funnels are useful for identifying places in your application where you lose players. 


![Level progression funnel](../uploads/Main/AnalyticsOverview4.png)

This example funnel shows player progression through a hypothetical game. Each step in the funnel represents the completion of a game level. While you can always expect some drop off from level to level, too large a drop after a given level could indicate a problem on that level. The funnel won’t tell you the cause -- it could be a game play problem, a bug, or the level might be too difficult -- but the funnel does indicate a worthwhile area for investigation.

See [Funnels](UnityAnalyticsFunnels) for information on implementing funnels.

## Revenue data
You can analyze in-app purchase (IAP) revenue along with your other analytics data. If you use the Unity IAP Service, the revenue data is available automatically. Otherwise, you can send an event to the Analytics Service whenever a player makes a purchase. If you use the Unity Ads Service, you can also analyze the resulting revenue on the Analytics Dashboard. (There isn’t any way to report outside ad revenue to the Analytics Service, though.)  

The following charts, displayed on the Overview tab of your Analytics Dashboard, show the daily revenue numbers for your project:

![LABEL](../uploads/Main/AnalyticsOverview5.png)

The first chart shows verified in-app purchase revenue and transactions and advertising revenue from the Unity Ads Service. The charts on the __Overview__ tab only show verified IAP revenue, but you can view all reported revenue in the __Data Explorer__. Unverified revenue sources include test transactions, fraudulent transactions, transactions from platforms that do not support receipt verification (like Amazon and the Windows store), and transactions reported using missing or incorrect information or without configuring the required store API keys. When you use the Unity IAP Service, IAP transactions are automatically reported and verified. When you use an external IAP API, you can report and verify IAP revenue through the [Unity Analytics API](UnityAnalyticsReceiptVerification).

The second chart shows the daily averages of revenue per paying user and per active user:

![LABEL](../uploads/Main/AnalyticsOverview6.png)

__Average Revenue Per Paying User__ (ARPPU) shows the average amount spent by those players who make IAP transactions on a given day. The __Average Revenue Per Daily Active User__ (ARPDAU) shows the average revenue from all users and includes both IAP revenue and advertising revenue on a given day. 

The overview charts show revenue for all users. To better understand how different groups of players monetize, use the [Data Explorer](UnityAnalyticsDataExplorer) to view revenue by segment. The standard segments include lifecycle cohort, geography, monetization category, demographics (when reported), and platform. You can also define your own segments.

The Data Explorer page of the Dashboard provides several additional monetization metrics and segments:

**Monetization Metrics**:

* ARPDAU (Average Revenue Per Daily Active User)
* ARPPU (Average revenue Per Paying User)
* Number of Unverified Transactions
* Number of Verified Transactions
* Total IAP Revenue
* Total Verified Revenue
* Unverified IAP Revenue
* Verified IAP Revenue
* Verified Paying Users

**Ad Metrics**:

* Ad ARPU (Average Revenue Per User)
* Ad Revenue
* Ad Starts
* Ads per DAU
* eCPM (estimated Cost Per Thousand Impressions)

**Monetization Segments**:

* Whales
* Dolphins
* Minnows
* Never Monetized
* All Spenders
 
See [Monetization](UnityAnalyticsMonetization) for more information about revenue analytics.
## Demographics data

One type of metric that Unity does not track is demographics for age or gender. However, the Analytics API does provide a mechanism for you to report age and gender. To use this type of information to study user behavior, your application must collect and report it. You can gather demographics by asking players for the information directly. Or, in some cases, you can use a third party API to obtain the information. For example, Facebook and Android have APIs that report the user’s self-selected gender.

When you collect and report age or gender information, you can view your Analytics data segmented by these facets. Thus, you can better understand how age or gender influences a player’s experience in your game.

See [User Attributes](UnityAnalyticsUserAttributes) for more information on reporting demographics data.
## Data segmentation
Segments help you better understand player behavior. The standard, predefined segments group players by the following categories:

* **Lifecycle** -- group players by the number of days since install. Lifecycle cohorts are useful for analyzing how player behavior changes with more experience in your application.
* **Geography** -- group players by country.
* **Monetization** -- group players by spending category. Monetization categories help you understand the behavior of players by how much revenue they generate.
* **Demographics** -- group by age and gender. Note that demographics information must be reported to the **Unity Analytics** Service by your application; it is not collected automatically.
* **Platform** -- group by the player’s computer OS or device type.

![The MAU metric segmented by lifecycle cohorts](../uploads/Main/AnalyticsOverview7.png)
 
You can use the __Segment Builder__ to define your own categories. However, you can only use any new categories that you make on data collected after those categories are created. For example, if you add a segment for players from Gibraltar, the segment is initially empty; only new activity from players in Gibraltar will show up in the segment.  

You can use segments in the [Data Explorer](UnityAnalyticsDataExplorer) and [Funnel](UnityAnalyticsFunnels) reports.  

For more information about creating your own segments, see [Segment Builder](UnityAnalyticsSegmentBuilder).

## Remote Settings
The __Remote Settings__ feature allows you to change the values of variables in your games from your Analytics Dashboard. You can create any number of __Remote Settings__ while developing your game and assign them to GameObject variables in the Editor. After launching your game, you can change the values of these variables at any time, allowing you to adapt game behavior without releasing an update. 

You can use __Remote Settings__ for tasks such as:

* Adjusting game-play tuning variables
* Enabling or disabling features
* Changing graphical themes

See [Remote Settings](UnityAnalyticsDashboardRemoteSettings) for more information.
## Heatmaps
Heatmaps visualize Analytics events spatially in your game.


![A heatmap displays Analytics events in the Unity Editor where they occurred in a scene](../uploads/Main/AnalyticsOverview8.png)



Use heatmaps while playtesting your game to identify performance and gameplay bottlenecks. Because they require a high volume of Analytics events, using heatmaps after your game has shipped and is in production is not supported.

See BitBucket documentation on [Heatmaps](https://bitbucket.org/Unity-Technologies/heatmaps/wiki/v2.md) for more information.

Heatmaps require __Raw Data Export__, which is only available with a Unity Pro subscription.

## Accessing your raw data
When the reports available on the Analytics Dashboard don’t support the type of analysis you want to perform, you can export your analytics events using __Raw Data Export__. You can export data from the Analytics Dashboard or using the Raw Data Export REST API in either JSON or tab-separated-value format. From there, you can import the data into a database or analysis tool.

__Raw Data Export__ requires a Unity-Pro subscription. See [Raw Data Export](UnityAnalyticsRawDataExport) for more information.

<a name="SupportedPlatforms"></a>
## Supported platforms

The Unity Analytics Service supports the following platforms:

* iOS
* Android
* Tizen
* Windows Phone 8.1
* Windows Store 8.1 (Desktop)
* Windows Store 10.0 (Desktop)
* Mac, PC, Linux Standalone
* WebGL - 5.3 integration and onwards

---
* <span class="page-edit">2017-08-29  <!-- include IncludeTextNewPageYesEdit --></span>
<span class="page-history">New feature in Unity 2017.1</span>

