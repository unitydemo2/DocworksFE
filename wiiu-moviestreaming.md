Movie Streaming
======

Use MovieTexture class to make use of movie streaming on Wii U. Wii U supports hardware-accelerated decoding of MP4 H264 video files. This is also the only format that Unity supports playing back on Wii U. The editor does not include H264 encoder, therefore the movie asset has to be encoded to H264 when added. It will be copied verbatim for use during runtime. 

To use, assign MovieTexture to an object, then call `Play()` method on it.

````
using UnityEngine;

public class RenderMovie : MonoBehaviour
{
	public MovieTexture movTexture;
	public AudioSource audio;

	void Start()
   	{
		GetComponent<MeshRenderer>().material.mainTexture = movTexture;
		GetComponent<AudioSource>().clip = movTexture.audioClip;

		movTexture.Play();
		audio.Play();
	}
}
````

Do have in mind, that decoded audio from a MovieTexture is in an uncompressed format, preventing it from being played on GamePad, which only supports playing GCADPCM format. For a workaround, do have a separate Movie audio clip compressed into GDCADPCM format and play it on GamePad.
