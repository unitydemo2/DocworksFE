Parallax Normal mapped Properties
---------------------------------

__Parallax Normal mapped__ is the same as regular __Normal mapped__, but with a better simulation of "depth". The extra depth effect is achieved through the use of a __Height Map__. The Height Map is contained in the alpha channel of the Normal map. In the alpha, black is zero depth and white is full depth. This is most often used in bricks/stones to better display the cracks between them.

The Parallax mapping technique is pretty simple, so it can have artifacts and unusual effects. Specifically, very steep height transitions in the Height Map should be avoided. Adjusting the __Height__ value in the __Inspector__ can also cause the object to become distorted in an odd, unrealistic way. For this reason, it is recommended that you use gradual Height Map transitions or keep the __Height__ slider toward the shallow end.
