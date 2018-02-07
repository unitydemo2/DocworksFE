# Preparing Assets for AssetBundles

When using AssetBundles you are free to assign any asset to any bundle you desire. However, there are certain strategies to consider when setting up your bundles. These grouping strategies are meant to be used however you see fit for your specific project. Feel free to mix and match these strategies as you see fit.

## Logical Entity Grouping

Logical Entity Grouping is where assets are assigned to AssetBundles based on the functional portion of the project they represent. This includes sections such as User-Interface, characters, environments, and anything else that may appear frequently throughout the lifetime of the application.

###Examples

* Bundling all the textures and layout data for a User-Interface screen
* Bundling all the models and animations for a character/set of characters
* Bundling the textures and models for pieces of the scenery shared across multiple levels

Logical Entity Grouping is ideal for downloadable content (DLC) for the fact that, with everything separated in this way, you’re able to make a change to a single entity and not require the download of additional, unchanged, assets. 

The biggest trick to being able to properly implement this strategy is that the developer assigning assets to their respective bundles must be familiar with precisely when and where each asset will be used by the project.

## Type Grouping

For this strategy you’ll assign assets that are of similar type, such as audio tracks or language localization files, to a single AssetBundle.

Type grouping is one of the better strategies for building AssetBundles to be used by multiple platforms. For example if your audio compression settings are identical between windows and mac platforms, you can pack all audio data into AssetBundles by themselves and reuse those bundles, whereas shaders tend to get compiled with more platform specific options so a shader bundle you build for mac may not be reused on windows. In addition, this method is great for making your AssetBundles compatible with more unity player versions as textures compression formats and settings change less frequently than something like your code scripts or prefabs.

## Concurrent Content Grouping

Concurrent Content Grouping is the idea that you will bundle assets together that will be loaded and used at the same time. You could think of these types of bundles as being used for a level based game where each level contains totally unique characters, textures, music, etc. You would want to be absolutely certain that an asset in one of these AssetBundles is only used at the same time the rest of the assets in that bundle are going to be used. Having a dependency on a single asset inside a Concurrent Content Grouping bundle would result in significant increased load times. You would be forced to download the entire bundle for that single asset.

The most common use-case for Concurrent Content Grouping bundles is for bundles that are based on scenes. In this assignment strategy, each scene bundle should contain most or all of that scenes dependencies.

Note that a project absolutely can and should mix these strategies as your needs require. Using the optimal asset assignment strategy for any given scenario greatly increases efficiency for any project.

For example, a project may decide to group its User-Interface (UI) elements for different platforms into their own Platform-UI specific bundle but group its interactive content by level/scene.

Regardless of the strategy you follow, here are some additional tips that are good to keep in mind across the board:

* Split frequently updated objects into AssetBundles separate from objects that rarely change
* Group objects that are likely to be loaded simultaneously. Such as a model, its textures, and its animations
* If you notice multiple objects across multiple AssetBundles are dependant on a single asset from a completely different AssetBundle, move the dependency to a separate AssetBundle. If several AssetBundles are referencing the same group of assets in other AssetBundles, it may be worth pulling those dependencies into a shared AssetBundle to reduce duplication.
* If two sets of objects are unlikely to ever be loaded at the same time, such as Standard and High Definition assets, be sure they are in their own AssetBundles.
* Consider splitting apart an AssetBundle if less that 50% of that bundle is ever frequently loaded at the same time
* Consider combining AssetBundles that are small (less that 5 to 10 assets) but whose content is frequently loaded simultaneously
* If a group of objects are simply different versions of the same object, consider AssetBundle Variants

----
* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>