How do I fix the rotation of an imported model?
===============================================


Some 3D art packages export their models so that the z-axis faces upward. Most of the standard scripts in Unity assume that the y-axis represents __up__ in your 3D world. It is usually easier to fix the rotation in Unity than to modify the scripts to make things fit.


![Your model with z-axis points upwards](../uploads/Main/wrong_rotation.png) 

If at all possible it is recommended that you fix the model in your 3D modelling application to have the y-axis face upwards before exporting.

If this is not possible, you can fix it in Unity by adding an extra parent transform:


1. Create an empty __GameObject__ using the __GameObject-&gt;Create Empty__ menu
1. Position the new GameObject so that it is at the center of your mesh or whichever point you want your object to rotate around.
1. Drag the mesh onto the empty GameObject

You have now made your mesh a __Child__ of an empty GameObject with the correct orientation. Whenever writing scripts that make use of the y-axis as up, attach them to the __Parent__ empty GameObject.


![The model with an extra empty transform](../uploads/Main/fixed_rotation.png) 
