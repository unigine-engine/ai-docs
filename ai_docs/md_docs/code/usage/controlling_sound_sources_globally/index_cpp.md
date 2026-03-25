# Controlling Sound Sources Globally (CPP)


In this example, you will learn how to stop and start the playback of all sounds on a specific channel.


## Creating Sounds


In order to control sounds in the scene, we should have them. Let's review how to add sounds.


The [Sound Source](../../../objects/sounds/sound_source.md) object can be created in UnigineEditor as a node (let's assume we did this way in our example), while [Ambient Source](../../../api/library/sounds/class.ambientsource_cpp.md) doesn't have any specific location and is created via code only.


In the *init()* method, we create the ambient source and configure it as required.


```cpp
int AppWorldLogic::init()
{
	AmbientSourcePtr ambient_0 = AmbientSource::create("sound0.mp3");
	ambient_0->setSourceMask(1);
	ambient_0->setLoop(1);
	ambient_0->play();

	return 1;
}


```


Having all these sources at hand, we can fine-tune their behavior.


## Getting Sounds


Now we need to get sounds to control them. We'll get Sound Sources by using the method *[World::getNodesByType()](../../../api/library/engine/class.world_cpp.md#getNodesByType_int_VECNode_void)* and add them to the vector storing all sound source nodes:


```cpp
void getAllSoundSources(Vector<SoundSourcePtr> &out_sounds)
{
	Vector<NodePtr> nodes;
	World::getNodesByType(Node::SOUND_SOURCE, nodes);

	out_sounds.clear();
	for (auto &n : nodes)
		out_sounds.append(checked_ptr_cast<SoundSource>(n));
}


```


We'll also declare a vector storing all ambient sounds:


```cpp
private:
	Unigine::Vector<Unigine::AmbientSourcePtr> ambient_sounds;


```


And add one more sound setting in the *init()* method that will add the ambient sound to the vector:


```cpp
ambient_sounds.append(ambient_0);


```


## Controlling the Playback


We can control the playback via the *SoundSource* and the *AmbientSource* class methods *[play()](../../../api/library/sounds/class.soundsource_cpp.md#play_void)*, *[stop()](../../../api/library/sounds/class.soundsource_cpp.md#stop_void)*, and *[setTime()](../../../api/library/sounds/class.soundsource_cpp.md#setTime_float_void)*. The general approach is to get all sound sources with the mask of the required channel enabled and then pause them using *[stop()](../../../api/library/sounds/class.soundsource_cpp.md#stop_void)*. This method doesn't reset the playback time, therefore the *[play()](../../../api/library/sounds/class.soundsource_cpp.md#play_void)* method will resume the sound playback from the moment it has been paused.


First, we create a method that plays sounds that have the corresponding sound channel enabled.


```cpp
void playSourceChannel(int number, const Vector<SoundSourcePtr> &sounds)
{
	for (auto &s : sounds)
	{
		if (s->getSourceMask() & (1 << number))
			s->play();
	}
}


```


Then we create a method that will play both Sound Sources and Ambient Sources on the specified channel at the same time:


```cpp
void playSourceChannel(int number, const Vector<SoundSourcePtr> &sources, const Vector<AmbientSourcePtr> &ambients)
{
	playSourceChannel(number, sources);

	for (auto &a : ambients)
	{
		if (a->getSourceMask() & (1 << number))
			a->play();
	}
}


```


Stopping the sound playback uses the same approach.


> **Notice:** If a sound source plays on several channels, disabling it means that it will be disabled on all channels.


```cpp
void stopSourceChannel(int number, const Vector<SoundSourcePtr> &sounds)
{
	for (auto &s : sounds)
	{
		if (s->getSourceMask() & (1 << number))
			s->stop();
	}
}

void stopSourceChannel(int number, const Vector<SoundSourcePtr> &sources, const Vector<AmbientSourcePtr> &ambients)
{
	stopSourceChannel(number, sources);

	for (auto &a : ambients)
	{
		if (a->getSourceMask() & (1 << number))
			a->stop();
	}
}


```


The only thing left is to bind methods and buttons:


```cpp
int AppWorldLogic::update()
{
	if (Input::isKeyDown(Input::KEY_P))
	{
		Vector<SoundSourcePtr> sources;
		getAllSoundSources(sources);
		playSourceChannel(0, sources, ambient_sounds);
	}

	if (Input::isKeyDown(Input::KEY_S))
	{
		Vector<SoundSourcePtr> sources;
		getAllSoundSources(sources);
		stopSourceChannel(0, sources, ambient_sounds);
	}

	return 1;
}


```


## Code Sample


Here's a complete code:


<details>
<summary>AppWorldLogic.h | Close</summary>

```cpp
#include <UnigineLogic.h>
#include <UnigineVector.h>
#include <UnigineSounds.h>

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic() {}
	virtual ~AppWorldLogic() {}

	int init() override;
	int update() override;

private:
	Unigine::Vector<Unigine::AmbientSourcePtr> ambient_sounds;
};


```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

```cpp
#include "AppWorldLogic.h"
#include <UnigineWorld.h>
#include <UnigineInput.h>

using namespace Unigine;

void getAllSoundSources(Vector<SoundSourcePtr> &out_sounds)
{
	Vector<NodePtr> nodes;
	World::getNodesByType(Node::SOUND_SOURCE, nodes);

	out_sounds.clear();
	for (auto &n : nodes)
		out_sounds.append(checked_ptr_cast<SoundSource>(n));
}

void playSourceChannel(int number, const Vector<SoundSourcePtr> &sounds)
{
	for (auto &s : sounds)
	{
		if (s->getSourceMask() & (1 << number))
			s->play();
	}
}

void playSourceChannel(int number, const Vector<SoundSourcePtr> &sources, const Vector<AmbientSourcePtr> &ambients)
{
	playSourceChannel(number, sources);

	for (auto &a : ambients)
	{
		if (a->getSourceMask() & (1 << number))
			a->play();
	}
}

void stopSourceChannel(int number, const Vector<SoundSourcePtr> &sounds)
{
	for (auto &s : sounds)
	{
		if (s->getSourceMask() & (1 << number))
			s->stop();
	}
}

void stopSourceChannel(int number, const Vector<SoundSourcePtr> &sources, const Vector<AmbientSourcePtr> &ambients)
{
	stopSourceChannel(number, sources);

	for (auto &a : ambients)
	{
		if (a->getSourceMask() & (1 << number))
			a->stop();
	}
}

int AppWorldLogic::init()
{
	AmbientSourcePtr ambient_0 = AmbientSource::create("sound0.mp3");
	ambient_0->setSourceMask(1);
	ambient_0->setLoop(1);
	ambient_0->play();
	ambient_sounds.append(ambient_0);

	AmbientSourcePtr ambient_1 = AmbientSource::create("sound1.mp3");
	ambient_1->setSourceMask(1);
	ambient_1->setLoop(1);
	ambient_1->play();
	ambient_sounds.append(ambient_1);

	return 1;
}

int AppWorldLogic::update()
{
	if (Input::isKeyDown(Input::KEY_P))
	{
		Vector<SoundSourcePtr> sources;
		getAllSoundSources(sources);
		playSourceChannel(0, sources, ambient_sounds);
	}

	if (Input::isKeyDown(Input::KEY_S))
	{
		Vector<SoundSourcePtr> sources;
		getAllSoundSources(sources);
		stopSourceChannel(0, sources, ambient_sounds);
	}

	return 1;
}


```

</details>
