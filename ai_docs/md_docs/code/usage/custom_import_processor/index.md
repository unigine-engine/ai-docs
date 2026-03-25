# Importing Models Directly to Memory


UNIGINE [Import System](../../../principles/import_system/index_cpp.md) allows you to import models and scenes in various external formats (FBX, DAE, OBJ, etc.). By default (i.e., when *DefaultProcessor* is used) for each imported scene or model a set of corresponding files in UNIGINE file formats (`.mesh, .texture, .node,` etc.) is created on disk.


However, in some cases it might be necessary to import models directly into your current scene on-the-fly, without creating any unnecessary files on disk (e.g. loading models of buildings for a smart city application, etc.). Moreover, this approach can speed up the whole importing process due to a reduced number of slow disk I/O operations.


For this purpose we should create a custom [import processor](../../../principles/import_system/index_cpp.md#processor).


This example demonstrates how to:


- Create your own custom import processor for the **FbxImporter** plugin.
- Use your custom import processor to bring a scene stored in an FBX file to the currently loaded UNIGINE scene.


> **Notice:** It is recommended that you've read the [Import System](../../../principles/import_system/index_cpp.md) article and familiarized with [basic import functionality classes](../../../api/library/common/import/index.md).


Before we get started, a little bit of theory (as key points).


- UNIGINE API offers us a [set of classes](../../../api/library/common/import/index.md) for implementing customized model import.
- All meta information about your imported scene should be stored in an instance of the *[ImportScene](../../../api/library/common/import/class.importscene_cpp.md)* class. Basically a scene may contain meshes (*[ImportMesh](../../../api/library/common/import/class.importmesh_cpp.md)*), lights (*[ImportLight](../../../api/library/common/import/class.importlight_cpp.md)*), cameras (*[ImportCamera](../../../api/library/common/import/class.importcamera_cpp.md)*), and other elements (see the complete list [here](../../../api/library/common/import/class.importscene_cpp.md#intro)).
- A custom import processor should be inherited from the *[ImportProcessor](../../../api/library/common/import/class.importprocessor_cpp.md)* class.


## Creating a Custom Import Processor


So, let's start with the processor. We call it **MemoryProcessor** and implement creation of objects in the current UNIGINE world from the contents of the FBX-file skipping unnecessary saving of data to disk. So we shall simply run through the components of the imported FBX scene (cameras, lights and meshes), build the corresponding node hierarchy to be added to the world and create all necessary materials and textures. The code below is supplemented with comments explaining the basic aspects of the process.


<details>
<summary>Direct Memory Import Processor | Close</summary>

**Direct Memory Import Processor**


```cpp
// including necessary libraries
#include <UnigineImport.h>
#include <UnigineMaterials.h>
#include <UnigineFileSystem.h>

using namespace Unigine;
// our custom ImportProcessor to be used for direct memory import of scenes
class MemoryProcessor : public ImportProcessor
{
public:

	void convertNode(const NodePtr &node_parent, const ImportNodePtr &import_node_parent,
		NodePtr &node, const ImportNodePtr &import_node)
	{
		using namespace Unigine::Math;
		if (ImportCameraPtr import_camera = import_node->getCamera())
		{
			node = getImporter()->importCamera(getImportProcessor(), import_camera);
			if (node)
				node->setWorldTransform(Mat4(import_node->getTransform()));
		} else if (ImportLightPtr import_light = import_node->getLight())
		{
			node = getImporter()->importLight(getImportProcessor(), import_light);
			if (node)
				node->setWorldTransform(Mat4(import_node->getTransform()));
		} else if (ImportMeshPtr import_mesh = import_node->getMesh())
		{
			ObjectPtr object;
			if (import_mesh->isHasAnimations())
			{
				float fps = getImporter()->getParameterFloat("fps");

				auto mesh_skinned = ObjectMeshSkinnedLegacy::create(import_mesh->getFilepath());
				if (!String::isEmpty(import_mesh->getAnimationFilepath()))
					mesh_skinned->setAnimPath(import_mesh->getAnimationFilepath());
				mesh_skinned->setSpeed(fps);
				object = mesh_skinned;
			} else
			{
				ObjectMeshStaticPtr mesh_static = ObjectMeshStatic::create(import_mesh->getFilepath());
				object = mesh_static;
				object->setWorldTransform(Mat4(import_node->getTransform()));
			}

			int num_geometries = import_mesh->getNumGeometries();
			for (int i = 0; i < num_geometries; ++i)
			{
				ImportGeometryPtr geometry = import_mesh->getGeometry(i);
				int num_surfaces = geometry->getNumSurfaces();
				for (int s = 0; s < num_surfaces; ++s)
				{
					ImportSurfacePtr surface = geometry->getSurface(s);
					const int surface_index = surface->getTargetSurface();
					if (surface_index == -1 || surface_index >= object->getNumSurfaces())
					{
						Log::error("MemoryProcessor: can't find surface \"%s\".\n", surface->getName());
						continue;
					}

					if (!compare(surface->getMinVisibleDistance(), -Consts::INF))
					{
						object->setMinVisibleDistance(surface->getMinVisibleDistance(),
							surface_index);
					}
					if (!compare(surface->getMaxVisibleDistance(), Consts::INF))
					{
						object->setMaxVisibleDistance(surface->getMaxVisibleDistance(),
							surface_index);
					}

					object->setMinFadeDistance(surface->getMinFadeDistance(), surface_index);
					object->setMaxFadeDistance(surface->getMaxFadeDistance(), surface_index);

					if (ImportMaterialPtr import_material = surface->getMaterial())
					{
						object->setMaterial(materials[import_material->getFilepath()],
							surface_index);
					}
				}
			}

			node = object;
		} else
		{
			node = NodeDummy::create();
			node->setWorldTransform(Mat4(import_node->getTransform()));
		}

		node->setName(import_node->getName());

		getImporter()->importNodeChild(getImportProcessor(), node_parent, import_node_parent,
			node, import_node);

		int num_children = import_node->getNumChildren();
		for (int i = 0; i < num_children; ++i)
		{
			NodePtr child;
			convertNode(node, import_node, child, import_node->getChild(i));
			node->addWorldChild(child);
		}
	}

protected:
	// method to be called on mesh processing
	bool onProcessMesh(const MeshPtr &mesh, const ImportMeshPtr &import_mesh) override
	{
		StringStack<> mesh_file_path = "import_mesh_temp_blob_";
		mesh_file_path += generate_unique_guid().makeString();
		mesh_file_path += ".mesh";
		if (!create_blob(mesh_file_path))
		{
			return false;
		}

		import_mesh->setFilepath(mesh_file_path);
		return mesh->save(import_mesh->getFilepath());
	}

	// method to be called on mesh animation processing
	bool onProcessAnimation(const MeshAnimationPtr &animation, const ImportMeshPtr &import_mesh,
		const ImportAnimationPtr &import_animation) override
	{
		StringStack<> animation_file_path = "import_animation_temp_blob_";
		animation_file_path += generate_unique_guid().makeString();
		animation_file_path += ".anim";

		if (!create_blob(animation_file_path))
		{
			return false;
		}

		import_animation->setFilepath(animation_file_path);
		if (!animation->save(import_animation->getFilepath()))
		{
			return false;
		}

		import_mesh->setAnimationFilepath(import_animation->getFilepath());
		return true;
	}

	// method to be called on texture processing
	bool onProcessTexture(const ImportTexturePtr &import_texture) override
	{
		if (!Dir::isAbsolute(import_texture->getOriginalFilepath()))
		{
			import_texture->setFilepath(
				String::joinPaths(String::pathname(getImporter()->getSourceFilepath()), import_texture->getOriginalFilepath()));
		}
		else
		{
			import_texture->setFilepath(import_texture->getOriginalFilepath());
		}
		return true;
	}

	// method to be called on material processing
	bool onProcessMaterial(const MaterialPtr &material,
		const ImportMaterialPtr &import_material) override
	{
		UGUID guid = generate_unique_guid();
		import_material->setFilepath(guid.makeString());
		materials.append(guid.makeString(), material);
		return true;
	}

private:
	UGUID generate_unique_guid()
	{
		UGUID guid;
		guid.generate();

		int attempt = 100;
		while (guids.contains(guid) && attempt-- > 0)
			guid.generate();

		guids.append(guid);

		return guid;
	}
private:
	bool create_blob(const String &filepath)
	{
		const bool added = FileSystem::addBlobFile(filepath);
		if (!added)
		{
			Log::error("Can't add a blob file: %s\n", filepath.get());
			return false;
		}
		return true;
	}

private:
	HashSet<UGUID> guids;
	// HashMaps to be used for imported materials
	HashMap<String, MaterialPtr> materials;
};


```

</details>


## Using Our Import Processor


We have got our custom import processor, let's write a function using it to import the contents of the specified FBX to the currently loaded UNIGINE world.


<details>
<summary>Import Function | Close</summary>

**Import Function**


```cpp
/// function importing the contents of the specified FBX to the currently loaded scene
NodePtr import(const char *filepath, Vector<UGUID> &blob_resources)
{
	// creating an importer for our fbx file
	ImporterPtr importer = Import::createImporterByFileName(filepath);
	if (!importer)
		return nullptr;

	if (!importer->init(filepath))
		return nullptr;

	// creating our custom MemoryProcessor and using it to import meshes, textures, materials, and nodes without saving data to files on disk
	MemoryProcessor memory_processor;
	ImportScenePtr scene = importer->getScene();
	int num_meshes = scene->getNumMeshes();
	for (int mesh_index = 0; mesh_index < num_meshes; ++mesh_index)
	{
		MeshPtr m = Mesh::create();
		const ImportMeshPtr &import_mesh = scene->getMesh(mesh_index);

		importer->importMesh(memory_processor.getImportProcessor(), m, import_mesh);

		blob_resources.append(FileSystem::getGUID(import_mesh->getFilepath()));

		if (m->getNumBones())
		{
			int num_animations = scene->getNumAnimations();
			for (int anim_index = 0; anim_index < num_animations; ++anim_index)
			{
				const ImportAnimationPtr &import_animation = scene->getAnimation(anim_index);
				MeshAnimationPtr animation_mesh = MeshAnimation::create();
				importer->importAnimation(memory_processor.getImportProcessor(), animation_mesh,
					import_mesh, import_animation);
				blob_resources.append(FileSystem::getGUID(import_animation->getFilepath()));
			}
		}
	}

	int num_textures = scene->getNumTextures();
	for (int i = 0; i < num_textures; ++i)
	{
		importer->importTexture(memory_processor.getImportProcessor(), scene->getTexture(i));
	}

	MaterialPtr mesh_base = Materials::findManualMaterial("Unigine::mesh_base");
	int num_materials = scene->getNumMaterials();
	for (int i = 0; i < num_materials; ++i)
	{
		MaterialPtr m = mesh_base->inherit();
		importer->importMaterial(memory_processor.getImportProcessor(), m, scene->getMaterial(i));
	}

	int num_nodes = scene->getNumNodes();
	ImportNodePtr root_node;
	for (int i = 0; i < num_nodes; ++i)
	{
		const ImportNodePtr &node = scene->getNode(i);
		if (node->getParent() == nullptr)
		{
			root_node = node;
			break;
		}
	}

	if (root_node)
	{
		NodePtr node;
		memory_processor.setImporter(importer);
		memory_processor.convertNode(nullptr, nullptr, node, root_node);
		return node;
	}

	return nullptr;
}


```

</details>


Now we can just load the **FbxImporter** plugin and use our *import()* function to add the desired model.


```cpp
// including necessary libraries
#include <UnigineConsole.h>

// ...

// loading the FbxImporter plugin
Console::run("plugin_load FbxImporter");
Console::flush();

// importing an FBX-model directly to the scene
NodePtr imported_node = import("material_ball.fbx");

```


## Example Code


To test our custom import processor, we can [create a new C++ project](../../../sdk/projects/index_cpp.md#creation) in *SDK Browser* and put all the code listed below in the `AppWorldLogic.h` and `AppWorldLogic.cpp` files.


<details>
<summary>AppWorldLogic.h | Close</summary>

**AppWorldLogic.h**


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

private:
	void run_animation(const Unigine::NodePtr &node);
	void setup_gui();
	void setup_player(const Unigine::NodePtr &node);
	void import_file(const Unigine::String &filepath);
	void dialog_file_ok_clicked(Unigine::WidgetDialogFilePtr dialog);
	void dialog_file_cancel_clicked(Unigine::WidgetDialogFilePtr dialog);
	void request_import();
	void clean_blob_resources();

	Unigine::NodePtr node_;
	Unigine::Vector<Unigine::UGUID> blob_resources_;
	Unigine::String default_dialog_path{"./"};
};

#endif // __APP_WORLD_LOGIC_H__

```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

**AppWorldLogic.cpp**


```cpp
#include "AppWorldLogic.h"
#include <UnigineMathLib.h>
// including necessary libraries
#include <UnigineImport.h>
#include <UnigineMaterials.h>
#include <UnigineFileSystem.h>
#include <UnigineDir.h>
#include <UnigineGame.h>
#include <UnigineWindowManager.h>
using namespace Unigine;
// our custom ImportProcessor to be used for direct memory import of scenes
class MemoryProcessor : public ImportProcessor
{
public:

	void convertNode(const NodePtr &node_parent, const ImportNodePtr &import_node_parent,
		NodePtr &node, const ImportNodePtr &import_node)
	{
		using namespace Unigine::Math;
		if (ImportCameraPtr import_camera = import_node->getCamera())
		{
			node = getImporter()->importCamera(getImportProcessor(), import_camera);
			if (node)
				node->setWorldTransform(Mat4(import_node->getTransform()));
		} else if (ImportLightPtr import_light = import_node->getLight())
		{
			node = getImporter()->importLight(getImportProcessor(), import_light);
			if (node)
				node->setWorldTransform(Mat4(import_node->getTransform()));
		} else if (ImportMeshPtr import_mesh = import_node->getMesh())
		{
			ObjectPtr object;
			if (import_mesh->isHasAnimations())
			{
				float fps = getImporter()->getParameterFloat("fps");

				auto mesh_skinned = ObjectMeshSkinnedLegacy::create(import_mesh->getFilepath());
				if (!String::isEmpty(import_mesh->getAnimationFilepath()))
					mesh_skinned->setAnimPath(import_mesh->getAnimationFilepath());
				mesh_skinned->setSpeed(fps);
				object = mesh_skinned;
			} else
			{
				ObjectMeshStaticPtr mesh_static = ObjectMeshStatic::create(import_mesh->getFilepath());
				object = mesh_static;
				object->setWorldTransform(Mat4(import_node->getTransform()));
			}

			int num_geometries = import_mesh->getNumGeometries();
			for (int i = 0; i < num_geometries; ++i)
			{
				ImportGeometryPtr geometry = import_mesh->getGeometry(i);
				int num_surfaces = geometry->getNumSurfaces();
				for (int s = 0; s < num_surfaces; ++s)
				{
					ImportSurfacePtr surface = geometry->getSurface(s);
					const int surface_index = surface->getTargetSurface();
					if (surface_index == -1 || surface_index >= object->getNumSurfaces())
					{
						Log::error("MemoryProcessor: can't find surface \"%s\".\n", surface->getName());
						continue;
					}

					if (!compare(surface->getMinVisibleDistance(), -Consts::INF))
					{
						object->setMinVisibleDistance(surface->getMinVisibleDistance(),
							surface_index);
					}
					if (!compare(surface->getMaxVisibleDistance(), Consts::INF))
					{
						object->setMaxVisibleDistance(surface->getMaxVisibleDistance(),
							surface_index);
					}

					object->setMinFadeDistance(surface->getMinFadeDistance(), surface_index);
					object->setMaxFadeDistance(surface->getMaxFadeDistance(), surface_index);

					if (ImportMaterialPtr import_material = surface->getMaterial())
					{
						object->setMaterial(materials[import_material->getFilepath()],
							surface_index);
					}
				}
			}

			node = object;
		} else
		{
			node = NodeDummy::create();
			node->setWorldTransform(Mat4(import_node->getTransform()));
		}

		node->setName(import_node->getName());

		getImporter()->importNodeChild(getImportProcessor(), node_parent, import_node_parent,
			node, import_node);

		int num_children = import_node->getNumChildren();
		for (int i = 0; i < num_children; ++i)
		{
			NodePtr child;
			convertNode(node, import_node, child, import_node->getChild(i));
			node->addWorldChild(child);
		}
	}

protected:
	// method to be called on mesh processing
	bool onProcessMesh(const MeshPtr &mesh, const ImportMeshPtr &import_mesh) override
	{
		StringStack<> mesh_file_path = "import_mesh_temp_blob_";
		mesh_file_path += generate_unique_guid().makeString();
		mesh_file_path += ".mesh";
		if (!create_blob(mesh_file_path))
		{
			return false;
		}

		import_mesh->setFilepath(mesh_file_path);
		return mesh->save(import_mesh->getFilepath());
	}

	// method to be called on mesh animation processing
	bool onProcessAnimation(const MeshAnimationPtr &animation, const ImportMeshPtr &import_mesh,
		const ImportAnimationPtr &import_animation) override
	{
		StringStack<> animation_file_path = "import_animation_temp_blob_";
		animation_file_path += generate_unique_guid().makeString();
		animation_file_path += ".anim";

		if (!create_blob(animation_file_path))
		{
			return false;
		}

		import_animation->setFilepath(animation_file_path);
		if (!animation->save(import_animation->getFilepath()))
		{
			return false;
		}

		import_mesh->setAnimationFilepath(import_animation->getFilepath());
		return true;
	}

	// method to be called on texture processing
	bool onProcessTexture(const ImportTexturePtr &import_texture) override
	{
		if (!Dir::isAbsolute(import_texture->getOriginalFilepath()))
		{
			import_texture->setFilepath(
				String::joinPaths(String::pathname(getImporter()->getSourceFilepath()), import_texture->getOriginalFilepath()));
		}
		else
		{
			import_texture->setFilepath(import_texture->getOriginalFilepath());
		}
		return true;
	}

	// method to be called on material processing
	bool onProcessMaterial(const MaterialPtr &material,
		const ImportMaterialPtr &import_material) override
	{
		UGUID guid = generate_unique_guid();
		import_material->setFilepath(guid.makeString());
		materials.append(guid.makeString(), material);
		return true;
	}

private:
	UGUID generate_unique_guid()
	{
		UGUID guid;
		guid.generate();

		int attempt = 100;
		while (guids.contains(guid) && attempt-- > 0)
			guid.generate();

		guids.append(guid);

		return guid;
	}
private:
	bool create_blob(const String &filepath)
	{
		const bool added = FileSystem::addBlobFile(filepath);
		if (!added)
		{
			Log::error("Can't add a blob file: %s\n", filepath.get());
			return false;
		}
		return true;
	}

private:
	HashSet<UGUID> guids;
	// HashMaps to be used for imported materials
	HashMap<String, MaterialPtr> materials;
};
/// function importing the contents of the specified FBX to the currently loaded scene
NodePtr import(const char *filepath, Vector<UGUID> &blob_resources)
{
	// creating an importer for our fbx file
	ImporterPtr importer = Import::createImporterByFileName(filepath);
	if (!importer)
		return nullptr;

	if (!importer->init(filepath))
		return nullptr;

	// creating our custom MemoryProcessor and using it to import meshes, textures, materials, and nodes without saving data to files on disk
	MemoryProcessor memory_processor;
	ImportScenePtr scene = importer->getScene();
	int num_meshes = scene->getNumMeshes();
	for (int mesh_index = 0; mesh_index < num_meshes; ++mesh_index)
	{
		MeshPtr m = Mesh::create();
		const ImportMeshPtr &import_mesh = scene->getMesh(mesh_index);

		importer->importMesh(memory_processor.getImportProcessor(), m, import_mesh);

		blob_resources.append(FileSystem::getGUID(import_mesh->getFilepath()));

		if (m->getNumBones())
		{
			int num_animations = scene->getNumAnimations();
			for (int anim_index = 0; anim_index < num_animations; ++anim_index)
			{
				const ImportAnimationPtr &import_animation = scene->getAnimation(anim_index);
				MeshAnimationPtr animation_mesh = MeshAnimation::create();
				importer->importAnimation(memory_processor.getImportProcessor(), animation_mesh,
					import_mesh, import_animation);
				blob_resources.append(FileSystem::getGUID(import_animation->getFilepath()));
			}
		}
	}

	int num_textures = scene->getNumTextures();
	for (int i = 0; i < num_textures; ++i)
	{
		importer->importTexture(memory_processor.getImportProcessor(), scene->getTexture(i));
	}

	MaterialPtr mesh_base = Materials::findManualMaterial("Unigine::mesh_base");
	int num_materials = scene->getNumMaterials();
	for (int i = 0; i < num_materials; ++i)
	{
		MaterialPtr m = mesh_base->inherit();
		importer->importMaterial(memory_processor.getImportProcessor(), m, scene->getMaterial(i));
	}

	int num_nodes = scene->getNumNodes();
	ImportNodePtr root_node;
	for (int i = 0; i < num_nodes; ++i)
	{
		const ImportNodePtr &node = scene->getNode(i);
		if (node->getParent() == nullptr)
		{
			root_node = node;
			break;
		}
	}

	if (root_node)
	{
		NodePtr node;
		memory_processor.setImporter(importer);
		memory_processor.convertNode(nullptr, nullptr, node, root_node);
		return node;
	}

	return nullptr;
}

AppWorldLogic::AppWorldLogic(){}

AppWorldLogic::~AppWorldLogic(){}

Vector<String> get_import_extensions()
{
	Vector<String> extensions = Import::getSupportedExtensions();
	extensions.removeOne(""); // ignore default importer
	return extensions;
}

int AppWorldLogic::init()
{
	if (get_import_extensions().empty())
	{
		Log::fatal("No import plugins available.\n");
		return 1;
	}
	setup_gui();
	return 1;
}

void AppWorldLogic::run_animation(const NodePtr &node)
{
	if (ObjectMeshSkinnedLegacyPtr skinned = checked_ptr_cast<ObjectMeshSkinnedLegacy>(node))
	{
		skinned->setLoop(1);
		skinned->play();
	}

	int num_children = node->getNumChildren();
	for (int i = 0; i < num_children; ++i)
		run_animation(node->getChild(i));
}

void AppWorldLogic::setup_gui()
{
	auto gui = Gui::getCurrent();

	auto window = WidgetWindow::create(gui, "Import File", 4, 4);

	StringStack<> info_text
		= "This sample allows importing 3D models in the following file formats:\n";
	info_text += String::join(get_import_extensions(), ", ").upper() + '.';

	auto info_label = WidgetLabel::create(gui, info_text);
	window->addChild(info_label, Gui::ALIGN_EXPAND);

	auto import_button = WidgetButton::create(gui, "Import");
	import_button->getEventClicked().connect(this, &AppWorldLogic::request_import);
	window->addChild(import_button, Gui::ALIGN_EXPAND);

	window->arrange();

	gui->addChild(window, Gui::ALIGN_OVERLAP | Gui::ALIGN_LEFT | Gui::ALIGN_TOP);
}

void AppWorldLogic::setup_player(const NodePtr &node)
{
	constexpr float CAMERA_PHI = 75.0f;
	constexpr float CAMERA_THETA = 140.0f;
	constexpr float CAMERA_DISTANCE = 2.0f;
	constexpr float FOV = 60.0f;

	using namespace Unigine::Math;

	ivec2 window_size = WindowManager::getMainWindow()->getClientSize();

	WorldBoundSphere bound_sphere = node->getHierarchyBoundSphere();

	Vec3 center = bound_sphere.center;
	Scalar radius = bound_sphere.radius * CAMERA_DISTANCE *
		max(1.0f, float(window_size.y) / float(window_size.y));
	quat rotation= quat(1.0f, 0.0f, 0.0f, -CAMERA_PHI) * quat(0.0f, 0.0f, 1.0f, CAMERA_THETA);

	Mat4 modelview{translate(Scalar(0.0f), Scalar(0.0f), -radius) *
		Mat4(rotation) * translate(-center)};

	mat4 projection = perspective(FOV, 1.0f, radius * 0.01f, radius * 2.0f);
	if (PlayerPtr player = Game::getPlayer())
	{
		player->setWorldTransform(inverse(modelview));
		player->setProjection(projection);
	} else
		Log::error("Main player not found.\n");
}

void AppWorldLogic::clean_blob_resources()
{
	for (const UGUID &guid : blob_resources_)
	{
		FileSystem::removeBlobFile(guid);
		FileSystem::removeVirtualFile(guid);
	}
	blob_resources_.clear();
}

void AppWorldLogic::import_file(const String &filepath)
{
	if (node_)
	{
		node_.deleteLater();
		node_ = nullptr;
	}

	clean_blob_resources();

	node_ = import(filepath, blob_resources_);
	if (node_)
	{
		Log::message("Node loaded \"%s\" from filepath \"%s\".\n",
			node_->getName(), filepath.get());
		setup_player(node_);
		run_animation(node_);
	}
	else
		Log::error("Can't import file from filepath %s\n", filepath.get());
}

void AppWorldLogic::dialog_file_ok_clicked(WidgetDialogFilePtr dialog)
{
	const String filepath = dialog->getFile();
	default_dialog_path = filepath.pathname();

	import_file(filepath);

	dialog.deleteLater();
}

void AppWorldLogic::dialog_file_cancel_clicked(WidgetDialogFilePtr dialog)
{
	dialog.deleteLater();
}

void AppWorldLogic::request_import()
{
	const Vector<String> supported_extensions = get_import_extensions();
	const String extensions_filter = "." + String::join(supported_extensions, ".");

	auto dialog_file = WidgetDialogFile::create(Gui::getCurrent(), "DialogFile");
	dialog_file->setPath(default_dialog_path);
	dialog_file->setFilter(extensions_filter);

	dialog_file->getOkButton()->getEventClicked().connect(this, &AppWorldLogic::dialog_file_ok_clicked, dialog_file);
	dialog_file->getCancelButton()->getEventClicked().connect(this, &AppWorldLogic::dialog_file_cancel_clicked, dialog_file);

	Gui::getCurrent()->addChild(dialog_file, Gui::ALIGN_OVERLAP | Gui::ALIGN_CENTER);

	dialog_file->setPermanentFocus();
	}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::update()
{
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
	return 1;
}

int AppWorldLogic::postUpdate()
{
	// The engine calls this function after updating each render frame: correct behavior after the state of the node has been updated.
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::shutdown()
{
	// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
	clean_blob_resources();
	return 1;
}

```

</details>
