#Creating a NavMesh Agent

Once you have a NavMesh baked for your level it is time to create a character which can navigate the scene. We're going to build our prototype agent from a cylinder and set it in motion. This is done using a NavMesh Agent component and a simple script.

![](../uploads/Main/NavMeshAgentSetup.svg)

First let's create the character:

1. Create a **cylinder**: __GameObject &gt; 3D Object &gt; Cylinder__.
2. The default cylinder dimensions (height 2 and radius 0.5) are good for a humanoid shaped agent, so we will leave them as they are.
3. Add a **NavMesh Agent** component: __Component &gt; Navigation &gt; NavMesh Agent__.

Now you have simple NavMesh Agent set up ready to receive commands!

When you start to experiment with a NavMesh Agent, you most likely are going to adjust its dimensions for your character size and speed.

The __NavMesh Agent__ component handles both the pathfinding and the movement control of a character. In your scripts, navigation can be as simple as setting the desired destination point - the NavMesh Agent can handle everything from there on.

````
	// MoveTo.cs
	using UnityEngine;
	using System.Collections;
	
	public class MoveTo : MonoBehaviour {
	   
	   public Transform goal;
	   
	   void Start () {
		  NavMeshAgent agent = GetComponent<NavMeshAgent>();
		  agent.destination = goal.position; 
	   }
	}
````

Next we need to build a simple script which allows you to send your character to the destination specified by another Game Object, and a Sphere which will be the destination to move to:

1. Create a new **C# script** (``MoveTo.cs``) and replace its contents with the above script.
2. Assign the MoveTo script to the character you've just created.
3. Create a **sphere**, this will be the destination the agent will move to.
4. Move the sphere away from the character to a location that is close to the NavMesh surface.
5. Select the character, locate the MoveTo script, and assign the Sphere to the **Goal** property.
6. **Press Play**; you should see the agent navigating to the location of the sphere.

To sum it up, in your script, you will need to get a reference to the NavMesh Agent component and then to set the agent in motion, you just need to assign a position to its [destination](ScriptRef:AI.NavMeshAgent-destination.html) property. The [Navigation How Tos](nav-HowTos) will give you further examples on how to solve common gameplay scenarios with the NavMesh Agent.


###Further Reading

- [Navigation HowTos](nav-HowTos) - common use cases for NavMesh Agent, with source code.
- [Inner Workings of the Navigation System](nav-InnerWorkings) - learn more about path following.
- [NavMesh Agent component reference](class-NavMeshAgent) – full description of all the NavMeshAgent properties.
- [NavMesh Agent scripting reference](ScriptRef:AI.NavMeshAgent.html) - full description of the NavMeshAgent scripting API.
