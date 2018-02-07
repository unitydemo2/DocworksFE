# Graph Visualizer

The Graph Visualizer is a tool that makes a diagram of any trees you make using [Playables](Playables). You can clone or download the Graph Visualizer from the [Unity Bitbucket repository](https://bitbucket.org/Unity-Technologies/playablegraphvisualizer).

### Usage
Add the Graph Visualizer files to your project, following the same folder structure as in the sample project provided with the Unity Bitbucket Graph Vizualizer download.

In the MonoBehaviour which creates the Playable graph, call `GraphVisualizerClient.Show(myPlayable, myTitle)` in your `Update` method. This renders the Playable graph in the __Graph Vis__ window. Open the __Graph Vis__ window by selecting __Graph Visualizer__ from the Window menu. 

**Note**: The Graph Visualizer shows a snapshot of the current status. You need to call `Show(`) on every update if your graph is dynamic or if blending weights change. 


Here's an example of the output:

![The Playables Graph Visualizer](../uploads/Main/PlayablesGraphVisualizer.png)

* Playables in the graph are represented by colored nodes, varying according to their type. 

* Wire color intensity indicates the blending weight. 


###Customizing the Graph Visualizer

You may implement your own `Drawer` to represent your custom Playables, as shown in `AnimationClipPlayableDrawer.cs`. 
 
 