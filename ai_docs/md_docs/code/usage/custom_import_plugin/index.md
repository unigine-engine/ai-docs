# Custom Import Plugin


UNIGINE's [Import System](../../../principles/import_system/index_cpp.md) allows you to import models and scenes in various external formats (FBX, DAE, OBJ, etc.). Although the basic set of file formats supported by UNIGINE out-of-the-box includes the most commonly used ones, in some cases you may need to import models or scenes in some specific file format. Fortunately, the Import System can be extended to support any custom file format.


This example demonstrates how to:


- Implement your own custom importer as a plugin.
- Create your own import pre-processor.
- Use your custom importer to bring a scene stored in a custom file format to UNIGINE.


> **Notice:** It is recommended that you've read the [Import System](../../../principles/import_system/index_cpp.md) article and familiarized with [basic import functionality classes](../../../api/library/common/import/index.md).


So, in this example, we are going to create a custom [importer](../../../principles/import_system/index_cpp.md#importer) for a custom file format. Let it be an XML-based format in which we declare our scene as a hierarchy of nodes that have a transformation and can have a mesh, light, or camera attribute. Let our file format have a `.myext` extension. An example of a scene in our custom format containing all available elements is given below.


<details>
<summary>my_scene.myext | Close</summary>

**my_scene.myext**


```xml
<?xml version="1.0"?>
<scene name="my_custom_scene">
	<node name="root">
		<node name="Mesh1">
			<attribute type="mesh">
				<surfaces>
					<surface name="cube_surface1" offset="0" size="12"/>
					<surface name="cube_surface2" offset="12" size="12"/>
					<surface name="cube_surface3" offset="24" size="12"/>
				</surfaces>
				<vertices>
					<vertex>0.0 0.0 0.0</vertex>
					<vertex>0.0 1.0 0.0</vertex>
					<vertex>1.0 1.0 0.0</vertex>
					<vertex>1.0 0.0 0.0</vertex>
					<vertex>0.0 0.0 1.0</vertex>
					<vertex>0.0 1.0 1.0</vertex>
					<vertex>1.0 1.0 1.0</vertex>
					<vertex>1.0 0.0 1.0</vertex>
				</vertices>
				<indices num_indices="36">0 1 2 2 3 0 4 7 6 6 5 4 3 2 6 6 7 3 4 5 1 1 0 4 4 0 3 3 7 4 5 6 2 2 1 5</indices>
			</attribute>
			<transform>1 0 0 0.0 0 1 0 0.0 0 0 1 0.0 -0.5 -1 0.0 1.0</transform>
		</node>
		<node name="OmniLight1">
			<attribute type="light">
				<light_type>LIGHT_OMNI</light_type>
				<color>0.0 1.0 0.0 1.0</color>
				<intensity>0.5f</intensity>
			</attribute>
			<transform>1 0 0 0.0 0 1 0 0.0 0 0 1 0.0 5.0 5.0 5.0 1.0</transform>
		</node>
		<node name="OmniLight2">
			<attribute type="light">
				<light_type>LIGHT_OMNI</light_type>
				<color>0.0 0.0 1.0 1.0</color>
				<intensity>0.5f</intensity>
			</attribute>
			<transform>1 0 0 0.0 0 1 0 0.0 0 0 1 0.0 -5.0 5.0 5.0 1.0</transform>
		</node>
		<node name="ProjectedLight1">
			<attribute type="light">
				<light_type>LIGHT_PROJ</light_type>
				<color>1.0 0.0 0.0 1.0</color>
				<intensity>1.0f</intensity>
			</attribute>
			<transform>1 0 0 0.0 0 1 0 0.0 0 0 1 5.0 0 0 3.0 1.0</transform>
		</node>
		<node name="my_camera">
			<attribute type="camera">
				<camera_type>TYPE_PERSPECTIVE</camera_type>
				<near>0.001f</near>
				<far>10000.0f</far>
				<fov>60.0f</fov>
				<target>10.0 10.0 10.0</target>
			</attribute>
			<transform>1 0 0 0.0 0 1 0 0.0 0 0 1 0.0 0.0 -2.0 2.0 1.0</transform>
		</node>
	</node>
</scene>

```

</details>


For our importer, we're going to create and use a custom pre-processor to reset light colors to white when the corresponding flag is set. Thus, we're going to have the following import options and parameters:


- **scale** - scale factor to be used for imported scene
- **vertex_cache** - vertex cache optimization for meshes
- **make_lights_white** - reset light colors flag for our pre-processor


At the end of this example, we're going to have this model imported to UNIGINE's world and saved in UNIGINE's native file formats in the specified folder. But before we get started, a little bit of theory (as key points).


- UNIGINE's API offers us a [set of classes](../../../api/library/common/import/index.md) for implementing customized model import.
- All meta information about your imported scene should be stored in an instance of the *[ImportScene](../../../api/library/common/import/class.importscene_cpp.md)* class. Basically a scene may contain meshes (*[ImportMesh](../../../api/library/common/import/class.importmesh_cpp.md)*), lights (*[ImportLight](../../../api/library/common/import/class.importlight_cpp.md)*), cameras (*[ImportCamera](../../../api/library/common/import/class.importcamera_cpp.md)*), and other elements (see the complete list [here](../../../api/library/common/import/class.importscene_cpp.md#intro)). You can specify which of these scene components are to be imported using the corresponding [import flags](../../../api/library/common/import/class.importer_cpp.md#IMPORT_LIGHTS) (*IMPORT_MESHES, IMPORT_LIGHTS*, etc.)
- A custom importer should be inherited from the *[Importer](../../../api/library/common/import/class.importer_cpp.md)* class.
- A custom import processor should be inherited from the *[ImportProcessor](../../../api/library/common/import/class.importprocessor_cpp.md)* class.


Enough words! Let's get to business! The code below is supplemented with comments explaining the basic aspects of the process.


## Making a Plugin


As you know, each importer should be implemented as a plugin. So, we're going to create a C++ plugin.


> **Notice:** To learn more about creating a C++ plugin, please, refer to [this article](../../../code/cpp/plugin.md).


First, we inherit our import plugin from the *[Plugin](../../../api/library/common/class.plugin_cpp.md)* class. Then we specify a plugin name by overriding the *[get_name()](../../../api/library/common/class.plugin_cpp.md#get_name_const_char_ptr)* method and also override the *[init()](../../../api/library/common/class.plugin_cpp.md#init_int)* and *[shutdown()](../../../api/library/common/class.plugin_cpp.md#shutdown_int)* methods to perform initialization and cleanup. As a result, we will have the following header file:


<details>
<summary>MyImportPlugin.h | Close</summary>

**MyImportPlugin.h**


```cpp
#pragma once
#include <UniginePlugin.h>
#include <UnigineVector.h>

struct MyImporterParameters;

class MyImportPlugin : public Unigine::Plugin
{
protected:
	// specifying our plugin's name
	const char *get_name() override;

	// overriding methods for initialization and cleanup on shutdown
	int init() override;
	int shutdown() override;

private:
	MyImporterParameters *importer_parameters{ nullptr };
	Unigine::Vector<void *> registered_importers;
	Unigine::Vector<void *> registered_processors;
};

```

</details>


As for plugin implementation, it's also simple. We include the header files for our importer and processor (`MyImporter.h` and `MyImportProcessor.h`) in addition to the plugin header file, implement plugin initialization and cleanup, and export the plugin.


<details>
<summary>MyImportPlugin.cpp | Close</summary>

**MyImportPlugin.cpp**


```cpp
#include "MyImportPlugin.h"
#include "MyImporter.h" // our importer's header file
#include "MyImportProcessor.h" // our import processor's header file

struct MyImporterParameters
{
	Unigine::String string_parameter;
};

namespace
{

	Unigine::Importer *importer_creator(void *args)
	{
		auto parameters = static_cast<MyImporterParameters *>(args);
		Unigine::Log::message("ImporterParameter: %s\n", parameters->string_parameter.get());
		return new MyImporter();
	}
	void importer_deletor(Unigine::Importer *importer, void *) { delete static_cast<MyImporter *>(importer); }

	Unigine::ImportProcessor *processor_creator(void *) { return new MyImportProcessor(); }
	void processor_deletor(Unigine::ImportProcessor *processor, void *) { delete processor; }

}

const char *MyImportPlugin::get_name()
{
	return "MyImportPlugin";
}

// plugin initialization
int MyImportPlugin::init()
{
	importer_parameters = new MyImporterParameters();
	importer_parameters->string_parameter = "MyStringParameter";

	// registering our custom importer and import processor
	for (const auto &ext : MyImporter::getExtensions())
	{
		registered_importers.append(Unigine::Import::registerImporter("MyVendorName", "MyImporter", ext, importer_creator, importer_deletor, importer_parameters));
	}

	if (!Unigine::Import::containsImportProcessor("MyImportProcessor"))
	{
		registered_processors.append(Unigine::Import::registerImportProcessor("MyImportProcessor", processor_creator, processor_deletor));
	}

	return 1;
}

// plugin cleanup on shutdown
int MyImportPlugin::shutdown()
{
	// removing our custom importer and import processor from the registry
	for (void *handle : registered_importers)
		Unigine::Import::unregisterImporter(handle);
	registered_importers.clear();

	for (void *handle : registered_processors)
		Unigine::Import::unregisterImportProcessor(handle);
	registered_processors.clear();

	delete importer_parameters;
	importer_parameters = nullptr;

	return 1;
}

extern "C"
{

	UNIGINE_EXPORT void *CreatePlugin()
	{
		return new MyImportPlugin();
	}

	UNIGINE_EXPORT void ReleasePlugin(void *plugin)
	{
		delete static_cast<MyImportPlugin *>(plugin);
	}

}

```

</details>


## Implementing Import Functionality


First, we should define some intermediate data structures to which all parameters of the imported scene elements are to be extracted.


<details>
<summary>Auxiliary Data Structures | Close</summary>

**Auxiliary Data Structures**


```cpp
#pragma once
#include <UnigineMathLib.h>
#include <UnigineString.h>
#include <UnigineVector.h>

using namespace Unigine;

// camera metadata structure
struct MyCamera
{
	String type;
	float near_plane;
	float far_plane;
	float fov;
	Math::vec3 target;
};

// light metadata structure
struct MyLight
{
	String type;
	float intensity;
	Math::vec4 color;
};

// mesh metadata structure
struct MyMesh
{
	String type;
	Vector<String> surfaces;
	Vector<Math::ivec3> polygons;
	Vector<Math::vec3> vertices;
	Vector<int> indices;
};

```

</details>


The general workflow will be as follows:


1. Create an *ImportScene* instance within the override of the *[Importer::onImport()](../../../api/library/common/import/class.importer_cpp.md#onImport_cstr_bool)* method: <details> <summary>MyImporter::onInit() | Close</summary> **MyImporter.cpp** ```cpp bool MyImporter::onInit(const ImportScenePtr &scene, const char *filepath) { // getting all necessary import parameters and making necessary preparations for scene import scale = getParameterFloat("scale"); String filesystem_filepath = FileSystem::getAbsolutePath(filepath); my_scene = Xml::create(); my_scene->load(filesystem_filepath); Log::message("\n\nLAUNCHING IMPORTING PROCESS... \n"); // parse input file and fill metadata structures return import_scene(scene); } ``` </details>
2. Extract data from the input file, put it to the corresponding import structures (*ImportMesh, ImportLight*, etc.) and add them to the scene. Our XML file parsing is implemented in the *MyImporter::import_scene()* and *MyImporter::process_node()* functions: <details> <summary>MyImporter::import_scene() | Close</summary> **MyImporter.cpp** ```cpp bool MyImporter::import_scene(const ImportScenePtr &import_scene) { // performing necessary checks on file format String n = my_scene->getName(); if (n != "scene") { Log::error("Scene loader: bad my_scene format\n"); return 0; } // checking scene name String name = my_scene->getArg("name"); if (name.empty()) { Log::error("Scene loader: scene name can't be empty\n"); return 0; } // parsing the input file and filling the ImportScene auto num_nodes = my_scene->getNumChildren(); Log::message("Importing [%s] scene num_nodes = %d\n", name.get(), num_nodes); for (int i = 0; i < num_nodes; i++) { const XmlPtr child_xml = my_scene->getChild(i); const String &child_name = child_xml->getName(); if (child_name == "node") { process_node(import_scene, nullptr, child_xml); } else { Log::error("Scene loader: unknown element \"%s\" in the \"%s\" scene\n", child_name.get(), name.get()); } } return true; } ``` </details> <details> <summary>MyImporter::process_node() | Close</summary> **MyImporter.cpp** ```cpp void MyImporter::process_node(const ImportScenePtr &import_scene, const ImportNodePtr &parent, XmlPtr scene_node) { ImportNodePtr node = import_scene->addNode(parent); node->setName(scene_node->getArg("name")); if (scene_node->getChild("transform")) { Math::dmat4 transform = scene_node->getChild("transform")->getDMat4Data(); transform.m03 *= scale; transform.m13 *= scale; transform.m23 *= scale; node->setTransform(transform); } // processing node attributes XmlPtr attribute = scene_node->getChild("attribute"); if (attribute) { String attr_type = attribute->getArg("type"); if (attr_type == "light") { // creating and filling light metadata MyLight *light = new MyLight(); lights.append(light); light->type = attribute->getChildData("light_type"); light->color = attribute->getChild("color")->getVec4Data(); light->intensity = attribute->getChild("intensity")->getFloatData(); // processing light metadata and adding ImportLight to the scene process_light(import_scene, node, light); Log::message("Artribute light: named %s , type %s, color (%f, %f, %f, %f)\n", node->getName(), light->type.get(), light->color.x, light->color.y, light->color.z, light->color.w); } else if (attr_type == "camera") { // creating and filling camera metadata MyCamera *camera = new MyCamera(); cameras.append(camera); camera->type = attribute->getChildData("player_type"); camera->fov = attribute->getChild("fov")->getFloatData(); camera->near_plane = attribute->getChild("near")->getFloatData(); camera->far_plane = attribute->getChild("far")->getFloatData(); camera->target = attribute->getChild("target")->getVec3Data(); // processing camera metadata and adding ImportCamera to the scene process_camera(import_scene, node, camera); Log::message("Artribute camera: named %s , type %s, target (%f, %f, %f)\n", node->getName(), camera->type.get(), camera->target.x, camera->target.y, camera->target.z); } else if (attr_type == "mesh") { // creating and filling mesh metadata MyMesh *mesh = new MyMesh(); meshes.append(mesh); int num_surfaces = attribute->getChild("surfaces")->getNumChildren(); int num_vertices = attribute->getChild("vertices")->getNumChildren(); Log::message("Artribute mesh: named %s , %d surfaces, %d vertices\n", node->getName(), num_surfaces, num_vertices); // getting all surfaces for (int i = 0; i < num_surfaces; ++i) { XmlPtr xml_surf = attribute->getChild("surfaces")->getChild(i); mesh->surfaces.append(xml_surf->getArg("name")); // filling polygons data mesh->polygons.append( Math::ivec3(i, xml_surf->getIntArg("offset"), xml_surf->getIntArg("size"))); Log::message("\nSurface [%d] named: %s\n", i, mesh->surfaces[i].get()); } // getting all vertices for (int i = 0; i < num_vertices; ++i) { mesh->vertices.append(attribute->getChild("vertices")->getChild(i)->getVec3Data()); Log::message("Vertex [%d] coordinates:(%f, %f, %f)\n", i, mesh->vertices[i].x, mesh->vertices[i].y, mesh->vertices[i].z); } // getting all indices XmlPtr indices_xml = attribute->getChild("indices"); int num_indices = indices_xml->getIntArg("num_indices"); mesh->indices.resize(num_indices); indices_xml->getIntArrayData(mesh->indices.get(), num_indices); // processing mesh metadata and adding ImportMesh to the scene process_mesh(import_scene, node, mesh); } } // processing all node's children int num_children = scene_node->getNumChildren(); for (int i = 0; i lt; num_children; ++i) { XmlPtr child = scene_node->getChild(i); const String &child_name = child->getName(); if (child_name == "node") process_node(import_scene, node, child); } } ``` </details> Scene components are added to the hierarchy in the corresponding *MyImporter::process_*()* methods. For example, for lights we'll have: <details> <summary>MyImporter::process_light() | Close</summary> **MyImporter.cpp** ```cpp void MyImporter::process_light(const ImportScenePtr &import_scene, const ImportNodePtr &node, MyLight *my_light) { Log::message("\n FUNCTION: process_light() reporting... \n"); // checking if the light import flag is set if ((getFlags() & IMPORT_LIGHTS) == 0) return; // adding a light source to the scene and setting lignt source data ImportLightPtr light = import_scene->addLight(node); light->setData(my_light); } ``` </details>
3. Use pre-processor(s) to prepare scene metadata when necessary (e.g. merge all static meshes into a single one, optimize vertex cache, etc.). In our example, we're going to strip off light color information if the corresponding option (**make_lights_white**) is set. For a pre-processor, we should only override the *[ImportProcessor::onProcessScene()](../../../api/library/common/import/class.importprocessor_cpp.md#onProcessScene_ImportScene_bool)* method. <details> <summary>MyImportProcessor.h | Close</summary> **Custom Pre-Processor** ```cpp #pragma once #include <UnigineImport.h> // inheriting our custom pre-processor from the ImportProcessor; // as it is a pre-processor we should only override the onProcessScene() method class MyImportProcessor : public Unigine::ImportProcessor { protected: bool onProcessScene(const Unigine::ImportScenePtr &scene) override; }; ``` </details> <details> <summary>MyImportProcessor.cpp | Close</summary> **Custom Pre-Processor** ```cpp #include "MyImportProcessor.h" #include "MyImporterData.h" using namespace Unigine; // custom scene preprocessor stripping out color information from all scene light sources bool MyImportProcessor::onProcessScene(const ImportScenePtr &scene) { Log::message("\n MyImportProcessor reporting... \n"); // getting the number of lights in the scene int num_lights = scene->getNumLights(); // checking if the scene contains lights and the make_lights_white flag is set if (getImporter()->getParameterInt("make_lights_white")) { for (int i = 0; i < num_lights; i++) { // getting light data from the ImportLight sctructure MyLight *light = static_cast<MyLight *>(scene->getLight(i)->getData()); // setting color to white light->color = Math::vec4_one; } } return true; } ``` </details>
4. Process scene metadata corresponding to the type of the imported scene element and create UNIGINE objects (nodes, meshes, lights, cameras, etc.). This is performed in overrides of the *[Importer::onImport*()](../../../api/library/common/import/class.importer_cpp.md#onImportLight_ImportProcessor_ImportLight_Light)* methods, i.e. for lights we'll have *MyImporter::onImportlight()* looking as follows: <details> <summary>MyImporter::onImportlights() | Close</summary> **MyImporter::onImportlight()** ```cpp LightPtr MyImporter::onImportLight(const ImportProcessorPtr &processor, const ImportLightPtr amp;import_light) { Log::message("\n onImportLight reporting... \n"); // trying to generate a Unigine light source using the ImportLight data LightPtr light = create_light(import_light); if (!light) { Log::error("MyImporter::onImportLight: can't create light.\n"); return nullptr; } // process light - save light data to the resulting *.node file processor->processLight(light, import_light); return light; } ``` </details> UNIGINE objects creation is implemented in the *MyImporter::create_*()* methods. For our lights, we'll have *create_light()* as follows: <details> <summary>MyImporter::create_light() | Close</summary> **MyImporter::create_light()** ```cpp LightPtr create_light(const ImportLightPtr &import_light) { using namespace Math; MyLight *my_light = static_cast<MyLight *>(import_light->getData()); // getting light parameters from the ImportLight structure String type = my_light->type; vec4 color = vec4(my_light->color); float intensity = my_light->intensity; // checking light source type and creating a corresponding light source if (type == "LIGHT_OMNI") { Log::message("\n FUNCTION: create_light() creating an OMNI light... \n"); LightOmniPtr light_omni = LightOmni::create(color, 100.0f); light_omni->setIntensity(intensity); light_omni->setShapeType(Light::SHAPE_RECTANGLE); return light_omni; } else if (type == "LIGHT_PROJ") { Log::message("\n FUNCTION: create_light() creating a PROJ light... \n"); return LightProj::create(color, 100.0f, 60.0f); } Log::error("create_light: unknown light type.\n"); return nullptr; } ``` </details>
5. Save generated UNIGINE objects to `*.node` and `*.mesh` files. This part is performed by the *[DefaultProcessor](../../../principles/import_system/index_cpp.md#importers_processors)*, so we do nothing here.


And there are a couple more things to consider for our importer - initialization and cleanup operations that are implemented in the constructor and destructor respectively. So, upon construction, we should set the default import parameters and add the necessary processors. While in the cleanup section, we should remove all added processors. In our case we have:


<details>
<summary>Initialization and Cleanup | Close</summary>

**Initialization and Cleanup**


```cpp
MyImporter::MyImporter()
{
	// setting up necessary import parameters
	setParameterInt("vertex_cache", 1);
	setParameterFloat("scale", 1.0f);

	// adding a custom pre-processor
	addPreProcessor("MyImportProcessor");
}

MyImporter::~MyImporter()
{
	// removing our custom pre-processor
	removePreProcessor("MyImportProcessor");

	// free memory
	for (MyLight *light : lights)
		delete light;
	for (MyCamera *camera : cameras)
		delete camera;
	for (MyMesh *mesh : meshes)
		delete mesh;
}

```

</details>


> **Notice:** These default values can be changed in your application when using the importer via the *[Importer::setParameter*()](../../../api/library/common/import/class.importer_cpp.md#setParameterInt_cstr_int_void)* methods.


So, here is the resulting code for our importer (*MyImporter*)


<details>
<summary>MyImporter.h | Close</summary>

**MyImporter.h**


```cpp
#pragma once

#include <UnigineImport.h>
#include <UnigineMesh.h>
#include <UnigineHashMap.h>
#include <UnigineXml.h>

struct MyCamera;
struct MyLight;
struct MyMesh;

// declaring our custom importer
class MyImporter : public Unigine::Importer
{
	using ImportScenePtr = Unigine::ImportScenePtr;
	using ImportProcessorPtr = Unigine::ImportProcessorPtr;
	using ImportMeshPtr = Unigine::ImportMeshPtr;
	using ImportLightPtr = Unigine::ImportLightPtr;
	using ImportCameraPtr = Unigine::ImportCameraPtr;
	using ImportNodePtr = Unigine::ImportNodePtr;

public:
	MyImporter();
	~MyImporter() override;

	// here we define file extensions to be exported by our plugin, let it be a single .myext
	UNIGINE_INLINE static Unigine::Vector<Unigine::String> getExtensions() { return{ "myext" }; }

protected:
	// overriding methods that we're going to use to import required scene components
	bool onInit(const ImportScenePtr &scene, const char *filepath) override;
	bool onImport(const char *output_path) override;
	bool onImportMesh(const ImportProcessorPtr &processor, const Unigine::MeshPtr &mesh, const ImportMeshPtr &import_mesh) override;
	Unigine::LightPtr onImportLight(const ImportProcessorPtr &processor, const ImportLightPtr &import_light) override;
	Unigine::PlayerPtr onImportCamera(const ImportProcessorPtr &processor, const ImportCameraPtr &import_camera) override;
	Unigine::NodePtr onImportNode(const ImportProcessorPtr &processor, const ImportNodePtr &import_node) override;

private:

	// method creating a new import scene, performing file format checks and parsing the input file
	// to fill the hierarchy of metadata structures
	bool import_scene(const ImportScenePtr &import_scene);

	// the methods below check required flags, perform necessary data preparations and
	// add components to the hierarchy of scene metada structures (import_scene)
	void process_node(const ImportScenePtr &import_scene, const ImportNodePtr &parent, Unigine::XmlPtr scene_node);
	void process_mesh(const ImportScenePtr &import_scene, const ImportNodePtr &node, MyMesh *my_mesh);
	void process_light(const ImportScenePtr &import_scene, const ImportNodePtr &node, MyLight *my_light);
	void process_camera(const ImportScenePtr &import_scene, const ImportNodePtr &node, MyCamera *my_camera);

private:
	float scale{ 1.0f }; // scale factor for the imported scene
	Unigine::XmlPtr my_scene; // initial xml scene structure
	Unigine::Vector<MyLight *> lights;
	Unigine::Vector<MyCamera *> cameras;
	Unigine::Vector<MyMesh *> meshes;

};

```

</details>


<details>
<summary>MyImporter.cpp | Close</summary>

**MyImporter.cpp**


```cpp
#include "MyImporter.h"
#include "MyImporterData.h"

#include <UnigineThread.h>
#include <UnigineFileSystem.h>
#include <UnigineMathLibGeometry.h>
#include <UnigineNodes.h>
#include <UnigineWorld.h>
#include <UnigineHashSet.h>
#include <UnigineMaterials.h>
#include <UnigineDir.h>
#include <UnigineSet.h>

using namespace Unigine;

// auxiliary functions creating UNIGINE objects
namespace
{

	bool create_mesh(const MeshPtr &mesh, const ImportMeshPtr &import_mesh, float scale);
	LightPtr create_light(const ImportLightPtr &import_light);
	PlayerPtr create_camera(const ImportCameraPtr &import_camera);

}

MyImporter::MyImporter()
{
	// setting up necessary import parameters
	setParameterInt("vertex_cache", 1);
	setParameterFloat("scale", 1.0f);

	// adding a custom pre-processor
	addPreProcessor("MyImportProcessor");
}

MyImporter::~MyImporter()
{
	// removing our custom pre-processor
	removePreProcessor("MyImportProcessor");

	// free memory
	for (MyLight *light : lights)
		delete light;
	for (MyCamera *camera : cameras)
		delete camera;
	for (MyMesh *mesh : meshes)
		delete mesh;
}

bool MyImporter::onInit(const ImportScenePtr &scene, const char *filepath)
{
	// getting all necessary import parameters and making necessary preparations for scene import
	scale = getParameterFloat("scale");

	String filesystem_filepath = FileSystem::getAbsolutePath(filepath);
	my_scene = Xml::create();
	my_scene->load(filesystem_filepath);

	Log::message("\n\nLAUNCHING IMPORTING PROCESS... \n");

	// parse input file and fill metadata structures
	return import_scene(scene);
}

bool MyImporter::onImport(const char *output_path)
{
	Log::message("\nOnImport() reporting... \n");

	ImportScenePtr scene = getScene();

	auto setup_processor = [this, output_path](ImportProcessorPtr proc) {
		proc->setOutputPath(output_path);
		proc->setImporter(getImporter());
	};

	// importing meshes
	if (ImportProcessorPtr proc = Import::createImportProcessor(getMeshesProcessor()))
	{
		setup_processor(proc);

		Unigine::MeshPtr mesh = Unigine::Mesh::create();

		int num_meshes = scene->getNumMeshes();
		for (int m = 0; m < num_meshes; ++m)
		{
			mesh->clear();
			importMesh(proc, mesh, scene->getMesh(m));
		}
	}

	// importing nodes
	if (ImportProcessorPtr proc = Import::createImportProcessor(getNodesProcessor()))
	{
		setup_processor(proc);

		int num_nodes = scene->getNumNodes();
		for (int n = 0; n < num_nodes; ++n)
		{
			ImportNodePtr node = scene->getNode(n);
			if (node->getParent() != nullptr)
				continue;

			NodePtr root_node = importNode(proc, node);
			setOutputFilepath(node->getFilepath());
			if (root_node)
				root_node.deleteForce();
		}
	}

	return true;
}

bool MyImporter::onImportMesh(const ImportProcessorPtr &processor, const MeshPtr &mesh, const ImportMeshPtr &import_mesh)
{
	Log::message("\n onImportMesh reporting... \n");

	// trying to generate a Unigine Mesh using the ImportMesh data
	if (!create_mesh(mesh, import_mesh, scale))
	{
		Log::error("MyImporter::onImportMesh: can't create mesh.\n");
		return false;
	}

	// checking vertex_cache parameter and optimizing cache if necessary
	if (getParameterInt("vertex_cache"))
		mesh->optimizeIndices(Unigine::Mesh::VERTEX_CACHE);

	// calling a default processor to save the mesh to a file
	return processor->processMesh(mesh, import_mesh);
}

PlayerPtr MyImporter::onImportCamera(const ImportProcessorPtr &processor, const ImportCameraPtr &import_camera)
{
	Log::message("\n onImportCamera reporting... \n");

	// trying to generate a Unigine player using the ImportCamera data
	PlayerPtr camera = create_camera(import_camera);
	if (!camera)
	{
		Log::error("MyImporter::onImportCamera: can't create camera.\n");
		return nullptr;
	}

	// process player
	processor->processCamera(camera, import_camera);
	return camera;
}

LightPtr MyImporter::onImportLight(const ImportProcessorPtr &processor, const ImportLightPtr &import_light)
{
	Log::message("\n onImportLight reporting... \n");
	// trying to generate a Unigine light source using the ImportLight data
	LightPtr light = create_light(import_light);
	if (!light)
	{
		Log::error("MyImporter::onImportLight: can't create light.\n");
		return nullptr;
	}

	// process light
	processor->processLight(light, import_light);
	return light;
}

NodePtr MyImporter::onImportNode(const ImportProcessorPtr &processor, const ImportNodePtr &import_node)
{
	Log::message("\n onImportNode reporting: importing %s node\n", import_node->getName());

	NodePtr node = convertNode(processor, import_node);
	processor->processNode(node, import_node);
	return node;
}

bool MyImporter::import_scene(const ImportScenePtr &import_scene)
{
	// performing necessary checks on file format
	String n = my_scene->getName();
	if (n != "scene")
	{
		Log::error("Scene loader: bad my_scene format\n");
		return 0;
	}

	// checking scene name
	String name = my_scene->getArg("name");
	if (name.empty())
	{
		Log::error("Scene loader: scene name can't be empty\n");
		return 0;
	}
	// parsing the input file and filling the ImportScene
	auto num_nodes = my_scene->getNumChildren();
	Log::message("Importing [%s] scene num_nodes = %d\n", name.get(), num_nodes);
	for (int i = 0; i < num_nodes; i++)
	{
		const XmlPtr child_xml = my_scene->getChild(i);
		const String &child_name = child_xml->getName();

		if (child_name == "node")
		{
			process_node(import_scene, nullptr, child_xml);
		}
		else
		{
			Log::error("Scene loader: unknown element \"%s\" in the \"%s\" scene\n",
				child_name.get(), name.get());
		}
	}

	return true;
}

void MyImporter::process_node(const ImportScenePtr &import_scene, const ImportNodePtr &parent, XmlPtr scene_node)
{
	ImportNodePtr node = import_scene->addNode(parent);
	node->setName(scene_node->getArg("name"));
	if (scene_node->getChild("transform"))
	{
		Math::dmat4 transform = scene_node->getChild("transform")->getDMat4Data();
		transform.m03 *= scale;
		transform.m13 *= scale;
		transform.m23 *= scale;
		node->setTransform(transform);
	}

	// processing node attributes
	XmlPtr attribute = scene_node->getChild("attribute");
	if (attribute)
	{
		String attr_type = attribute->getArg("type");
		if (attr_type == "light")
		{
			// creating and filling light metadata
			MyLight *light = new MyLight();
			lights.append(light);
			light->type = attribute->getChildData("light_type");
			light->color = attribute->getChild("color")->getVec4Data();
			light->intensity = attribute->getChild("intensity")->getFloatData();

			// processing light metadata and adding ImportLight to the scene
			process_light(import_scene, node, light);

			Log::message("Artribute light: named %s , type %s, color (%f, %f, %f, %f)\n",
				node->getName(), light->type.get(),
				light->color.x, light->color.y, light->color.z, light->color.w);
		}
		else if (attr_type == "camera")
		{
			// creating and filling camera metadata
			MyCamera *camera = new MyCamera();
			cameras.append(camera);

			camera->type = attribute->getChildData("player_type");
			camera->fov = attribute->getChild("fov")->getFloatData();
			camera->near_plane = attribute->getChild("near")->getFloatData();
			camera->far_plane = attribute->getChild("far")->getFloatData();
			camera->target = attribute->getChild("target")->getVec3Data();

			// processing camera metadata and adding ImportCamera to the scene
			process_camera(import_scene, node, camera);
			Log::message("Artribute camera: named %s , type %s, target (%f, %f, %f)\n",
				node->getName(), camera->type.get(),
				camera->target.x, camera->target.y, camera->target.z);
		}
		else if (attr_type == "mesh")
		{
			// creating and filling mesh metadata
			MyMesh *mesh = new MyMesh();
			meshes.append(mesh);

			int num_surfaces = attribute->getChild("surfaces")->getNumChildren();
			int num_vertices = attribute->getChild("vertices")->getNumChildren();

			Log::message("Artribute mesh: named %s , %d surfaces, %d vertices\n",
				node->getName(), num_surfaces, num_vertices);

			// getting all surfaces
			for (int i = 0; i < num_surfaces; ++i) {
				XmlPtr xml_surf = attribute->getChild("surfaces")->getChild(i);
				mesh->surfaces.append(xml_surf->getArg("name"));
				// filling polygons data
				mesh->polygons.append(
					Math::ivec3(i, xml_surf->getIntArg("offset"), xml_surf->getIntArg("size")));
				Log::message("\nSurface [%d] named: %s\n", i, mesh->surfaces[i].get());
			}
			// getting all vertices
			for (int i = 0; i < num_vertices; ++i)
			{
				mesh->vertices.append(attribute->getChild("vertices")->getChild(i)->getVec3Data());

				Log::message("Vertex [%d] coordinates:(%f, %f, %f)\n",
					i, mesh->vertices[i].x, mesh->vertices[i].y, mesh->vertices[i].z);
			}
			// getting all indices
			XmlPtr indices_xml = attribute->getChild("indices");
			int num_indices = indices_xml->getIntArg("num_indices");

			mesh->indices.resize(num_indices);
			indices_xml->getIntArrayData(mesh->indices.get(), num_indices);

			// processing mesh metadata and adding ImportMesh to the scene
			process_mesh(import_scene, node, mesh);
		}
	}

	// processing all node's children
	int num_children = scene_node->getNumChildren();
	for (int i = 0; i < num_children; ++i) {
		XmlPtr child = scene_node->getChild(i);
		const String &child_name = child->getName();
		if (child_name == "node")
			process_node(import_scene, node, child);
	}
}

void MyImporter::process_mesh(const ImportScenePtr amp;import_scene, const ImportNodePtr &node, sMyMesh *my_mesh)
{
	Log::message("\n FUNCTION: process_mesh() reporting... \n");
	if ((getFlags() & IMPORT_MESHES) == 0)
		return;

	ImportMeshPtr mesh = import_scene->addMesh(node);
	mesh->setName(node->getName());

	ImportGeometryPtr geometry = mesh->addGeometry();
	geometry->setData(my_mesh);

	//adding surfaces to the mesh
	for (int i = 0; i < my_mesh->surfaces.size(); i++)
	{
		ImportSurfacePtr s = geometry->addSurface();
		s->setName(my_mesh->surfaces[i]);
		s->setTargetSurface(geometry->getNumSurfaces() - 1);
	}
}

void MyImporter::process_light(const ImportScenePtr &import_scene, const ImportNodePtr &node, MyLight *my_light)
{
	Log::message("\n FUNCTION: process_light() reporting... \n");
	// checking if the light import flag is set
	if ((getFlags() & IMPORT_LIGHTS) == 0)
		return;

	// adding a light source to the scene and setting lignt source data
	ImportLightPtr light = import_scene->addLight(node);
	light->setData(my_light);
}

void MyImporter::process_camera(const ImportScenePtr &import_scene, const ImportNodePtr &node, MyCamera *my_camera)
{
	Log::message("\n FUNCTION: process_camera() reporting... \n");
	// checking if the camera import flag is set
	if ((getFlags() & IMPORT_CAMERAS) == 0)
		return;

	// adding a camera to the scene and setting camera data
	ImportCameraPtr camera = import_scene->addCamera(node);
	camera->setData(my_camera);
}

namespace
{
	// auxiliary data structures to store mesh geometry information
	struct SurfaceData
	{
		int index;
		ImportSurfacePtr surface;
		Unigine::Vector<int> cindices;
		Unigine::Vector<int> tindices;
	};

	struct GeometryData
	{
		Unigine::Math::vec3 *vertices;
		Unigine::Math::dmat4 transform;
	};

	bool create_surfaces(const MeshPtr &mesh, const Unigine::Vector<SurfaceData> &surfaces, const GeometryData &geometry_data, float scale)
	{

		Log::message("\n FUNCTION: create_surfaces() reporting... \n");
		using namespace Unigine;
		using namespace Unigine::Math;

		const dmat4 &transform = geometry_data.transform;
		const Unigine::Math::vec3 *vertices = geometry_data.vertices;

		mat3 rotation = mat3(transform);
		// creating mesh surfaces using metadata
		for (const SurfaceData &surface : surfaces)
		{
			if (surface.cindices.empty())
				continue;

			int s = surface.surface->getTargetSurface();
			while (s >= mesh->getNumSurfaces())
				mesh->addSurface();

			mesh->setSurfaceName(s, surface.surface->getName());

			for (int index : surface.cindices) {
				mesh->addVertex(vec3(transform * vec3(vertices[index])), s);
				Log::message("\n FUNCTION: create_surfaces() reporting: adding vertex[%d] with coords (%f, %f, %f)... \n",
					index, vertices[index].x, vertices[index].y, vertices[index].z);
			}
			// applying scale
			mesh->setSurfaceTransform(Math::scale(vec3(scale)), s);
		}

		return true;
	}

	bool create_geometry(const Unigine::MeshPtr &mesh, const ImportGeometryPtr &geometry, float scale)
	{
		Log::message("\n FUNCTION: create_geometry() REPORTING... \n");
		using namespace Unigine;
		using namespace Unigine::Math;

		MyMesh *my_mesh = static_cast<MyMesh *>(geometry->getData());

		const dmat4 &transform = geometry->getTransform();

		GeometryData geometry_data;
		geometry_data.vertices = &my_mesh->vertices[0];
		geometry_data.transform = transform;

		Unigine::Vector<SurfaceData> surfaces_data;

		for (int n_surf = 0; n_surf < my_mesh->surfaces.size(); n_surf++)
		{
			// adding cindices and tindices and calling create surfaces
			SurfaceData &surface = surfaces_data.append();
			surface.index = n_surf;
			surface.surface = geometry->getSurface(n_surf);

			int offset = my_mesh->polygons[n_surf].y;
			int size = my_mesh->polygons[n_surf].z;
			for (int i = 0; i < size; i++)
			{
				surface.cindices.append(my_mesh->indices[offset + i]);
				surface.tindices.append(my_mesh->indices[offset + i]);
			}
		}

		create_surfaces(mesh, surfaces_data, geometry_data, scale);
		return true;
	}

	bool create_mesh(const Unigine::MeshPtr &mesh, const ImportMeshPtr &import_mesh, float scale)
	{
		Log::message("\n FUNCTION: create_mesh() reporting... \n");
		int num_geometries = import_mesh->getNumGeometries();
		for (int i = 0; i < num_geometries; ++i)
			create_geometry(mesh, import_mesh->getGeometry(i), scale);

		int num_surfaces = mesh->getNumSurfaces();

		// creating mesh indices
		mesh->createIndices();

		for (int s = 0; s < num_surfaces; ++s)
		{
			if (!mesh->getNumTangents(s, 0))
				mesh->createTangents(s, 0);

			for (int t = 1; t < mesh->getNumSurfaceTargets(s); ++t)
				mesh->createTangents(s, t);
		}

		// creating mesh bounds
		mesh->createBounds();

		return true;
	}

	LightPtr create_light(const ImportLightPtr &import_light)
	{
		using namespace Math;

		MyLight *my_light = static_cast<MyLight *>(import_light->getData());

		// getting light parameters from the ImportLight structure
		String type = my_light->type;
		vec4 color = vec4(my_light->color);
		float intensity = my_light->intensity;

		// checking light source type and creating a corresponding light source
		if (type == "LIGHT_OMNI")
		{
			Log::message("\n FUNCTION: create_light() creating an OMNI light... \n");
			LightOmniPtr light_omni = LightOmni::create(color, 100.0f);
			light_omni->setIntensity(intensity);
			light_omni->setShapeType(Light::SHAPE_RECTANGLE);
			return light_omni;
		}
		else if (type == "LIGHT_PROJ")
		{
			Log::message("\n FUNCTION: create_light() creating a PROJ light... \n");
			return LightProj::create(color, 100.0f, 60.0f);
		}

		Log::error("create_light: unknown light type.\n");
		return nullptr;
	}

	PlayerPtr create_camera(const ImportCameraPtr &import_camera)
	{
		Log::message("\n FUNCTION: create_camera() reporting... \n");

		MyCamera *my_camera = static_cast<MyCamera *>(import_camera->getData());

		// getting camera parameters from the ImportCamera structure
		float fov = my_camera->fov;
		float znear = my_camera->near_plane;
		float zfar = my_camera->far_plane;

		PlayerDummyPtr player_dummy = PlayerDummy::create();
		player_dummy->setZNear(znear);
		player_dummy->setZFar(zfar);
		//player_dummy->worldLookAt((Math::Vec3)my_camera->target, Math::vec3_up);

		// setting player projection
		if (my_camera->type == "TYPE_ORTHOGONAL")
			player_dummy->setProjection(Math::ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar));

		if (my_camera->type == "TYPE_PERSPECTIVE")
			player_dummy->setFov(fov);

		return player_dummy;
	}

}

```

</details>


After we have implemented all the functionality, we [compile the plugin library](../../../code/cpp/plugin.md#step_2).


## Using a Plugin


Now that our library is ready, we should perform the following steps to use it in our project:


1. First, let us [create a new project](../../../sdk/projects/index_cpp.md#creation) named **MyProject** that will use our library. Let it be a simple project using C++.
2. Put the created plugin library module (a `*.dll` or `*.so` file) to the corresponding project's directory � `bin/plugins/<vendor_name>/<plugin_name>`. For more information about plugin naming and the paths to plugin folders, please refer to the [Creating C++ Plugin](../../../code/cpp/plugin.md#path_to_plugin_files) article. > **Notice:** Make sure your project's binary and plugin library have the **same precision and version**.
3. Put the file in your custom format (`my_scene.myext`) to the `data` folder of the project.
4. Provide plugin loading in one of the following ways:

  - Pass the plugin as a command-line argument `extern_plugin`. Once passed, it is written into the configuration file. ```bash MyProject.exe -extern_plugin MyImportPlugin ```
  - Specify the plugin directly in the configuration file (`data/configs/default.boot`, *extern_plugin* string).
  - Add and use the plugin in the project's **world logic** via *[Engine::addPlugin()](../../../api/library/engine/class.engine_cpp.md#addPlugin_const_char_ptr_bool)* (or via *Engine.addPlugin()* for C# projects).
  - Add and use the plugin in the **system logic**:

    - Add the plugin via *[Engine::addPlugin()](../../../api/library/engine/class.engine_cpp.md#addPlugin_const_char_ptr_bool)* and use it in the **world logic**. You cannot initialize the plugin in the system logic and call plugin functions from it at the same time.
    - Use the plugin in the system logic after initializing it via the command-line argument `extern_plugin`.
5. Use the plugin in the project. We will add some lines of code to the *init()* method of the world logic (the `AppWorldLogic.cpp` file) to demonstrate the idea. **When it's necessary to set up import parameters:** <details> <summary>AppWorldLogic.cpp | Close</summary> ```cpp #include "AppWorldLogic.h" #include <UnigineImport.h> #include <UnigineGame.h> using namespace Unigine; int AppWorldLogic::init() { NodePtr node0 = importCustom(); if (PlayerPtr player = Game::getPlayer()) { const Math::Vec3 position(5.8f, -1.5f, 3.0f); player->setWorldTransform( Math::inverse(Math::lookAt(position, Math::Vec3_zero, Math::vec3_up))); } return 1; } NodePtr AppWorldLogic::importCustom() { // string to store the path to the resulting .node file with our imported scene String filepath_node; // getting an importer for our file extension from the list of importers registered in the Import System ImporterPtr my_importer = Import::createImporterByFileName(DEFAULT_FILEPATH); // if such importer was found setting up necessary import options if (my_importer) { my_importer->setParameterInt("make_lights_white", 1);	// stripping off light color information my_importer->setParameterFloat("scale", 0.8f);			// setting scale my_importer->init(DEFAULT_FILEPATH, ~0);				// initializing the importer with default import flags IMPROT_LIGHTS, IMPORT_MESHES, IMPORT_CAMERAS, etc. // importing our scene to the output folder my_importer->import(DEFAULT_OUTPUT_PATH); // getting a path to resulting *.node file with our imported scene filepath_node = my_importer->getOutputFilepath(); } if (filepath_node.empty()) { Log::error("Scene import failure.\n"); return nullptr; } // reporting the result and adding a node reference to the world on success Log::message("Successfully imported your scene, now you can use: %s\n", filepath_node.get()); return NodeReference::create(filepath_node); } ``` </details> **To import with default settings:** <details> <summary>AppWorldLogic.cpp | Close</summary> ```cpp #include "AppWorldLogic.h" #include <UnigineImport.h> #include <UnigineGame.h> using namespace Unigine; int AppWorldLogic::init() { NodePtr node1 = importDefault(); if (PlayerPtr player = Game::getPlayer()) { const Math::Vec3 position(5.8f, -1.5f, 3.0f); player->setWorldTransform( Math::inverse(Math::lookAt(position, Math::Vec3_zero, Math::vec3_up))); } return 1; } NodePtr AppWorldLogic::importDefault() { // string to store the path to the resulting .node file with our imported scene String filepath_node; // importing our scene with default settings to the output folder and getting a path to resulting *.node file filepath_node = Import::doImport(DEFAULT_FILEPATH, DEFAULT_OUTPUT_PATH); if (filepath_node.empty()) { Log::error("Scene import failure.\n"); return nullptr; } // reporting the result and adding a node reference to the world on success Log::message("Successfully imported your scene, now you can use: %s\n", filepath_node.get()); return NodeReference::create(filepath_node); } ``` </details>


Now when we launch our project with the *MyImportPlugin* plugin loaded and the *MyProject* world opened, the scene is imported to the world, and the corresponding files are saved to the `MyProject/data/output_folder/` folder.
