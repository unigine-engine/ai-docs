# Playing Sounds on Collisions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The example below demonstrates how to:

- Create a new sound source.
- Update settings of the existing sound source.
- Implement a contact callback that plays a sound at a contact with a physical body.


> **Notice:** The sound file used in the example can be found in the `<UnigineSDK>/data/samples/sounds/sounds` folder. You can also specify any other file, including `.mp3`.


```cpp
#include <core/unigine.h>

SoundSource sounds[0];

void contact_callback(Body body,int num)
{

	if (num >= body.getNumContacts())
		        return;

	// get coordinates of the contact point
	Vec3 position = body.getContactPoint(num);
	// get the relative impulse in the contact point
	float impulse = body.getContactImpulse(num);
	// calculate volume of the sound played for the contact
	float volume = impulse * 0.5f - 1.0f;

	// a flag indicating that no sounds have played yet
	int need_sound = 1;
	for (int i = 0; i < sounds.size(); i++)
	{
		if (sounds[i].isPlaying() == 0)
		{
			need_sound = 0;

			// reuse the existing sound source
			sounds[i].setEnabled(1);
			sounds[i].setGain(saturate(volume));
			sounds[i].setWorldTransform(translate(position));
			engine.sound.renderWorld(1);
			sounds[i].play();
			break;
		}
	}
	if (need_sound)
	{
		// create a new sound source
		SoundSource s = new SoundSource("static_impact_00.wav");
		// specify necessary settings for the sound source
		s.setOcclusion(0);
		s.setMinDistance(10.0f);
		s.setMaxDistance(100.0f);
		s.setGain(saturate(volume));
		s.setWorldTransform(translate(position));
		// play the sound source
		s.play();

		// append the sound to the vector of the playing sounds
		sounds.append(s);
	}
}

// method creating a box mesh with a physical body
void create_box(Vec3 position)
{
	ObjectMeshStatic object = node_remove(new ObjectMeshStatic("core/meshes/box.mesh"));

	object.setWorldTransform(translate(position));
	object.setCollision(1, 0);

	BodyRigid body = class_remove(new BodyRigid(object));
	class_remove(new ShapeBox(body,vec3(0.5f)));
	// set a callback function that is run when a contact with the box occurs
	body.setContactCallback(functionid(contact_callback));
}

int init() {

	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,-3.401f,1.5f));
	player.setDirection(Vec3(0.0f,1.0f,-0.4f));
	engine.game.setPlayer(player);

	// create box meshes
	for(int i = -5; i <= 5; i++)
	{
		create_box(Vec3(0.0f,i * 2.0f,8.0f + i * 1.0f));
	}
	// create another box mesh
	create_box(Vec3(0.0f,0.0f,50.0f));

	return 1;
}

int update() {

	foreach(SoundSource s; sounds)
	{
		if(!s.isPlaying()) s.setEnabled(0);
	}

	return 1;
}

int postUpdate() {

	return 1;
}

int updatePhysics() {

	return 1;
}

int shutdown() {

	return 1;
}

```
