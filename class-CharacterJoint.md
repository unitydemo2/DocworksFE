Character Joint
===============


__Character Joints__ are mainly used for Ragdoll effects. They are an extended ball-socket joint which allows you to limit the joint on each axis.

If you just want to set up a ragdoll read about [Ragdoll Wizard](wizard-RagdollWizard).


![](../uploads/Main/Inspector-CharacterJoint.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Connected Body__ |Optional reference to the __Rigidbody__ that the joint is dependent upon. If not set, the joint connects to the world. |
|__Anchor__ |The point in the __GameObject's__ local space where the joint rotates around. |
|__Axis__ |The twist axes. Visualized with the orange gizmo cone. |
|__Auto Configure Connected Anchor__ |If this is enabled, then the Connected Anchor position will be calculated automatically to match the global position of the anchor property. This is the default behavior. If this is disabled, you can configure the position of the connected anchor manually.|
|__Connected Anchor__ |Manual configuration of the connected anchor position. |
|__Swing Axis__ |The swing axis. Visualized with the green gizmo cone. |
|__Low Twist Limit__ |The lower limit of the joint. See below. |
|__High Twist Limit__ |The higher limit of the joint. See below. |
|__Swing 1 Limit__ |Limits the rotation around one element of the defined __Swing Axis__ (visualized with the green axis on the gizmo). See below. |
|__Swing 2 Limit__ |Limits movement around one element of the defined __Swing Axis__. See below. |
|__Break Force__ |The force that needs to be applied for this joint to break. |
|__Break Torque__ |The torque that needs to be applied for this joint to break. |
|__Enable Collision__ |When checked, this enables collisions between bodies connected with a joint. |
|__Enable Preprocessing__ | Disabling preprocessing helps to stabilize impossible-to-fulfil configurations. |

![The Character Joint on a Ragdoll](../uploads/Main/CharacterJointWindow.png) 

Details
-------


Character joints give you a lot of possibilities for constraining motion like with a universal joint.

The twist axis (visualized with the orange access on the gizmo) gives you most control over the limits as you can specify a lower and upper limit in degrees (the limit angle is measured relative to the starting position). A value of -30 in __Low Twist Limit__-&gt;__Limit__ and 60 in __High Twist Limit__-&gt;__Limit__ limits the rotation around the twist axis (orange gizmo) between -30 and 60 degrees.

The __Swing 1 Limit__ limits the rotation around the swing axis (visualized with the green axis on the gizmo). The limit angle is symmetric. Thus a value of 30 will limit the rotation between -30 and 30.

The __Swing 2 Limit__ axis isn't visualized on the gizmo but the axis is orthogonal to the two other axes (that is the twist axis visualised in orange on the gizmo and the __Swing 1 Limit__ visualised in green on the gizmo).
The angle is symmetric, thus a value of 40 will limit the rotation around that axis between -40 and 40 degrees.

For each of the limits the following values can be set:


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Bounciness__ | A value of 0 will not bounce. A value of 1 will bounce without any loss of energy.|
|__Spring__ | The spring force used to keep the two objects together.|
|__Damper__ | The damper force used to dampen the spring force.|
|__Contact Distance__ | Within the contact distance from the limit contacts will persist in order to avoid jitter.|


###Breaking joints

You can use the __Break Force__ and __Break Torque__ properties to set limits for the joint's strength. If these are less than infinity, and a force/torque greater than these limits are applied to the object, its Fixed Joint will be destroyed and will no longer be confined by its restraints.

Hints
-----


* You do not need to assign a __Connected Body__ to your joint for it to work.
* Character Joints require your object to have a Rigidbody attached.
* For Character Joints made with the Ragdoll wizard, take a note that the setup is made such that the joint's Twist axis corresponds with the limb's largest swing axis, the joint's Swing 1 axis corresponds with limb's smaller swing axis and joint's Swing 2 is for twisting the limb. This naming scheme is for legacy reasons.
