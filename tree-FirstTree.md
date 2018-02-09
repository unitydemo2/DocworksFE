#Building Your First Tree

We'll now walk you through the creation of your first tree with the Tree creation tool.


##Adding a new Tree


To create a new __Tree__ asset, select __GameObject &gt; 3D Object &gt; Tree__. You'll see a new Tree asset is created in your Project View, and instantiated in the currently open Scene. This new tree is very basic with only a single branch, so let's add some character to it.


##Adding Branches

![A brand new tree in your scene](../uploads/Main/TreeCreator-BasicBranch.png) 

Select the tree to view the __Tree__ window in the __Inspector__. This interface provides all the tools for shaping and sculpting your trees. You will see the __Tree Hierarchy__ window with two nodes present: the __Tree Root__ node and a single __Branch Group__ node, which we'll call the trunk of the tree.

In the __Tree Hierarchy__, select the __Branch Group__, which acts as the trunk of the tree. Click on the __Add Branch Group__ button and you'll see a new __Branch Group__ appear connected to the Main Branch. Now you can play with the settings in the __Branch Group Properties__ to see alterations of the branches attached to the tree trunk.


![Adding branches to the tree trunk.](../uploads/Main/TreeCreator-AddingBranches1.png) 

After creating the branches that are attached to the trunk, we can now add smaller twigs to the newly created branches by attaching another __Branch Group__ node. Select the secondary __Branch Group__ and click the __Add Branch Group__ button again. Tweak the values of this group to create more branches that are attached to the secondary branches.


![Adding branches to the secondary branches.](../uploads/Main/TreeCreator-AddingBranches2.png) 

Now the tree's branch structure is in place. Our game doesn't take place in the winter time, so we should also add some __Leaves__ to the different branches, right?


##Adding Leaves

We decorate our tree with leaves by adding __Leaf Groups__, which basically work the same as the Branch groups we've already used. Select your secondary Branch Group node and then click the __Add Leaf Group__ button. If you're really hardcore, you can add another leaf group to the tiniest branches on the tree as well.

![Leaves added to the secondary and smallest branches](../uploads/Main/TreeCreator-AddingLeaves.png) 

Right now the leaves are rendered as opaque planes. This is because we want to adjust the leaves' values (size, position, rotation, etc.) before we add a material to them. Tweak the Leaf values until you find some settings you like.


##Adding Materials

In order to make our tree realistic looking, we need to apply __Materials__ for the branches and the leaves. Create a new Material in your project using __Assets &gt; Create &gt; Material__. Rename it to "My Tree Bark", and choose __Nature &gt; Tree Creator Bark__ from the Shader drop-down. From here you can assign the __Textures__ provided in the Tree Creator Package to the Base, Normalmap, and Gloss properties of the Bark Material. We recommend using the texture "BigTree\_bark\_diffuse" for the Base and Gloss properties, and "BigTree\_bark\_normal" for the Normalmap property.

Now we'll follow the same steps for creating a Leaf Material. Create a new Material and assign the shader as __Nature &gt; Tree Creator Leaves__. Assign the texture slots with the leaf textures from the Tree Creator Package.


![Material for the Leaves](../uploads/Main/TreeCreator-LeavesMaterial.png) 

When both Materials are created, we'll assign them to the different Group Nodes of the Tree. Select your Tree and click any Branch or Leaf node, then expand the __Geometry__ section of the __Branch Group Properties__. You will see a Material assignment slot for the type of node you've selected. Assign the relevant Material you created and view the results.


![Setting the leaves material](../uploads/Main/TreeCreator-AddingMaterialToLeaves.png) 

To finish off the tree, assign your Materials to all the __Branch__ and __Leaf Group__ nodes in the Tree. Now you're ready to put your first tree into a game!


![Tree with materials on leaves and branches.](../uploads/Main/TreeCreator-FinalTree.png) 


##Hints.

* Creating trees is a trial and error process.
* Don't create too many leaves/branches as this can affect the performance of your game.
* Check the [alpha maps](HOWTO-alphamaps) guide for creating custom leaves.
