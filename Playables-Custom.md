# Creating custom animation Playables

You can create custom animation [Playables](Playables) using the [`CustomAnimationPlayable`](ScriptRef:Experimental.Director.CustomAnimationPlayable) class in the Unity Script Reference (API).

##How to use

In the Script Reference (API), use overloading on the [`PrepareFrame`](ScriptRef:Experimental.Director.Playable.PrepareFrame) method to handle the nodes as you need them. 

In the script example below, the goal is to have animation clips play one after the other. You change the weight of the nodes so that only one clip plays at a time, and adjust the local time of the clips so that they start at the moment they get activated. 

Custom Playables can also use the [`OnSetPlayState`](ScriptRef:Experimental.Director.Playable.OnSetPlayState) and [`OnSetTime`](ScriptRef:Experimental.Director.Playable.OnSetTime) methods, to specify custom behaviors when a Playable's state or local time has changed.


````
using UnityEngine;
using UnityEngine.Experimental.Director;
 
public class PlayQueuePlayable : CustomAnimationPlayable
{
	public int m_CurrentClipIndex = -1;
	public float m_TimeToNextClip;
	public AnimationMixerPlayable m_Mixer;

	public PlayQueuePlayable()
	{		
		m_Mixer = AnimationMixerPlayable.Create();
		AddInput(m_Mixer);
	}

	public void SetInputs(AnimationClip[] clipsToPlay)
	{
		foreach (AnimationClip clip in clipsToPlay)
		{
			m_Mixer.AddInput(AnimationClipPlayable.Create(clip));
		}
	}
 
	override public void PrepareFrame(FrameData info)
	{	
 		// Advance to next clip if necessary
		m_TimeToNextClip -= (float)info.deltaTime;
		if (m_TimeToNextClip <= 0.0f)
		{
			m_CurrentClipIndex++;
			if (m_CurrentClipIndex < m_Mixer.inputCount)
			{
				var currentClip = m_Mixer.GetInput(m_CurrentClipIndex).CastTo<AnimationClipPlayable>();
 
				// Reset the time so that the next clip starts at the correct position
				currentClip.time = 0;
				m_TimeToNextClip = currentClip.clip.length;
			}
			else
			{
				// Pause when queue is complete
				state = PlayState.Paused;
			}
		}
 
		// Adjust the weight of the inputs
		for (int a = 0; a < m_Mixer.inputCount; a++)
		{
			if (a == m_CurrentClipIndex)
				m_Mixer.SetInputWeight(a, 1.0f);
			else
				m_Mixer.SetInputWeight(a, 0.0f);
		}
	}
}
 
 
[RequireComponent (typeof (Animator))]
public class PlayQueue : MonoBehaviour
{
	public AnimationClip[] clipsToPlay;

	void Start ()
	{
		var playQueue =  Playable.Create<PlayQueuePlayable>();
		playQueue.SetInputs(clipsToPlay);

		// Bind the queue to the player
		GetComponent<Animator>().Play(playQueue);
	}
}



````

###Playable lifetime

When a Playable is created using the Unity Script Reference (API), Unity internally keeps track of connections made to that Playable.  When a new scene loads, Unity  automatically releases the resources allocated to all Playables. 

However, it is a good practice to call [`Playable.Destroy()`](ScriptRef:Experimental.Director.Playable.Destroy) explicitly when you have finished with a particular Playable in a scene. This helps Unity to reuse internal resources and so helps to avoid any unnecessary slowing down of your project.

**NOTE:** You use `Playable.Destroy()` in a similar way to  `Object.Destroy()`.

