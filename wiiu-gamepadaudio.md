Audio
=====

## Playing Audio on GamePad

By default, AudioSource will play back through a TV speaker. To change the output device, call a platform-specific API which is represented by `UnityEngine.WiiU.AudioSourceOutput` class. It allows you to query and change bits of a value that controls the output device assignment. Output can be TV, GamePad, any of Wii Remotes or a combination thereof - multiple devices are supported.

````
public void AssignToTVAndGamePad (AudioSource audio)
{
	WiiU.AudioSourceOutput.Assign (audio, WiiU.AudioOutput.TV|WiiU.AudioOutput.GamePad);
}
````

`WiiU.GamePad.AssignAudioSource` is implemented in terms of this functionality.

## Audio Compression and Decoding


Starting with version 5, Unity supports the following formats on Wii U: Vorbis, ADPCM, GCADPCM and uncompressed. The following table describes how various format are decoded:

| | |
|:--|:--|:--|
|Format    	|Decoding	|Notes|
|Vorbis		|Software	|Requires the most processing, but offers highest compression ratio. Use this only when it is absolutely necessary to save distribution size. Keep in mind that decoder for vorbis stream also allocates memory, in order of hundreds of kB, depends on the file and compression.|
|GCADPCM	|Hardware	|Wii U specific format, decoded by DSP hardware. The only format supported on GamePad.|
|ADPCM		|Software	|While decoded in software, the speed using this is similar to GCADPCM.|
|uncompressed|n/a		|Minimal processing cost.|

Generally for static sounds you want to use GCADPCM. It has a good compresion ratio and high performance. At the same time try to keep number of concurent audio clips playing low enough not to exceed what DSP can handle. Use Vorbis only for very large files and don't use at all if distribution size is of no concern.

| |
|:--|:--|
|Load Type	|Notes|
|Memory		|The sound data remains in *import format* after load. This is the preferable method to load audio.|
|Streaming	|Audio data is read and decompressed on-demand. Use this for large files like music and don't play more that 1-2 streaming clips simultaneously.|
|Decompress on Load|This type should be avoided. Useful when distribution size important (then strongest compression is used and data is converted to uncompressed to not incur runtime processing cost) and free runtime memory is plenty.|

The guideline is to prefer sounds kept in memory. Storing large files in memory can result in unavailable memory, so use streaming for large files.

