Ragdoll Wizard
==============


Unity has a simple wizard that lets you quickly create your own ragdoll. You simply have to drag the different limbs on the respective properties in the wizard. Then select create and Unity will automatically generate all __Colliders__, __Rigidbodies__ and __Joints__ that make up the Ragdoll for you.


Creating the Character
----------------------


Ragdolls make use of __Skinned Meshes__, that is a character mesh rigged up with bones in the 3D modeling application. For this reason, you must build ragdoll characters in a 3D package like Maya or Cinema4D.

When you've created your character and rigged it, save the asset normally in your __Project Folder__. When you switch to Unity, you'll see the character asset file. Select that file and the __Import Settings__ dialog will appear inside the inspector. Make sure that __Mesh Colliders__ is not enabled.


Using the Wizard
----------------


It's not possible to make the actual source asset into a ragdoll. This would require modifying the source asset file, and is therefore impossible. You will make an instance of the character asset into a ragdoll, which can then be saved as a __Prefab__ for re-use.

Create an instance of the character by dragging it from the __Project View__ to the __Hierarchy View__. Expand its __Transform Hierarchy__ by clicking the small arrow to the left of the instance's name in the Hierarchy. Now you are ready to start assigning your ragdoll parts.

Open the Ragdoll Wizard by choosing __GameObject &gt; 3D Object &gt; Ragdoll...__ from the menu bar. You will now see the Wizard itself.


![The Ragdoll Wizard](../uploads/Main/RagdollWizard.png) 

Assigning parts to the wizard should be self-explanatory. Drag the different Transforms of your character instance to the appropriate property on the wizard. This should be especially easy if you created the character asset yourself.

When you are done, click the __Create Button__. Now when you enter __Play Mode__, you will see your character go limp as a ragdoll.

The final step is to save the setup ragdoll as a Prefab. Choose __Assets -&gt; Create -&gt; Prefab__ from the menu bar. You will see a New Prefab appear in the Project View. Rename it to "Ragdoll Prefab". Drag the ragdoll character instance from the Hierarchy on top of the "Ragdoll Prefab". You now have a completely set-up, re-usable ragdoll character to use as much as you like in your game.

Note
----

For Character Joints made with the Ragdoll wizard, take a note that the setup is made such that the joint's Twist axis corresponds with the limb's largest swing axis, the joint's Swing 1 axis corresponds with limb's smaller swing axis and joint's Swing 2 is for twisting the limb. This naming scheme is for legacy reasons.
