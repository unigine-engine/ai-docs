# Playing Sounds on Collisions (CS)


The example below demonstrates how to:

- Create a new sound source.
- Update settings of the existing sound source.
- Implement a contact callback that plays a sound at a contact with a physical body.


> **Notice:** The sound file used in the example can be found in the `<UnigineSDK>/data/samples/sounds/sounds` folder. You can also specify any other file, including `.mp3`.


`AppWorldLogic.cs`:


```csharp
#region Math Variables
#if UNIGINE_DOUBLE
using Vec2 = Unigine.dvec2;
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Vec2 = Unigine.vec2;
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
using WorldBoundBox = Unigine.BoundBox;
using WorldBoundSphere = Unigine.BoundSphere;
using WorldBoundFrustum = Unigine.BoundFrustum;
#endif
#endregion

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

class UnigineApp
{
	class AppWorldLogic : WorldLogic
	{

		public struct ContactArguments
		{
			public Body body;
			public int num;

			public ContactArguments(Body body, int num)
			{
				this.body = body;
				this.num = num;
			}
		};

		public List<ContactArguments> events = new List<ContactArguments>();
		public List<SoundSource> sounds = new List<SoundSource>();

		public AppWorldLogic()
		{
		}

		public void contact_handler(Body body, int num)
		{
			events.Add(new ContactArguments(body, num));
		}

		public void contact_event_handler(Body body, int num)
		{

			if (num >= body.NumContacts)
				return;

			// get coordinates of the contact point
			Vec3 position = new Vec3(body.GetContactPoint(num));
			// get the relative impulse in the contact point
			float impulse = body.GetContactImpulse(num);
			// calculate volume of the sound played for the contact
			float volume = impulse * 0.5f - 1.0f;

			// a flag indicating that no sounds have played yet
			bool need_sound = true;

			for (int i = 0; i < sounds.Count; i++)
			{
				if (sounds[i].IsPlaying)
				{
					need_sound = false;

					// reuse the existing sound source
					sounds[i].Enabled = true;
					sounds[i].Gain = MathLib.Saturate(volume);
					sounds[i].WorldTransform = MathLib.Translate(position);
					Sound.RenderWorld(1);
					sounds[i].Play();
					break;
				}
			}
			if (need_sound)
			{
				// create a new sound source
				SoundSource s = new SoundSource("static_impact_00.wav");
				// specify necessary settings for the sound source
				s.Occlusion = 0;
				s.MinDistance = 10.0f;
				s.MaxDistance = 100.0f;
				s.Gain = MathLib.Saturate(volume);
				s.WorldTransform = MathLib.Translate(position);
				// play the sound source
				s.Play();

				// append the sound to the vector of the playing sounds
				sounds.Add(s);
			}
		}

		// method creating a box mesh with a physical body
		public void create_box(Vec3 position)
		{

			ObjectMeshStatic object_mesh = new ObjectMeshStatic("core/meshes/box.mesh");
			object_mesh.WorldTransform = MathLib.Translate(position);
			object_mesh.SetCollision(true, 0);

			BodyRigid body = new BodyRigid(object_mesh);
			new ShapeBox(body, new vec3(1.0f));
			// set a handler function subscribing for a Contact event (when a contact with the box occurs)
			body.EventContactEnter.Connect(contact_handler);

		}

		public override bool Init()
		{

			// create box meshes
			for (int i = -5; i <= 5; i++)
			{
				create_box(new Vec3(0.0f, i * 2.0f, 8.0f + i * 1.0f));
			}
			// create another box mesh
			create_box(new Vec3(5.0f, 10.0f, 50.0f));

			sounds.Clear();
			events.Clear();

			return true;
		}

		public override bool Update()
		{

			if (events.Count > 0)
			{
				for (int i = 0; i < events.Count; i++)
				{
					contact_event_handler(events[i].body, events[i].num);
					events.Remove(events[i]);
				}
				events.Clear();
			}

			return true;
		}

		public override bool PostUpdate()
		{

			return true;
		}

		public override bool UpdatePhysics()
		{

			return true;
		}
		// end of the main loop

		public override bool Shutdown()
		{

			foreach (var s in sounds)

			sounds.Clear();

			return true;
		}
	}
	class AppSystemLogic : SystemLogic
	{
		public override bool Init()
		{
			Engine.BackgroundUpdate = Engine.BACKGROUND_UPDATE.BACKGROUND_UPDATE_RENDER_NON_MINIMIZED;
			Unigine.Console.Run("world_load data/sounds_collisions");
			Unigine.Console.Run("show_visualizer 1");
			return true;
		}
	}

	[STAThread]
	static void Main(string[] args)
	{
		// init engine
		Engine.InitParameters init_params = new Engine.InitParameters();
		init_params.window_title = "UNIGINE Engine: UsageExample - Playing Sounds on Collisions (C#)";
		Engine.Init(init_params, args);

		// enter main loop
		AppSystemLogic system_logic = new AppSystemLogic();
		AppWorldLogic world_logic = new AppWorldLogic();
		Engine.Main(system_logic, world_logic, null);

		// shutdown engine
		Engine.Shutdown();
	}
}

```
