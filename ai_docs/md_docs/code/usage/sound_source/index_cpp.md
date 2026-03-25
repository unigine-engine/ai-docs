# Playing Sounds on Collisions (CPP)


The example below demonstrates how to:

- Create a new sound source.
- Update settings of the existing sound source.
- Implement a contact callback that plays a sound at a contact with a physical body.


> **Notice:** The sound file used in the example can be found in the `<UnigineSDK>/data/samples/sounds/sounds` folder. You can also specify any other file, including `.mp3`.


`AppWorldLogic.h`:


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UniginePhysics.h>
#include <UnigineMesh.h>
#include <UnigineSounds.h>
#include <UnigineObjects.h>
#include <UnigineEditor.h>

class AppWorldLogic : public Unigine::WorldLogic {

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	virtual int init();

	virtual int update();
	virtual int postUpdate();
	virtual int updatePhysics();

	virtual int shutdown();

private:

	// callbacks
	struct ContactArguments
	{
		Unigine::BodyPtr body;
		int num;

		ContactArguments(const Unigine::BodyPtr &body, int num)
		{
			this->body = body;
			this->num = num;
		}
	};

	Unigine::Vector<ContactArguments> contact_events;
	Unigine::Vector<Unigine::SoundSourcePtr> sounds;
	void contact_handler(const Unigine::BodyPtr &body, int num);
	void contact_event_handler(const Unigine::BodyPtr &body, int num);
	void create_box(Unigine::Math::Vec3 position);
};

#endif // __APP_WORLD_LOGIC_H__

```


`AppWorldLogic.cpp`:


```cpp
#include "AppWorldLogic.h"
// World logic, it takes effect only when the world is loaded.
// These methods are called right after corresponding world script's (UnigineScript) methods.

using namespace Unigine;
using namespace Math;

AppWorldLogic::AppWorldLogic() {

}

AppWorldLogic::~AppWorldLogic() {

}

// a function to be executed when a contact with a given body emerges
void AppWorldLogic::contact_handler(const BodyPtr &body, int num)
{
	ContactArguments ca = ContactArguments(body, num);
	contact_events.append(ca);
}

void AppWorldLogic::contact_event_handler(const BodyPtr &body, int num)
{

	if (num >= body->getNumContacts())
		return;

	// get coordinates of the contact point
	Vec3 position = body->getContactPoint(num);
	// get the relative impulse in the contact point
	float impulse = body->getContactImpulse(num);
	// calculate volume of the sound played for the contact
	float volume = impulse * 0.5f - 1.0f;

	// a flag indicating that no sounds have played yet
	bool need_sound = true;

	for (int i = 0; i < sounds.size(); i++)
	{
		if (!sounds[i]->isPlaying())
		{
			need_sound = false;

			// reuse the existing sound source
			sounds[i]->setEnabled(1);
			sounds[i]->setGain(saturate(volume));
			sounds[i]->setWorldTransform(translate(position));
			Sound::renderWorld(1);
			sounds[i]->play();
			break;
		}
	}
	if (need_sound)
	{
		// create a new sound source
		SoundSourcePtr s = SoundSource::create("static_impact_00.wav");
		// specify necessary settings for the sound source
		s->setOcclusion(0);
		s->setMinDistance(10.0f);
		s->setMaxDistance(100.0f);
		s->setGain(saturate(volume));
		s->setWorldTransform(translate(position));
		// play the sound source
		s->play();

		// append the sound to the vector of the playing sounds
		sounds.append(s);
	}
}

// method creating a box mesh with a physical body
void AppWorldLogic::create_box(Vec3 position)
{

	ObjectMeshStaticPtr object_mesh = ObjectMeshStatic::create("core/meshes/box.mesh");
	object_mesh->setWorldTransform(translate(position));
	object_mesh->setCollision(1, 0);

	BodyRigidPtr body = BodyRigid::create(object_mesh);
	ShapeBox::create(body, vec3(1.0f));
	// subscribe for a contact enter event (when a contact with the box occurs)
	body->getEventContactEnter().connect(this, &AppWorldLogic::contact_handler);

}

int AppWorldLogic::init() {

	// create box meshes
	for (int i = -5; i <= 5; i++) {
		AppWorldLogic::create_box(Vec3(0.0f, i * 2.0f, 8.0f + i * 1.0f));
	}
	// create another box mesh
	AppWorldLogic::create_box(Vec3(5.0f, 10.0f, 50.0f));

	sounds.clear();
	contact_events.clear();

	return 1;
}

int AppWorldLogic::update() {

	if (contact_events.size() > 0)
	{
		for (int i = 0; i > contact_events.size(); i++)
		{
			contact_event_handler(contact_events[i].body, contact_events[i].num);
		}
		contact_events.clear();
	}

	return 1;
}

int AppWorldLogic::postUpdate() {

	return 1;
}

int AppWorldLogic::updatePhysics() {

	return 1;
}

int AppWorldLogic::shutdown() {

	for (int i = 0; i < sounds.size(); i++)
		sounds[i].clear();
	sounds.clear();

	return 1;
}

```
