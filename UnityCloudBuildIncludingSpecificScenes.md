# Including specific Scenes

By default, Unity Cloud Build builds the Scenes you've added to your project in the Unity Editor to __File__ > __Build Settings__ > __Scenes in Build__. Click __Add Open Scenes__ to add additional Scenes. See documentation on [Publishing builds](PublishingBuilds) for more information.

To instruct Unity Cloud Build to ignore the __Scenes in Build__ list in the Unity Editor and build a different list of Scenes, you need to provide a __Scene List__ via the [Unity Developer website](https://developer.cloud.unity3d.com).

On the Unity Developer website, go to the build target’s __Advanced Options__. (See documentation on accessing and editing [Advanced Options](UnityCloudBuildAdvancedOptions).)



![The Edit Advanced Options screen](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptionsEdit.png)

Add the list of Scenes you want to include to the __Scene List__. Provide the file path as a relative path from the __Assets__ directory to each Scene file you wish to include.

This is useful for development. For example, you may have one build target that includes all the Scenes, but takes a long time to build. If you’re only working on one Scene, you might find it helpful to create another build target that only includes that Scene. This should build much faster, and allow for more rapid iteration of development versions.
