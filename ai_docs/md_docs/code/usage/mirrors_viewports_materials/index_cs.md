# Creating Mirrors Using Viewports (Rendering to Texture) or a Standard Material (CS)


![Car Rearview Mirrors](car_mirrors.gif)

*Car Rearview Mirrors*


This example covers some aspects of using viewports and cameras as well as demonstrates 2 different ways of implementing mirrors:

- Using the planar reflection option of the standard [mesh_base](../../../content/materials/library/mesh_base/index.md) material. > **Notice:** Planar reflections don't reflect each other and miss post-effects.
- Using the [Viewport class](../../../api/library/rendering/class.viewport_cs.md) to render an image from a certain camera to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cs.md) interface and then setting the texture as albedo texture of the mirror material.

 **Key features:**
- 3 rearview mirrors implemented using viewport texture rendering
- large top rearview tilted mirror implemented using the planar reflection option of the [mesh_base](../../../content/materials/library/mesh_base/index.md) material.
- 2 modes:

  - Single viewport for multiple cameras
  - Separate viewport for each camera
- Keyboard control of car movement.


## Using the Standard mesh_base Material


You can create mirrors by simply using the planar reflection option the [mesh_base](../../../content/materials/library/mesh_base/index.md) material. The basic workflow here is as follows:

1. Create a mesh, that is going to represent a mirror.
2. Inherit a material from the [mesh_base](../../../content/materials/library/mesh_base/index.md).
3. For the new inherited material perform the following actions: **For metalness workflow:** **For specular workflow:**

  - Enable the planar reflection option for the new inherited material.

  - Set the value of the [metalness](../../../content/materials/library/mesh_base/index.md#shading_metalness) parameter to **1**.
  - Set the value of the [roughness](../../../content/materials/library/mesh_base/index.md#shading_metalness) parameter to **0**.

  - Set the value of the [gloss](../../../content/materials/library/mesh_base/index.md#specular_workflow) parameter to **1**.
  - Set the value of the [microfiber](../../../content/materials/library/mesh_base/index.md#specular_workflow) parameter to **0**.
4. Tune the reflection_pivot_rotation parameter to compensate rotation of the surface if any.
5. Assign the new inherited material to the reflecting surface.
6. Enable rendering of planar reflections using the [render_reflection_dynamic](../../../code/console/index.md#render_reflection_dynamic) console command.

 This approach is implemented here in the *create_top_mirror()* method, that creates the top rearview tilted mirror.
## Using Viewports (Rendering to Texture)


Another way of creating mirrors is to use a [viewport](../../../api/library/rendering/class.camera_cs.md) to render an image from a [camera](../../../api/library/rendering/class.camera_cs.md) placed behind the mirror to a texture and set it as albedo texture for the material of the reflecting surface. This approach can also be used to create various portals or monitors showing an image from a certain camera etc. The basic workflow here is as follows:

1. Create a mesh, that is going to represent a mirror.
2. Inherit a material from the [mesh_base](../../../content/materials/library/mesh_base/index.md).
3. Create a camera and set its projection and modelview matrices (in case of implementing a mirror the camera should be placed behind the mirror looking in the direction of the normal to the reflecting surface).
4. Create a 2D [texture](../../../api/library/rendering/class.texture_cs.md) to render the image from the camera to.
5. Create a viewport to render the image from the camera to the texture. > **Notice:** It is recommended to use a separate viewport for each camera. In case of using several cameras with a single viewport rendering of screen-space effects should be disabled to avoid artefacts (See the [render_screen_space_effects](../../../code/console/index.md#render_screen_space_effects) console command).
6. Save current [render state](../../../api/library/rendering/class.renderstate_cs.md) and change necessary settings.
7. Render an image from the camera to the texture using the [renderTexture2D()](../../../api/library/rendering/class.viewport_cs.md#renderTexture2D_Camera_Texture_void) method of the [Viewport](../../../api/library/rendering/class.viewport_cs.md) class.
8. Restore the previously saved render state.
9. Set the texture as albedo texture for the material of the reflecting surface.

 This approach is implemented here for all three small rearview mirrors.
## Using Both Approaches to Create Mirrors for a Car


[Create a C# component](../../../principles/component_system/component_system_cs/index.md#create) and add the following code to it:


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Mat4 = Unigine.mat4;
#endif
#endregion

public partial class CarMirrorsExample : Component
{
	enum VMode
	{
		MODE_VIEWPORT_SINGLE,   // use a single viewport for multiple cameras
		MODE_VIEWPORT_MULTIPLE  // use a separate viewport for each camera
	};

	// rearview mirror
	struct Mirror
	{
		public ObjectMeshStatic mesh;                   // mirror mesh
		public String m_type;                           // mirror type (left/right/mid)
		public Texture texture;                         // mirror texture
		public PlayerDummy camera;                      // mirror camera
		public Viewport viewport;                       // mirror viewport
		public Vec3 position;                          // mirror position
	};

	const float MOVING_SPEED = 10.0f;               // speed of objects movement
	const float DELTA_ANGLE = 60.0f;                // delta angle of objects rotation
	const int ASPECT_RATIO = 1;                     // aspect ratio
	const float HFOV = 60;                          // horizontal field of view
	const float VFOV = HFOV / ASPECT_RATIO;         // vertical field of view
	VMode MODE = VMode.MODE_VIEWPORT_MULTIPLE;      // set viewport mode (single/multiple)

	ObjectMeshStatic car_frame;
	ObjectMeshDynamic material_mirror;
	Mirror[] mirrors = new Mirror[3];
	Controls controls;
	float ifps;

	///  Method creating a mirror using a Planar Reflection Probe
	public bool create_top_mirror()
	{
		// creating a reflecting plane for the top mirror
		// onto which the reflection is to be projected by the probe
		material_mirror = Primitives.CreatePlane(0.8f, 0.3f, 1);

		// creating a planar reflection probe of the same size
		LightPlanarProbe planar_probe = new LightPlanarProbe();
		planar_probe.ProjectionSize = new vec3(1.0f, 0.5f, 1);
		// adding reflection plane and planar probe as children to the car frame
		car_frame.AddChild(material_mirror);
		car_frame.AddChild(planar_probe);

		// rotating the reflecting plane by 101 degrees around the X-axis and shifting it to its position
		material_mirror.Transform = MathLib.Translate(new Vec3(0.0f, 0.1f, 2.65)) * MathLib.RotateX(101.0f);

		// putting the planar probe so that it covers the reflecting surface
		planar_probe.Transform = material_mirror.Transform;

		// inheriting a new material from the one assigned
		// to the surface by default in order to tweak it
		// and set metalness and roughness values (metallic and polished)
		Material plane_mat = material_mirror.GetMaterialInherit(0);
		plane_mat.SetParameterFloat("metalness", 1.0f);
		plane_mat.SetParameterFloat("roughness", 0.0f);

		// setting the distance from the camera, up to which
		// the planar reflection will be visible
		planar_probe.VisibleDistance = 5.0f;

		return true;
	}

	private void Init()
	{
		// setting texture width and height
		int width = 512;
		int height = width / ASPECT_RATIO;

		// creating car body using a mesh and passing it to the Editor
		car_frame = new ObjectMeshStatic("meshes/car_body.mesh");
		car_frame.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);

		// creating a top rearview mirror a Planar Reflection Probe
		create_top_mirror();

		// setting type and position for all mirrors
		mirrors[0].m_type = "left";
		mirrors[1].m_type = "mid";
		mirrors[2].m_type = "right";
		mirrors[0].position = new Vec3(-1.8f, 1.0f, 1.1f);
		mirrors[1].position = new Vec3(0.0f, 0.35f, 2.45f);
		mirrors[2].position = new Vec3(1.8f, 1.0f, 1.1f);

		// initializing mirrors
		for (int i = 0; i < 3; i++)
		{
			// creating the current mirror and setting its transform
			mirrors[i].mesh = new ObjectMeshStatic("meshes/mirror_plane.mesh");
			mirrors[i].mesh.Transform = new mat4(MathLib.Translate(new Vec3(mirrors[i].position)) * MathLib.RotateX(90.0f));

			// creating and setting materials for the current mirror mesh
			Material mesh_base = Materials.FindManualMaterial("Unigine::mesh_base");
			Material car_mirror = mesh_base.Inherit();
			mirrors[i].mesh.SetMaterial(car_mirror, 0);

			// creating a camera for the current mirror and setting its parameters
			mirrors[i].camera = new PlayerDummy();
			mirrors[i].camera.Projection = MathLib.Perspective(VFOV, 2.0f, 0.05f, 10000.0f) * MathLib.Scale(-1.0f, 1.0f, 1.0f);
			mirrors[i].camera.Position = mirrors[i].position;
			mirrors[i].camera.SetDirection(new vec3(0.0f, -1.0f, 0.0f), vec3.UP);

			// adding mirror mesh and camera as children to the car frame
			car_frame.AddChild(mirrors[i].mesh);
			car_frame.AddChild(mirrors[i].camera);

			// creating a 2D texture to be set for the mirror material
			mirrors[i].texture = new Texture();

			mirrors[i].texture.Create2D(width, height, Texture.FORMAT_RGBA8, Texture.FORMAT_USAGE_RENDER);

			// checking viewport mode and creating necessary number of viewports
			if (MODE == VMode.MODE_VIEWPORT_MULTIPLE)
			{
				mirrors[i].viewport = new Viewport();
			} else if ((MODE == VMode.MODE_VIEWPORT_SINGLE) && (i == 1))
			{
				mirrors[i].viewport = new Viewport();
			}
		}

		// setting up player and controls
		PlayerSpectator player = new PlayerSpectator();
		car_frame.AddChild(player);
		player.WorldPosition = new Vec3(0.0f, -1.7f, 2.0f);
		player.Controlled = false;
		Game.Player = player;
		Game.Enabled = true;
		player.Fov = 60.0f;
		player.SetDirection(new vec3(0.0f, 1.0f, 0.0f), new vec3(0.0f, 0.0f, 1.0f));
		player.Collision = 0;
		controls = player.Controls;
	}

	private void Update()
	{
		ifps = Engine.IFps;
		// getting the current world transformation matrix of the mesh
		Mat4 transform = car_frame.WorldTransform;

		// getting the direction vector of the mesh from the second column of the transformation matrix
		Vec3 direction = transform.GetColumn3(1);

		// checking controls states and changing car frame transformation
		if ((controls.GetState(Controls.STATE_FORWARD) == 1) || (controls.GetState(Controls.STATE_TURN_UP) == 1))
		{
			car_frame.WorldPosition = car_frame.WorldPosition + direction * MOVING_SPEED * ifps;
		}
		if ((controls.GetState(Controls.STATE_BACKWARD) == 1) || (controls.GetState(Controls.STATE_TURN_DOWN) == 1))
		{
			car_frame.WorldPosition = car_frame.WorldPosition - direction * MOVING_SPEED * ifps;
		}
		if ((controls.GetState(Controls.STATE_MOVE_LEFT) == 1) || (controls.GetState(Controls.STATE_TURN_LEFT) == 1))
		{
			car_frame.SetWorldRotation(car_frame.GetWorldRotation() * new quat(0.0f, 0.0f, DELTA_ANGLE * ifps));
			direction.z += DELTA_ANGLE * ifps;
		}
		if ((controls.GetState(Controls.STATE_MOVE_RIGHT) == 1) || (controls.GetState(Controls.STATE_TURN_RIGHT) == 1))
		{
			car_frame.SetWorldRotation(car_frame.GetWorldRotation() * new quat(0.0f, 0.0f, -DELTA_ANGLE * ifps));
			direction.z -= DELTA_ANGLE * ifps;
		}
	}

	private void PostUpdate()
	{
		Viewport viewport;

		for (int i = 0; i < 3; i++)
		{
			if (MODE == VMode.MODE_VIEWPORT_MULTIPLE)
			{
				// using a separate viewport for each camera
				viewport = mirrors[i].viewport;
			} else
			{
				// using a single viewport for all cameras
				viewport = mirrors[1].viewport;

				// skipping post effects when using a single viewport for multiple cameras to avoid artefacts
				viewport.AppendSkipFlags(Viewport.SKIP_POSTEFFECTS);
			}

			// saving current render state and clearing it
			RenderState.SaveState();
			RenderState.ClearStates();

			// enabling polygon front mode to correct camera flipping
			RenderState.PolygonFront = 1;

			// rendering and image from the camera of the current mirror to the texture
			viewport.RenderTexture2D(mirrors[i].camera.Camera, mirrors[i].texture);

			// restoring back render state
			RenderState.PolygonFront = 0;
			RenderState.RestoreState();

			Material material = mirrors[i].mesh.GetMaterialInherit(0);
			// setting rendered texture as albedo texture for the material of the current mirror
			material.SetTexture(material.FindTexture("albedo"), mirrors[i].texture);
		}
	}
}

```
