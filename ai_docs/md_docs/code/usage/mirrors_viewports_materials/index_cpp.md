# Creating Mirrors Using Viewports (Rendering to Texture) or a Standard Material (CPP)


![Car Rearview Mirrors](car_mirrors.gif)

*Car Rearview Mirrors*


This example covers some aspects of using viewports and cameras as well as demonstrates 2 different ways of implementing mirrors:

- Using the planar reflection option of the standard [mesh_base](../../../content/materials/library/mesh_base/index.md) material. > **Notice:** Planar reflections don't reflect each other and miss post-effects.
- Using the [Viewport class](../../../api/library/rendering/class.viewport_cpp.md) to render an image from a certain camera to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md) interface and then setting the texture as albedo texture of the mirror material.

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


Another way of creating mirrors is to use a [viewport](../../../api/library/rendering/class.camera_cpp.md) to render an image from a [camera](../../../api/library/rendering/class.camera_cpp.md) placed behind the mirror to a texture and set it as albedo texture for the material of the reflecting surface. This approach can also be used to create various portals or monitors showing an image from a certain camera etc. The basic workflow here is as follows:

1. Create a mesh, that is going to represent a mirror.
2. Inherit a material from the [mesh_base](../../../content/materials/library/mesh_base/index.md).
3. Create a camera and set its projection and modelview matrices (in case of implementing a mirror the camera should be placed behind the mirror looking in the direction of the normal to the reflecting surface).
4. Create a 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to render the image from the camera to.
5. Create a viewport to render the image from the camera to the texture. > **Notice:** It is recommended to use a separate viewport for each camera. In case of using several cameras with a single viewport rendering of screen-space effects should be disabled to avoid artefacts (See the [render_screen_space_effects](../../../code/console/index.md#render_screen_space_effects) console command).
6. Save current [render state](../../../api/library/rendering/class.renderstate_cpp.md) and change necessary settings.
7. Render an image from the camera to the texture using the [renderTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderTexture2D_Camera_Texture_void) method of the [Viewport](../../../api/library/rendering/class.viewport_cpp.md) class.
8. Restore the previously saved render state.
9. Set the texture as albedo texture for the material of the reflecting surface.

 This approach is implemented here for all three small rearview mirrors.
## Using Both Approaches to Create Mirrors for a Car


First let us declare our Car class and all necessary variables and constants.


```cpp
#pragma once
// Car.h
#ifndef __CAR_H__
#define __CAR_H__
#include <UnigineEngine.h>
#include <UnigineObjects.h>
#include <UnigineMaterials.h>
#include <UnigineViewport.h>
#include <UnigineEditor.h>
#include <UnigineGame.h>
#include <UnigineRender.h>

enum
{
	MODE_VIEWPORT_SINGLE = 0,				// use a single viewport for multiple cameras
	MODE_VIEWPORT_MULTIPLE					// use a separate viewport for each camera
};

const float MOVING_SPEED = 10.0f;			// speed of objects movement
const float DELTA_ANGLE = 60.0f;			// delta angle of objects rotation
const int ASPECT_RATIO = 2;					// aspect ratio
const double HFOV = 60;						// horizontal field of view for mirror cameras
const double VFOV = HFOV / ASPECT_RATIO;	// vertical field of view for mirror cameras

// rearview mirror
struct Mirror {
	Unigine::ObjectMeshStaticPtr mesh;		// mirror mesh
	Unigine::String m_type;					// mirror type (left/right/mid)
	Unigine::TexturePtr texture;			// mirror texture
	Unigine::PlayerDummyPtr camera;			// mirror camera
	Unigine::ViewportPtr viewport;			// mirror viewport
	Unigine::Math::Vec3 position;			// mirror position
};

class Car
{
public:
	Car() {	}
	~Car() {	}

	int create_top_mirror();
	int init();
	int update();
	int render();
	int shutdown();

	Unigine::ObjectMeshStaticPtr car_frame;
	Unigine::ObjectMeshDynamicPtr material_mirror;

	Mirror mirrors[3];
	Unigine::ControlsPtr controls;
};
#endif // __CAR_H__

```


And implement all methods using the approaches described above.


```cpp
#include "Car.h"
#include <UnigineConsole.h>
#include <UniginePrimitives.h>
#include <UnigineLights.h>

using namespace Unigine;
using namespace Math;

// setting viewport mode (single/multiple)
int VMODE = MODE_VIEWPORT_MULTIPLE;

///  Method creating a mirror using a Planar Reflection Probe
int Car::create_top_mirror()
{
	// creating a reflecting plane for the top mirror
	// onto which the reflection is to be projected by the probe
	material_mirror = Primitives::createPlane(0.8f, 0.3f, 1);

	// creating a planar reflection probe of the same size
	LightPlanarProbePtr planar_probe = LightPlanarProbe::create();
	planar_probe->setProjectionSize(vec3(1.0f, 0.5f, 1));
	// adding reflection plane and planar probe as children to the car frame
	car_frame->addChild(material_mirror);
	car_frame->addChild(planar_probe);

	// rotating the reflecting plane by 101 degrees around the X-axis and shifting it to its position
	material_mirror->setTransform(Math::translate(Vec3(0.0f, 0.1f, 2.65)) * Math::rotateX(101.0f));

	// putting the planar probe so that it covers the reflecting surface
	planar_probe->setTransform(material_mirror->getTransform());

	// inheriting a new material from the one assigned
	// to the surface by default in order to tweak it
	// and set metalness and roughness values (metallic and polished)
	MaterialPtr plane_mat = material_mirror->getMaterialInherit(0);
	plane_mat->setParameterFloat("metalness", 1.0f);
	plane_mat->setParameterFloat("roughness", 0.0f);

	// setting the distance from the camera, up to which
	// the planar reflection will be visible
	planar_probe->setVisibleDistance(5.0f);

	return 1;
}

int Car::init()
{
	int width = 512;
	int height = width / ASPECT_RATIO;

	// creating car body using a car_body.mesh file
	car_frame = ObjectMeshStatic::create("meshes/car_body.mesh");
	car_frame->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);

	// creating a top rearview mirror a Planar Reflection Probe
	create_top_mirror();

	// setting type and position for all mirrors
	mirrors[0].m_type = "left";
	mirrors[1].m_type = "mid";
	mirrors[2].m_type = "right";
	mirrors[0].position = Vec3(-1.8f, 1.0f, 1.1f);
	mirrors[1].position = Vec3(0.0f, 0.35f, 2.45f);
	mirrors[2].position = Vec3(1.8f, 1.0f, 1.1f);

	// initializing mirrors
	for (int i = 0; i < 3; i++)
	{
		// creating a mesh for the current mirror
		MeshPtr mesh = Mesh::create();
		mesh->addPlaneSurface("mirror_plane", 0.2f, 0.1f, 1);

		// creating the current mirror and setting its transform
		mirrors[i].mesh = ObjectMeshStatic::create("meshes/mirror_plane.mesh");
		mirrors[i].mesh->setTransform(Mat4(translate(vec3(mirrors[i].position)) * rotateX(90.0f)));

		// creating and setting materials for the current mirror mesh
		MaterialPtr mesh_base = Materials::findManualMaterial("Unigine::mesh_base");
		MaterialPtr car_mirror = mesh_base->inherit();
		mirrors[i].mesh->setMaterial(car_mirror, 0);

		// creating a camera for the current mirror and setting its parameters
		mirrors[i].camera = PlayerDummy::create();
		mirrors[i].camera->setProjection(perspective(VFOV, 2.0, 0.05, 10000) * scale(-1.0f, 1.0f, 1.0f));
		mirrors[i].camera->setPosition(mirrors[i].position);
		mirrors[i].camera->setDirection(vec3(0.0f, -1.0f, 0.0f), vec3_up);

		// adding mirror mesh and camera as children to the car frame
		car_frame->addChild(mirrors[i].mesh);
		car_frame->addChild(mirrors[i].camera);

		// creating a 2D texture to be set for the mirror material
		mirrors[i].texture = Texture::create();
		mirrors[i].texture->create2D(width, height, Texture::FORMAT_RGBA8, Texture::FORMAT_USAGE_RENDER);

		// checking viewport mode and creating necessary number of viewports
		if (VMODE == MODE_VIEWPORT_MULTIPLE)
		{
			mirrors[i].viewport = Viewport::create();
		}
		else if ((VMODE == MODE_VIEWPORT_SINGLE) && (i == 1))
		{
			mirrors[i].viewport = Viewport::create();
		}
	}

	// setting up player and controls
	PlayerSpectatorPtr player = PlayerSpectator::create();

	car_frame->addChild(player);
	player->setWorldPosition(Vec3(0.0f, -1.7f, 2.0f));
	player->setControlled(0);
	Game::setPlayer(player);
	Game::setEnabled(1);
	player->setFov(60.0f);
	player->setDirection(vec3(0.0f, 1.0f, 0.0f), vec3(0.0f, 0.0f, 1.0f));
	player->setCollision(0);
	controls = player->getControls();

	return 1;
}

float ifps;

int Car::update()
{
	ifps = Game::getIFps();
	// get the current world transformation matrix of the mesh
	Mat4 transform = car_frame->getWorldTransform();

	// get the direction vector of the mesh from the second column of the transformation matrix
	Vec3 direction = transform.getColumn3(1);

	// checking controls states and changing car frame transformation
	if (controls->getState(Controls::STATE_FORWARD) || controls->getState(Controls::STATE_TURN_UP))
	{
		car_frame->setWorldPosition(car_frame->getWorldPosition() + direction * MOVING_SPEED * ifps);
	}
	if (controls->getState(Controls::STATE_BACKWARD) || controls->getState(Controls::STATE_TURN_DOWN))
	{
		car_frame->setWorldPosition(car_frame->getWorldPosition() - direction * MOVING_SPEED * ifps);
	}
	if (controls->getState(Controls::STATE_MOVE_LEFT) || controls->getState(Controls::STATE_TURN_LEFT))
	{
		car_frame->setWorldRotation(car_frame->getWorldRotation() * quat(0.0f, 0.0f, DELTA_ANGLE * ifps));
		direction.z += DELTA_ANGLE * ifps;
	}
	if (controls->getState(Controls::STATE_MOVE_RIGHT) || controls->getState(Controls::STATE_TURN_RIGHT))
	{
		car_frame->setWorldRotation(car_frame->getWorldRotation() * quat(0.0f, 0.0f, -DELTA_ANGLE * ifps));
		direction.z -= DELTA_ANGLE * ifps;
	}

	return 1;
}

int Car::render()
{
	ViewportPtr viewport;

	for (int i = 0; i < 3; i++)
	{
		MaterialPtr material = mirrors[i].mesh->getMaterialInherit(0);

		if (VMODE == MODE_VIEWPORT_MULTIPLE)
		{
			// using a separate viewport for each camera
			viewport = mirrors[i].viewport;
		}
		else if (VMODE == MODE_VIEWPORT_SINGLE)
		{
			// using a single viewport for all cameras
			viewport = mirrors[1].viewport;

			// skipping post effects when using a single viewport for multiple cameras
			viewport->appendSkipFlags(Viewport::SKIP_POSTEFFECTS);
		}

		// rendering

		// saving current render state and clearing it
		RenderState::saveState();
		RenderState::clearStates();

		// enabling polygon front mode to correct camera flipping
		RenderState::setPolygonFront(1);

		// rendering and image from the camera of the current mirror to the texture
		viewport->renderTexture2D(mirrors[i].camera->getCamera(), mirrors[i].texture);

		// restoring back render state
		RenderState::setPolygonFront(0);
		RenderState::restoreState();

		// setting rendered texture as albedo texture for the material of the current mirror
		material->setTexture(material->findTexture("albedo"), mirrors[i].texture);

	}

	return 1;
}

int Car::shutdown()
{
	car_frame.clear();

	for (int i = 0; i < 3; i++)
	{
		mirrors[i].mesh.clear();
		mirrors[i].texture.clear();
		mirrors[i].camera.clear();
	}

	return 1;
}

```


Let us integrate our car with the **AppWorldLogic** class.


```cpp
// AppWorldLogic.h
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include "Car.h"

class AppWorldLogic : public Unigine::WorldLogic
{

public:

	/* .. */

	Car car;

};
#endif // __APP_WORLD_LOGIC_H__

```


And let us insert the following code into the **AppWorldLogic.cpp** file.


```cpp
#include "AppWorldLogic.h"

/* .. */

int AppWorldLogic::init()
{
	// creating and initializing a car
	car.init();

	return 1;
}
// start of the main loop
int AppWorldLogic::update() {

	// calling car update
	car.update();

	return 1;
}

int AppWorldLogic::postUpdate() {

	// calling car render
	car.render();

	return 1;
}

int AppWorldLogic::shutdown() {

	// calling car shutdown
	car.shutdown();

	return 1;
}

/* .. */


```
