#Playable API

The Unity Scripting API [Playable](ScriptRef:Experimental.Director.Playable.html) feature provides a way to create tools, effects or other gameplay mechanisms through scripting. It does this by organizing and evaluating data sources in scripts in a conceptual tree-like structure known as the `PlayableGraph`. 

Use the `PlayableGraph` to mix, blend, and modify multiple data sources and play them through a single output. The Playable feature supports animation graphs, providing the capacity to interact with [the animation system](AnimationSection) via scripting. 

The Playable API is limited use with animation and script (`AnimationPlayable` and `ScriptPlayable`).


## The PlayableGraph

The `PlayableGraph` is responsible for the life cycle of Playables. Use it for their creation, destruction and connection.

The `PlayableGraph` defines a set of `PlayableOutputs` that are bound to a [GameObject](gameobjects) or [component](Components). For example, an `AnimationOutput` is bound to to an Animator component.

![The PlayableGraph](../uploads/Main/Playables-0.png)

When working with the PlayableGraph, use [PlayableHandles](ScriptRef:Experimental.Director.PlayableHandle.html). These are C# structs which do not allocate garbage collection memory (see documentation on [Understanding Automatic Memory Management](UnderstandingAutomaticMemoryManagement)). `PlayableHandles` are used for all topological operations on the PlayableGraph, such as connection, disconnection and creation. 

To get the Playable object from the `PlayableHandle`, use the `PlayableHandle.GetObject<>` function, which returns the `PlayableHandle` of the Playable.

Destroying the `PlayableGraph` automatically destroys all Playables and `PlayableOutputs` that were created by the graph. You must call `PlayableGraph.Destroy()` manually, or Unity generates an error message.

## PlayableGraph Visualizer

The  [PlayableGraph Visualizer](https://github.com/UnityTech/graph-visualizer) is a tool that visualizes trees made using the Playables API. 

To use the PlayableGraph Visualizer:

1. Download the PlayableGraph Visualizer corresponding to your Unity version from the [GitHub repository](https://github.com/UnityTech/graph-visualizer).

2. To open the tool, select __Window__ > __PlayableGraph Visualizer__.

![The PlayableGraph Visualizer’s output](../uploads/Main/Playables-1.png)

Playables in the graph are represented by colored nodes. Wire color intensity indicates the weight of the blending. 

__Note:__ See [PlayableGraph Visualizer documentation on GitHub](https://github.com/UnityTech/graph-visualizer) for more information.



## PlayableGraph Example Scripts

**Playing a single clip on a GameObject**

The following [MonoBehaviour](ScriptingRef:MonoBehaviour.html) code example creates a simple data tree structure with a single node, which plays a single clip. 

The example includes an `AnimationClipPlayable`. This is derived from the generic `AnimationPlayable`, and wraps an `AnimationClip` in order to make it compatible with the Playable API.

````
using UnityEngine;
using UnityEngine.Playables;

[RequireComponent (typeof (Animator))]
public class PlayAnimation : MonoBehaviour
{
    public AnimationClip clip;
    PlayableGraph playableGraph;
    void Start () 
    {
        playableGraph = PlayableGraph.CreateGraph();
        var playableOutput = playableGraph.CreateAnimationOutput("Animation", GetComponent<Animator>());
        // Wrap the clip in a playable
        var clipPlayable = playableGraph.CreateAnimationClipPlayable(clip);
        // Connect the Playable to an output
        playableOutput.sourcePlayable = clipPlayable;
        // Plays the Graph.
        playableGraph.Play();
    }
    void OnDisable()
    {
        // Destroys all Playables and Outputs created by the graph.
        playableGraph.Destroy();
    }
}

````

You can also use `AnimationPlayableUtilities` to simplify the creation and playback of AnimationPlayables, as seen in the example below.

````
using UnityEngine;
using UnityEngine.Playables;

[RequireComponent (typeof (Animator))]
public class PlayAnimation : MonoBehaviour
{
    public AnimationClip clip;
    PlayableGraph playableGraph;
    void Start () 
    {
        AnimationPlayableUtilities.PlayClip(GetComponent<Animator>(), clip, out playableGraph);
    }
    void OnDisable()
    {
        // Destroys all Playables and Outputs created by the graph.
        playableGraph.Destroy();
    }
}
````

**Creating an animation blend tree through scripting**

The `AnimationMixerPlayable` can blend two or more `AnimationClipPlayables`, or blend other mixers which themselves blend other clips. 

The weight of each clip in the blend is adjusted dynamically via `SetInputWeight()`.


````
using UnityEngine;
using UnityEngine.Playables;

[RequireComponent (typeof (Animator))]
public class MixAnimation : MonoBehaviour
{
    public AnimationClip clip1;
    public AnimationClip clip2;
    public float weight;
    private PlayableGraph playableGraph;
    private PlayableHandle mixer;
    void Start () 
    {
        // Creates the graph, the mixer and binds them to the Animator.
        mixer = AnimationPlayableUtilities.PlayMixer(GetComponent<Animator>(), 2, out playableGraph);
        // Creates AnimationClipPlayable and connects them to the mixer.
        playableGraph.Connect(playableGraph.CreateAnimationClipPlayable(clip1), 0, mixer, 0);
        playableGraph.Connect(playableGraph.CreateAnimationClipPlayable(clip2), 0, mixer, 1);
    }
    void Update()
    {
        weight = Mathf.Clamp01(weight);
        mixer.SetInputWeight(0, 1.0f-weight);
        mixer.SetInputWeight(1, weight);
    }
    void OnDisable()
    {
        // Destroys all Playables and Outputs created by the graph.
        playableGraph.Destroy();
    }
}
````

**Blending AnimatorController**

Like the `AnimationClipPlayable`, above, the `AnimatorControllerPlayable` wraps `AnimatorControllers`, allowing them to be blended with other `AnimationPlayable`s. 

````
using UnityEngine;
using UnityEngine.Playables;

[RequireComponent (typeof (Animator))]
public class MixController : MonoBehaviour
{
    public AnimationClip clip1;
    public RuntimeAnimatorController controller;
    public float weight;
    private PlayableGraph playableGraph;
    private PlayableHandle mixer;
    void Start () 
    {
        // Creates the graph, the mixer and binds them to the Animator.
        mixer = AnimationPlayableUtilities.PlayMixer(GetComponent<Animator>(), 2, out playableGraph);
        // Creates and connects the Playbles to the mixer.
        playableGraph.Connect(playableGraph.CreateAnimationClipPlayable(clip1), 0, mixer, 0);
        playableGraph.Connect(playableGraph.CreateAnimatorControllerPlayable(controller), 0, mixer, 1);
    }
    void Update()
    {
        weight = Mathf.Clamp01(weight);
        mixer.SetInputWeight(0, 1.0f-weight);
        mixer.SetInputWeight(1, weight);
    }
    void OnDisable()
    {
        // Destroys all Playables and Outputs created by the graph.
        playableGraph.Destroy();
    }
}
````


**Controlling the timing of the PlayableGraph data tree manually**

By default, the `Play()` function in the `PlayableGraph` handles all the timing of the tree playback. However, you can manually set the local time of a Playable. In the below example, the playback is paused, and the time is controlled using a variable:

````
using UnityEngine;
using UnityEngine.Playables;

[RequireComponent (typeof (Animator))]
public class PlayWithTimeControl : MonoBehaviour
{
    public AnimationClip clip;
    public float time;
    PlayableGraph playableGraph;
    PlayableHandle clipPlayableHandle;
    void Start () 
    {
        clipPlayableHandle = AnimationPlayableUtilities.PlayClip(GetComponent<Animator>(), clip, out playableGraph);
        // stops time from progressing automatically.
        clipPlayableHandle.playState = PlayState.Paused;
    }
    void Update () 
    {
        // Control the time manually
        clipPlayableHandle.time = time;
    }
    void OnDisable()
    {
        // Destroys all Playables and Outputs created by the graph.
        playableGraph.Destroy();
    }
}
````

**Controlling the playing state of the tree**

To set the state of the tree, or a branch of the tree, change the `Playable.state` parameter. The state propagates to all children of the node, regardless of their previous state.

__Note:__ If a child node was explicitly paused, set a parent node to the `Playing` state to also set its child to the `Playing` state. 

**Creating ScriptPlayable**

The `Playable` API allows you to create custom Playables derived from `ScriptPlayable`. Override the `PrepareFrame` function for more control over how nodes are handled.

The below example plays animation clips one after the other. The weight of the nodes has been changed so that only one clip plays at a time, and the local time of the clips has been adjusted so that they start at the moment they are activated. 

Custom Playables can also use the `OnSetPlayState` and `OnSetTime` functions to implement custom behaviors when a Playable’s state or local time has changed.

````
using UnityEngine;
using UnityEngine.Playables;

public class PlayQueuePlayable : ScriptPlayable
{
    private int m_CurrentClipIndex = -1;
    private float m_TimeToNextClip;
    private PlayableHandle mixer;
    public void Initialize(AnimationClip[] clipsToPlay)
    {
        handle.inputCount = 1;
        mixer = handle.graph.CreateAnimationMixerPlayable(1);
        handle.graph.Connect(mixer,0, handle,0);
        mixer.inputCount = clipsToPlay.Length;
        for (int clipIndex = 0 ; clipIndex < mixer.inputCount ; ++clipIndex)
        {
            handle.graph.Connect(handle.graph.CreateAnimationClipPlayable(clipsToPlay[clipIndex]),0, mixer, clipIndex);
        }
    }
    override public void PrepareFrame(FrameData info)
    {    
        *// Advance to next clip if necessary*
        m_TimeToNextClip -= (float)info.deltaTime;
        if (m_TimeToNextClip <= 0.0f)
        {
            m_CurrentClipIndex++;
            if (m_CurrentClipIndex < mixer.inputCount)
            {
                var currentClip = mixer.GetInput(m_CurrentClipIndex).GetObject<AnimationClipPlayable>();
                *// Reset the time so that the next clip starts at the correct position*
                currentClip.handle.time = 0;
                m_TimeToNextClip = currentClip.clip.length;
            }
        }
        *// Adjust the weight of the inputs*
        for (int clipIndex = 0 ; clipIndex < mixer.inputCount ; ++clipIndex)
        {
            if (clipIndex == m_CurrentClipIndex)
                mixer.SetInputWeight(clipIndex, 1.0f);
            else
                mixer.SetInputWeight(clipIndex, 0.0f);
        }
    }
}
[RequireComponent (typeof (Animator))]
public class PlayQueue : MonoBehaviour
{
    public AnimationClip[] clipsToPlay;
    PlayableGraph playableGraph;
    void Start ()
    {
        playableGraph = PlayableGraph.CreateGraph();
        var playQueue = playableGraph.CreateScriptPlayable<PlayQueuePlayable>().GetObject<PlayQueuePlayable>();
        playQueue.Initialize(clipsToPlay);
        var playableOutput = playableGraph.CreateAnimationOutput("Animation", GetComponent<Animator>());
        playableOutput.sourcePlayable = playQueue;
        playableGraph.Play();
    }
    void OnDisable()
    {
        *// Destroys all Playables and Outputs created by the graph.*
        playableGraph.Destroy();
    }
}
````



