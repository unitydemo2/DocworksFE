#WheelCollider Tutorial
 
The new WheelCollider is powered by the PhysX3 Vehicles SDK that is basically a completely new vehicle simulation library when compared to PhysX2. 

Let's go through the process of creating a basic functioning car in Unity 5.0.

- Start by selecting GameObject -&gt; 3D Object -&gt; Plane. This is the ground the car is going to drive on. Make sure the ground has zero transform (Transform -&gt; Reset) for simplicity. Scale it by putting something like 100 in Transform scale components.

- Create a basic car skeleton:

    1. First, add a GameObject as the car root object: GameObject -> Create Empty. Change the name to `car_root`.
    
    1. Add a Physics 3D Rigidbody component to `car_root`. The default mass of 1 kg is way too light for the default suspension settings. Change it to 1500 kg.
    
    1. Now create the car body collider: GameObject -&gt; 3D Object -&gt; Cube. Parent the box under `car_root`. Reset the transform to make it perfectly aligned in local space. Since our car is going to be oriented along the Z axis, scale the box along the Z axis by setting z scaling to 3.
    
    1. Add the wheels root. Select `car_root` and GameObject -&gt; Create Empty Child. Change the name to `wheels`. Reset the transform on it. This node is not mandatory, but it is for tuning convenience later. 

    1. Create the first wheel: select the `wheels` object, GameObject -&gt; Create Empty Child, and name it `frontLeft`. Reset the transform on it. Set the position to  (-1, 0, 1). Add Physics component -&gt; wheel collider to the wheel.
    
    1. Duplicate the `frontLeft` object (Cmd-D or Control-D). Change the x position to 1. Change the name to `frontRight`.
    
    1. Select both the `frontLeft` and `frontRight` objects. Duplicate them. Change the z position of both objects to -1. Change the names to `rearLeft` and `rearRight` respectively.
    
    1. Finally, select the `car_root` object and using the transform manipulators, raise it slightly above the ground.

- Now you should be able to see something like this:

     ![](../uploads/Main/WheelColliderTutorial.png) 
     
- To make this car actually drivable we need to write a controller for it. Let's dive into some scripting:

````
	using UnityEngine;
	using System.Collections;
	using System.Collections.Generic;
	
	public class SimpleCarController : MonoBehaviour {
		public List<AxleInfo> axleInfos; // the information about each individual axle
		public float maxMotorTorque; // maximum torque the motor can apply to wheel
		public float maxSteeringAngle; // maximum steer angle the wheel can have
		
		public void FixedUpdate()
		{
			float motor = maxMotorTorque * Input.GetAxis("Vertical");
			float steering = maxSteeringAngle * Input.GetAxis("Horizontal");
			
			foreach (AxleInfo axleInfo in axleInfos) {
				if (axleInfo.steering) {
					axleInfo.leftWheel.steerAngle = steering;
					axleInfo.rightWheel.steerAngle = steering;
				}
				if (axleInfo.motor) {
					axleInfo.leftWheel.motorTorque = motor;
					axleInfo.rightWheel.motorTorque = motor;
				}
			}
		}
	}
	
	[System.Serializable]
	public class AxleInfo {
		public WheelCollider leftWheel;
		public WheelCollider rightWheel;
		public bool motor; // is this wheel attached to motor?
		public bool steering; // does this wheel apply steer angle?
	}
````

    Just drop this snippet on the `car_root` object, tune the script parameters as shown below and kick off to play mode. Play around with the settings, Those shown below seem to work reasonably well:

    ![](../uploads/Main/WheelColliderSettings.png) 

    You can have up to 20 wheels on a single vehicle instance with each of them applying steering, motor or braking torque.

- Now we will move on to visual wheels. As can see, WheelCollider doesn't apply the simulated wheel position and rotation back to WheelCollider's transform. So adding visual wheel requires some tricks. 

    1. We need some wheel geometry here. we can make a simple wheel shape out of a cylinder. 

    1. Now there could be several approaches to adding visual wheels: making it so that we have to assign visual wheels manually in script properties or writing some logic to find the corresponding visual wheel automatically. We'll follow the second approach.

    1. Attach the visual wheels to wheel collider objects.

    1. Now change the controller script:

````
	using UnityEngine;
	using System.Collections;
	using System.Collections.Generic;

	[System.Serializable]
	public class AxleInfo {
		public WheelCollider leftWheel;
		public WheelCollider rightWheel;
		public bool motor;
		public bool steering;
	}
	 
	public class SimpleCarController : MonoBehaviour {
		public List<AxleInfo> axleInfos; 
		public float maxMotorTorque;
		public float maxSteeringAngle;
	 
		// finds the corresponding visual wheel
		// correctly applies the transform
		public void ApplyLocalPositionToVisuals(WheelCollider collider)
		{
			if (collider.transform.childCount == 0) {
				return;
			}
	 
			Transform visualWheel = collider.transform.GetChild(0);
	 
			Vector3 position;
			Quaternion rotation;
			collider.GetWorldPose(out position, out rotation);
	 
			visualWheel.transform.position = position;
			visualWheel.transform.rotation = rotation;
		}
	 
		public void FixedUpdate()
		{
			float motor = maxMotorTorque * Input.GetAxis("Vertical");
			float steering = maxSteeringAngle * Input.GetAxis("Horizontal");
	 
			foreach (AxleInfo axleInfo in axleInfos) {
				if (axleInfo.steering) {
					axleInfo.leftWheel.steerAngle = steering;
					axleInfo.rightWheel.steerAngle = steering;
				}
				if (axleInfo.motor) {
					axleInfo.leftWheel.motorTorque = motor;
					axleInfo.rightWheel.motorTorque = motor;
				}
				ApplyLocalPositionToVisuals(axleInfo.leftWheel);
				ApplyLocalPositionToVisuals(axleInfo.rightWheel);
			}
		}
	}
````

- One important parameter of WheelCollider component is forceAppPointDistance. This is the distance from the base of the resting wheel to the point where the wheel forces are applied at. The default value is 0, which means to apply the forces at the base of the resting wheel, but actually, it is wise to have this point located somewhere slightly below the car's centre of mass. 
