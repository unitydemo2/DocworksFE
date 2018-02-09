#The Fresnel Effect

One important visual cue of objects in the real world has to do with how they become more reflective at grazing angles (illustrated below). This is called the Fresnel effect.

![The fresnel effect visible at grazing angles in relation to the viewer is increasingly apparent as the surface of a material becomes smoother](../uploads/Main/StandardShaderFresnelGraduationTable.png)

There are two things to note in this example; firstly, these reflections only appear around the edges of the sphere (that’s when its surface is at a grazing angle), and also that they become more visible and sharper as the smoothness of the material goes up.

In the Standard shader there is no direct control over the Fresnel effect. Instead it is indirectly controlled through the smoothness of the material. Smooth surfaces will present a stronger Fresnel, totally rough surfaces will have no Fresnel.