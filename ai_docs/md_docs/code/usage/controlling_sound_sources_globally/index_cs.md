# Controlling Sound Sources Globally (CS)


In this example, you will learn how to stop and start the playback of all sounds on a specific channel.


## Creating Sounds


In order to control sounds in the scene, we should have them. Let's review how to add sounds.


The [Sound Source](../../../objects/sounds/sound_source.md) object can be created in UnigineEditor as a node (let's assume we did this way in our example), while [Ambient Source](../../../api/library/sounds/class.ambientsource_cs.md) doesn't have any specific location and is created via code only.


In the *Init()* method, we create the ambient source and configure it as required.


```csharp
private void Init()
{
	AmbientSource ambient0 = new AmbientSource("sound0.mp3");
		ambient0.SourceMask = 1;
		ambient0.Loop = 1;
		ambient0.Play();

}


```


Having all these sources at hand, we can fine-tune their behavior.


## Getting Sounds


Now we need to get sounds to control them. We'll get Sound Sources by using the method *[World.GetNodesByType()](../../../api/library/engine/class.world_cs.md#getNodesByType_int_VECNode_void)* and add them to the vector storing all sound source nodes:


```csharp
private void GetAllSoundSources(out List<SoundSource> sounds)
{
	List<Node> nodes = new List<Node>();
	World.GetNodesByType((int)Node.TYPE.SOUND_SOURCE, nodes);

	sounds = new List<SoundSource>();
	foreach (var n in nodes)
		sounds.Add(n as SoundSource);
}


```


We'll also declare a vector storing all ambient sounds:


```csharp
private List<AmbientSource> ambientSounds = new List<AmbientSource>();


```


And add one more sound setting in the *Init()* method that will add the ambient sound to the vector:


```csharp
ambientSounds.Add(ambient0);


```


## Controlling the Playback


We can control the playback via the *SoundSource* and the *AmbientSource* class methods *[Play()](../../../api/library/sounds/class.soundsource_cs.md#play_void)*, *[Stop()](../../../api/library/sounds/class.soundsource_cs.md#stop_void)*, and the *[Time](../../../api/library/sounds/class.soundsource_cs.md#setTime_float_void)* property. The general approach is to get all sound sources with the mask of the required channel enabled and then pause them using *[Stop()](../../../api/library/sounds/class.soundsource_cs.md#stop_void)*. This method doesn't reset the playback time, therefore the *[Play()](../../../api/library/sounds/class.soundsource_cs.md#play_void)* method will resume the sound playback from the moment it has been paused.


First, we create a method that plays sounds that have the corresponding sound channel enabled.


```csharp
private void PlaySourceChannel(int number, in List<SoundSource> sounds)
{
	foreach (var s in sounds)
	{
		if ((s.SourceMask & (1 << number)) != 0)
			s.Play();
	}
}


```


Then we create a method that will play both Sound Sources and Ambient Sources on the specified channel at the same time:


```csharp
private void PlaySourceChannel(int number, in List<SoundSource> sources, in List<AmbientSource> ambients)
{
	PlaySourceChannel(number, sources);

	foreach (var a in ambients)
	{
		if ((a.SourceMask & (1 << number)) != 0)
			a.Play();
	}
}


```


Stopping the sound playback uses the same approach.


> **Notice:** If a sound source plays on several channels, disabling it means that it will be disabled on all channels.


```csharp
private void StopSourceChannel(int number, in List<SoundSource> sounds)
{
	foreach (var s in sounds)
	{
		if ((s.SourceMask & (1 << number)) != 0)
			s.Stop();
	}
}

private void StopSourceChannel(int number, in List<SoundSource> sources, in List<AmbientSource> ambients)
{
	StopSourceChannel(number, sources);

	foreach (var a in ambients)
	{
		if ((a.SourceMask & (1 << number)) != 0)
			a.Stop();
	}
}


```


The only thing left is to bind methods and buttons:


```csharp
private void Update()
{
	if (Input.IsKeyDown(Input.KEY.P))
		{
			GetAllSoundSources(out List<SoundSource> sources);
			PlaySourceChannel(0, sources, ambientSounds);
		}

		if (Input.IsKeyDown(Input.KEY.S))
		{
			GetAllSoundSources(out List<SoundSource> sources);
			StopSourceChannel(0, sources, ambientSounds);
		}
}


```


## Code Sample


Here's a complete code:


You can [create a C# component](../../../code/csharp/application.md#logic) and add the following code to it except for the *PropertyGuid* value, which is generated individually for each component at its creation. Keep in mind adding audio files with the corresponding names to your project.


<details>
<summary>AppWorldLogic.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class GlobalSoundSourcesController : Component
{

		private List<AmbientSource> ambientSounds = new List<AmbientSource>();

	private void Init()
	{
		AmbientSource ambient0 = new AmbientSource("sound0.mp3");
			ambient0.SourceMask = 1;
			ambient0.Loop = 1;
			ambient0.Play();
			ambientSounds.Add(ambient0);

			AmbientSource ambient1 = new AmbientSource("sound1.mp3");
			ambient1.SourceMask = 1;
			ambient1.Loop = 1;
			ambient1.Play();
			ambientSounds.Add(ambient1);

	}

	private void Update()
	{
		if (Input.IsKeyDown(Input.KEY.P))
			{
				GetAllSoundSources(out List<SoundSource> sources);
				PlaySourceChannel(0, sources, ambientSounds);
			}

			if (Input.IsKeyDown(Input.KEY.S))
			{
				GetAllSoundSources(out List<SoundSource> sources);
				StopSourceChannel(0, sources, ambientSounds);
			}
	}
		private void GetAllSoundSources(out List<SoundSource> sounds)
		{
			List<Node> nodes = new List<Node>();
			World.GetNodesByType((int)Node.TYPE.SOUND_SOURCE, nodes);

			sounds = new List<SoundSource>();
			foreach (var n in nodes)
				sounds.Add(n as SoundSource);
		}
		private void PlaySourceChannel(int number, in List<SoundSource> sounds)
		{
			foreach (var s in sounds)
			{
				if ((s.SourceMask & (1 << number)) != 0)
					s.Play();
			}
		}
		private void PlaySourceChannel(int number, in List<SoundSource> sources, in List<AmbientSource> ambients)
		{
			PlaySourceChannel(number, sources);

			foreach (var a in ambients)
			{
				if ((a.SourceMask & (1 << number)) != 0)
					a.Play();
			}
		}
		private void StopSourceChannel(int number, in List<SoundSource> sounds)
		{
			foreach (var s in sounds)
			{
				if ((s.SourceMask & (1 << number)) != 0)
					s.Stop();
			}
		}

		private void StopSourceChannel(int number, in List<SoundSource> sources, in List<AmbientSource> ambients)
		{
			StopSourceChannel(number, sources);

			foreach (var a in ambients)
			{
				if ((a.SourceMask & (1 << number)) != 0)
					a.Stop();
			}
		}
}

```

</details>
