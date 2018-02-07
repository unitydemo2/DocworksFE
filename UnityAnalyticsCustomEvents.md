Custom Events
=============

Custom events can be any specific in-game action your user performs. They allow you to track player behavior Unity Analytics does not track automatically, such as level achievement, scene change, entering a store, or interacting with game objects. Each custom event can have its own parameters. Setting parameters on your event allows you to filter data collected at the time the event occurred. Visualization tools for Custom Events can be viewed in the Analytics Dashboard, including Data Explorer, Funnel Analyzer, and Segment Builder.

There are two ways to send custom events to the Unity Analytics server:

- Using the [AnalyticsTracker](UnityAnalyticsAnalyticsTracker) component on a GameObject
- Calling the [Analytics.CustomEvent](UnityAnalyticsCustomEventScripting) function from a script


 

