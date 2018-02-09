Animation Blend Shapes
======================

Preparing the Artwork
---------------------

Once you have your Blend Shapes setup in Maya:

* Export your selection to fbx ensuring the animation box is checked and blend Shapes under deformed models is checked.

* Import your fbx file into Unity (assets->import new assets->[name of file].fbx).

* Drag the asset into the hierarchy window. If you select your object in the hierarchy and look in the inspector, you will see your Blend Shapes are listed under the SkinnedMeshRenderer component. Here you can adjust the influence of the blend shape to the default shape, 0 means the blend shape has no influence and 100 means the blend shape has full influence.

Create Animations In Unity
--------------------------

It is also possible to use the Animation window in Unity to create a blend animation, here are the steps:

* Open the Animation window under Window->Animation.

* On the left of the window click ‘Add Curve’ and add a Blend Shape which will be under Skinned Mesh Renderer.

From here you can manipulate the keyframes and Blend Weights to create the required animation.

Once you are finished editing your animation you can click play in the editor window or the animation window to preview your animation.

Scripting Access
----------------

It’s also possible to set the blend weights through code using functions like GetBlendShapeWeight and SetBlendShapeWeight.

You can also check how many blend shapes a Mesh has on it by accessing the blendShapeCount variable along with other useful functions.

Here is an example of code which blends a default shape into two other Blend Shapes over time when attached to a gameobject that has 3 or more blend shapes:

````
//Using C#
 
using UnityEngine;
using System.Collections;
 
public class BlendShapeExample : MonoBehaviour
{
 
       int blendShapeCount;
       SkinnedMeshRenderer skinnedMeshRenderer;
       Mesh skinnedMesh;
       float blendOne = 0f;
       float blendTwo = 0f;
       float blendSpeed = 1f;
       bool blendOneFinished = false;
 
       void Awake ()
       {
          skinnedMeshRenderer = GetComponent<SkinnedMeshRenderer> ();
          skinnedMesh = GetComponent<SkinnedMeshRenderer> ().sharedMesh;
       }
 
       void Start ()
       {
          blendShapeCount = skinnedMesh.blendShapeCount; 
       }
 
       void Update ()
       {
          if (blendShapeCount > 2) {
 
                 if (blendOne < 100f) {
                    skinnedMeshRenderer.SetBlendShapeWeight (0, blendOne);
                    blendOne += blendSpeed;
                 } else {
                    blendOneFinished = true;
                 }
 
                 if (blendOneFinished == true && blendTwo < 100f) {
                    skinnedMeshRenderer.SetBlendShapeWeight (1, blendTwo);
                    blendTwo += blendSpeed;
                 }
 
          }
       }
}
````

