#Introduction to components


A __GameObject__ contains __components__. (See documentation on [GameObject](GameObjects) for more information.)

Below is an example of how the __GameObject__ and __component__ relationship works using the most common __component__, the __Transform Component__. 

You can see the __Transform Component__ by looking at the __Inspector__ for a new __GameObject__:

* Open any scene in any project in the Unity Editor. (See documentation on [Getting Started](GettingStarted) for guidance on this.)
* Create a new __GameObject__ (menu: __GameObject__ > __Create Empty__).
* The new  __GameObject__ is pre-selected, with the __Inspector__ showing its __Transform Component__, as in the image below. (If it isn't pre-selected, click on it to see its __Inspector__.)


![The Inspector of a new, empty GameObject showing the Transform Component](../uploads/Main/EmptyGO.png) 

Notice that the new, empty __GameObject__ contains a name ("GameObject"), a [Tag](Tags) ("Untagged"), and a [Layer](Layers) ("Default"). It also contains a __Transform Component__. 


The Transform Component
-----------------------

It is impossible to create a __GameObject__ in the Editor without a __Transform Component__. This component defines the __GameObject's__ position, rotation, and scale in the game world and __Scene view__.

The __Transform Component__ also enables a concept called 'parenting' which is a critical part of working with __GameObjects__. To learn more about the __Transform Component__ and parenting, see the [Transform Component Reference page](class-Transform).


Other components
----------------


The __Transform Component__ is critical to all __GameObjects__, so each __GameObject__ has one but __GameObjects__ can contain other __components__ as well.

Every Scene has a __Main Camera__ __GameObject__ by default.  It has several __components__.(You can see see this by selecting it in your open __Scene__ to view its __Inspector__.) 


![The Main Camera is a type of GameObject - it is in each scene by default and has several components by default](../uploads/Main/GameObject-maincamera.png) 

Looking at the __Inspector__ of the __Main Camera__ __GameObject__, you can see that it contains additional __components__. Specifically, a [Camera Component](class-Camera), a [GUILayer](class-GUILayer), a [Flare Layer](class-FlareLayer), and an [Audio Listener](class-AudioListener). All of these __components__ provide functionality to this __GameObject__.

[Rigidbody](RigidbodiesOverview), [Collider](CollidersOverview), [Particle System](PartSysWhatIs), and  [Audio](AudioOverview) are all different __components__  that you can add to a __GameObject__.
