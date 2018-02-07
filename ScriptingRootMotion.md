Tutorial: Scripting Root Motion for "in-place" humanoid animations
==================================================================


Sometimes your animation comes as "in-place", which means if you put it in a scene, it will not move the character that it's on. In other words, the animation does not contain "root motion". For this, we can modify root motion from script. To put everything together follow the steps below (note there are many variations of achieving the same result, this is just one recipe). 


* Open the inspector for the FBX file that contains the in-place animation, and go to the __Animation__ tab
* Make sure the __Muscle Definition__ is set to the Avatar you intend to control (let's say this avatar is called _Dude_, and it has already been added to the __Hierarchy View__).
* Select the animation clip from the available clips
* Make sure __Loop Pose__ is properly aligned (the light next to it is green), and that the checkbox for __Loop Pose__ is clicked


![](../uploads/Main/MecanimRootMotionChristmasTree.png) 


* Preview the animation in the animation viewer to make sure the beginning and the end of the animation align smoothly, and that the character is moving "in-place"
* On the animation clip [create a curve](animeditor-AnimationCurves) that will control the speed of the character (you can add a curve from the __Animation Import inspector__ __Curves-&gt; +__)
* Name that curve something meaningful, like "Runspeed"


![](../uploads/Main/MecanimRootMotionCurve.png) 


* Create a new __Animator Controller__, (let's call it __RootMotionController__)
* Drop the desired animation clip into it, this should create a state with the name of the animation (say __Run__)
* Add a parameter to the Controller with the same name as the curve (in this case, "Runspeed")


![](../uploads/Main/MecanimRootMotionController.png) 


* Select the character __Dude__ in the __Hierarchy__, whose inspector should already have an __Animator__ component.
* Drag __RootMotionController__ onto the __Controller__ property of the Animator
* If you press play now, you should see the "Dude" running in place

Finally, to control the motion, we will need to create a script (RootMotionScript.cs), that implements the [OnAnimatorMove](ScriptRef:MonoBehaviour.OnAnimatorMove.html) callback:-




````
using UnityEngine;
using System.Collections;

[RequireComponent(typeof(Animator))]
	
public class RootMotionScript : MonoBehaviour {
			
	void OnAnimatorMove()
	{
            Animator animator = GetComponent<Animator>(); 
                              
            if (animator)
            {
	 Vector3 newPosition = transform.position;
               newPosition.z += animator.GetFloat("Runspeed") * Time.deltaTime; 
	 transform.position = newPosition;
            }
	}
}


````


You should attach RootMotionScript.cs to the "Dude" object. When you do this, the Animator component will detect that the script has an [OnAnimatorMove](ScriptRef:MonoBehaviour.OnAnimatorMove.html) function and show the __Apply Root Motion__ property as _Handled by Script_


![](../uploads/Main/MecanimRootMotionDude.png) 

