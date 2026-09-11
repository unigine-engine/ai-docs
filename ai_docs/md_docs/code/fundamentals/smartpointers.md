# Working with Smart Pointers


## Some Basics


In UNIGINE instances of C++ API classes (such as: *Node, Mesh, Body, Image* and so on...) only store pointers to instances of internal C++ classes, they cannot be created and deleted via the standard *new/delete* operators. So they should be declared as **smart pointers** (*[Unigine::Ptr](../../api/library/common/class.ptr_cpp.md)*) that allow you to automatically manage their lifetime. UNIGINE has its own optimized memory allocator for faster and more efficient memory management. Each smart pointer stores a reference counter, i.e. how many smart pointers are pointing to the managed object. Reference counting is thread-safe, as modifying the counter is an atomic operation.


Not all methods of the Engine's internal C++ classes are exposed to the user, some of them are used by the Engine only. These are specific functions that either are used only for some internal purposes, or cannot be given to the user "as is". So, to filter out such methods an intermediate level, called **interface**, is used. This interface stores a pointer to the instance of the Engine's internal C++ class.


**To create an instance** of an internal class we should declare a smart pointer for it and call the *create()* method � class constructor � providing construction parameters if necessary.


```cpp
// instantiating an object of an internal class
<Class>Ptr instance = <Class>::create(<construction_parameters>);

```


## Lifetime


We can divide all objects into two groups based on the way their lifetime is managed:


- ***Ownership* objects** (*Image, Texture, Mesh, Tileset*, etc.) these objects are managed in accordance with reference counter: when the last smart pointer is destroyed, the counter goes to 0, and the managed object is then automatically deleted. In this case it is assumed that the object is no longer needed (the Engine doesn�t know anything about it, and the user has got no pointer to be able to use it) and, therefore, it is deleted. (e.g. such objects declared within a scope will be automatically deleted when leaving the scope). ```cpp // creating a new image ImagePtr img = Image::create(); // now two pointers point to our image (reference counter increment) ImagePtr img2 = img; // removing the image (as both pointers no longer point to it and reference counter is zero) img2 = img = nullptr; ``` <details> <summary>Complete list of Ownership Objects | close</summary> **Complete list of *Ownership* Objects:** | - *[AnimationBind](../../api/library/animations/timeline/class.animationbind_cpp.md)* - *[AnimationBindComponent](../../api/library/animations/timeline/class.animationbindcomponent_cpp.md)* - *[AnimationBindMaterial](../../api/library/animations/timeline/class.animationbindmaterial_cpp.md)* - *[AnimationBindNode](../../api/library/animations/timeline/class.animationbindnode_cpp.md)* - *[AnimationBindPropertyParameter](../../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md)* - *[AnimationBindRuntime](../../api/library/animations/timeline/class.animationbindruntime_cpp.md)* - *[AnimationChannel](../../api/library/animations/timeline/class.animationchannel_cpp.md)* - *[AnimationChannelBones](../../api/library/animations/timeline/class.animationchannelbones_cpp.md)* - *[AnimationChannelBool](../../api/library/animations/timeline/class.animationchannelbool_cpp.md)* - *[AnimationChannelDouble](../../api/library/animations/timeline/class.animationchanneldouble_cpp.md)* - *[AnimationChannelDVec2](../../api/library/animations/timeline/class.animationchanneldvec2_cpp.md)* - *[AnimationChannelDVec3](../../api/library/animations/timeline/class.animationchanneldvec3_cpp.md)* - *[AnimationChannelDVec4](../../api/library/animations/timeline/class.animationchanneldvec4_cpp.md)* - *[AnimationChannelEvent](../../api/library/animations/timeline/class.animationchannelevent_cpp.md)* - *[AnimationChannelEventState](../../api/library/animations/timeline/class.animationchanneleventstate_cpp.md)* - *[AnimationChannelFloat](../../api/library/animations/timeline/class.animationchannelfloat_cpp.md)* - *[AnimationChannelFVec2](../../api/library/animations/timeline/class.animationchannelfvec2_cpp.md)* - *[AnimationChannelFVec3](../../api/library/animations/timeline/class.animationchannelfvec3_cpp.md)* - *[AnimationChannelFVec4](../../api/library/animations/timeline/class.animationchannelfvec4_cpp.md)* - *[AnimationChannelInfo](../../api/library/animations/timeline/class.animationchannelinfo_cpp.md)* - *[AnimationChannelInt](../../api/library/animations/timeline/class.animationchannelint_cpp.md)* - *[AnimationChannelIVec2](../../api/library/animations/timeline/class.animationchannelivec2_cpp.md)* - *[AnimationChannelIVec3](../../api/library/animations/timeline/class.animationchannelivec3_cpp.md)* - *[AnimationChannelIVec4](../../api/library/animations/timeline/class.animationchannelivec4_cpp.md)* - *[AnimationChannelNode](../../api/library/animations/timeline/class.animationchannelnode_cpp.md)* - *[AnimationChannelQuat](../../api/library/animations/timeline/class.animationchannelquat_cpp.md)* - *[AnimationChannelScalar](../../api/library/animations/timeline/class.animationchannelscalar_cpp.md)* - *[AnimationChannelSkeletonAnimation](../../api/library/animations/timeline/class.animationchannelskeletonanimation_cpp.md)* - *[AnimationChannelSound](../../api/library/animations/timeline/class.animationchannelsound_cpp.md)* - *[AnimationChannelString](../../api/library/animations/timeline/class.animationchannelstring_cpp.md)* - *[AnimationChannelSubSequence](../../api/library/animations/timeline/class.animationchannelsubsequence_cpp.md)* - *[AnimationChannelUGUID](../../api/library/animations/timeline/class.animationchanneluguid_cpp.md)* - *[AnimationChannelVec2](../../api/library/animations/timeline/class.animationchannelvec2_cpp.md)* - *[AnimationChannelVec3](../../api/library/animations/timeline/class.animationchannelvec3_cpp.md)* - *[AnimationChannelVec4](../../api/library/animations/timeline/class.animationchannelvec4_cpp.md)* - *[AnimationCurve](../../api/library/animations/timeline/class.animationcurve_cpp.md)* - *[AnimationCurveBool](../../api/library/animations/timeline/class.animationcurvebool_cpp.md)* - *[AnimationCurveDouble](../../api/library/animations/timeline/class.animationcurvedouble_cpp.md)* - *[AnimationCurveFloat](../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)* - *[AnimationCurveInt](../../api/library/animations/timeline/class.animationcurveint_cpp.md)* - *[AnimationCurveQuat](../../api/library/animations/timeline/class.animationcurvequat_cpp.md)* - *[AnimationCurveScalar](../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)* - *[AnimationCurveString](../../api/library/animations/timeline/class.animationcurvestring_cpp.md)* - *[AnimationCurveUGUID](../../api/library/animations/timeline/class.animationcurveuguid_cpp.md)* - *[AnimationSequence](../../api/library/animations/timeline/class.animationsequence_cpp.md)* - *[AnimationSequencePlayer](../../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* - *[Blob](../../api/library/common/class.blob_cpp.md)* - *[Camera](../../api/library/rendering/class.camera_cpp.md)* - *[Curve2d](../../api/library/common/class.curve2d_cpp.md)* | - *[Dir](../../api/library/filesystem/class.dir_cpp.md)* - *[Ellipsoid](../../api/library/geodetics/class.ellipsoid_cpp.md)* - *[File](../../api/library/filesystem/class.file_cpp.md)* - *[GameIntersection](../../api/library/engine/class.gameintersection_cpp.md)* - *[Image](../../api/library/common/class.image_cpp.md)* - *[ImageConverter](../../api/library/common/class.imageconverter_cpp.md)* - *[ImportAnimation](../../api/library/common/import/class.importanimation_cpp.md)* - *[ImportCamera](../../api/library/common/import/class.importcamera_cpp.md)* - *[ImportGeometry](../../api/library/common/import/class.importgeometry_cpp.md)* - *[ImportLight](../../api/library/common/import/class.importlight_cpp.md)* - *[ImportMaterial](../../api/library/common/import/class.importmaterial_cpp.md)* - *[ImportMesh](../../api/library/common/import/class.importmesh_cpp.md)* - *[ImportMeshSkinned](../../api/library/common/import/class.importmeshskinned_cpp.md)* - *[ImportNode](../../api/library/common/import/class.importnode_cpp.md)* - *[ImportProcessor](../../api/library/common/import/class.importprocessor_cpp.md)* - *[ImportScene](../../api/library/common/import/class.importscene_cpp.md)* - *[ImportSkeleton](../../api/library/common/import/class.importskeleton_cpp.md)* - *[ImportSurface](../../api/library/common/import/class.importsurface_cpp.md)* - *[Importer](../../api/library/common/import/class.importer_cpp.md)* - *[InputEvent](../../api/library/controls/class.inputevent_cpp.md)* - *[InputEventJoyAxisMotion](../../api/library/controls/class.inputeventjoyaxismotion_cpp.md)* - *[InputEventJoyButton](../../api/library/controls/class.inputeventjoybutton_cpp.md)* - *[InputEventJoyDevice](../../api/library/controls/class.inputeventjoydevice_cpp.md)* - *[InputEventJoyPovMotion](../../api/library/controls/class.inputeventjoypovmotion_cpp.md)* - *[InputEventKeyboard](../../api/library/controls/class.inputeventkeyboard_cpp.md)* - *[InputEventMouseButton](../../api/library/controls/class.inputeventmousebutton_cpp.md)* - *[InputEventMouseMotion](../../api/library/controls/class.inputeventmousemotion_cpp.md)* - *[InputEventMouseWheel](../../api/library/controls/class.inputeventmousewheel_cpp.md)* - *[InputEventPadAxisMotion](../../api/library/controls/class.inputeventpadaxismotion_cpp.md)* - *[InputEventPadButton](../../api/library/controls/class.inputeventpadbutton_cpp.md)* - *[InputEventPadDevice](../../api/library/controls/class.inputeventpaddevice_cpp.md)* - *[InputEventPadTouchMotion](../../api/library/controls/class.inputeventpadtouchmotion_cpp.md)* - *[InputEventSystem](../../api/library/controls/class.inputeventsystem_cpp.md)* - *[InputEventText](../../api/library/controls/class.inputeventtext_cpp.md)* - *[InputEventTouch](../../api/library/controls/class.inputeventtouch_cpp.md)* - *[InputEventVRButton](../../api/library/controls/class.inputeventvrbutton_cpp.md)* - *[InputEventVRButtonTouch](../../api/library/controls/class.inputeventvrbuttontouch_cpp.md)* - *[InputEventVRDevice](../../api/library/controls/class.inputeventvrdevice_cpp.md)* - *[InputEventVRAxisMotion](../../api/library/controls/class.inputeventvraxismotion_cpp.md)* - *[Json](../../api/library/common/class.json_cpp.md)* - *[LandscapeFetch](../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)* - *[LandscapeImages](../../api/library/objects/landscape_terrain/class.landscapeimages_cpp.md)* - *[LandscapeMapFileCompression](../../api/library/objects/landscape_terrain/class.landscapemapfilecompression_cpp.md)* | - *[LandscapeMapFileCreator](../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_cpp.md)* - *[LandscapeMapFileSettings](../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_cpp.md)* - *[LandscapeTextures](../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)* - *[Mesh](../../api/library/rendering/class.mesh_cpp.md)* - *[MeshDynamic](../../api/library/rendering/class.meshdynamic_cpp.md)* - *[MeshRender](../../api/library/rendering/class.meshrender_cpp.md)* - *[MeshSkinned](../../api/library/rendering/class.meshskinned_cpp.md)* - *[MeshSkinnedAnimation](../../api/library/rendering/class.meshskinnedanimation_cpp.md)* - *[ObjectIntersection](../../api/library/objects/class.objectintersection_cpp.md)* - *[ObjectIntersectionNormal](../../api/library/objects/class.objectintersectionnormal_cpp.md)* - *[ObjectIntersectionTexCoord](../../api/library/objects/class.objectintersectiontexcoord_cpp.md)* - *[PackageUng](../../api/library/filesystem/class.packageung_cpp.md)* - *[Path](../../api/library/common/class.path_cpp.md)* - *[PathRouteIntersection](../../api/library/pathfinding/class.pathrouteintersection_cpp.md)* - *[PhysicsIntersection](../../api/library/physics/class.physicsintersection_cpp.md)* - *[PhysicsIntersectionNormal](../../api/library/physics/class.physicsintersectionnormal_cpp.md)* - *[RegExp](../../api/library/common/class.regexp_cpp.md)* - *[RenderTarget](../../api/library/rendering/class.rendertarget_cpp.md)* - *[ResourceExternalMemory](../../api/library/rendering/class.resourceexternalmemory_cpp.md)* - *[ResourceFence](../../api/library/rendering/class.resourcefence_cpp.md)* - *[Shader](../../api/library/rendering/class.shader_cpp.md)* - *[ShapeContact](../../api/library/physics/class.shapecontact_cpp.md)* - *[Skeleton](../../api/library/animations/skeletal/class.skeleton_cpp.md)* - *[SkeletonPoseDecomposed](../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)* - *[SkeletonPoseMatrix](../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)* - *[Socket](../../api/library/networking/class.socket_cpp.md)* - *[SSLSocket](../../api/library/networking/class.sslsocket_cpp.md)* - *[Stream](../../api/library/common/class.stream_cpp.md)* - *[StructuredBuffer](../../api/library/rendering/class.structuredbuffer_cpp.md)* - *[SystemDialog](../../api/library/engine/class.systemdialog_cpp.md)* - *[Texture](../../api/library/rendering/class.texture_cpp.md)* - *[TextureRamp](../../api/library/rendering/class.textureramp_cpp.md)* - *[TilesetFile](../../api/library/objects/class.tilesetfile_cpp.md)* - *[UlonArg](../../api/library/common/class.ulonarg_cpp.md)* - *[UlonNode](../../api/library/common/class.ulonnode_cpp.md)* - *[UlonValue](../../api/library/common/class.ulonvalue_cpp.md)* - *[Viewport](../../api/library/rendering/class.viewport_cpp.md)* - *[WindowEvent](../../api/library/gui/class.windowevent_cpp.md)* - *[WindowEventDpi](../../api/library/gui/class.windoweventdpi_cpp.md)* - *[WindowEventDrop](../../api/library/gui/class.windoweventdrop_cpp.md)* - *[WindowEventGeneric](../../api/library/gui/class.windoweventgeneric_cpp.md)* - *[WorldIntersection](../../api/library/worlds/class.worldintersection_cpp.md)* - *[WorldIntersectionNormal](../../api/library/worlds/class.worldintersectionnormal_cpp.md)* - *[WorldIntersectionTexCoord](../../api/library/worlds/class.worldintersectiontexcoord_cpp.md)* - *[Xml](../../api/library/common/class.xml_cpp.md)* | |---|---|---| </details>
- ***Non-Ownership* objects** (nodes, widgets, materials, properties, etc.) � these objects interact with the Engine and become managed by it since the moment of their creation (they are engaged in the main loop, can be retrieved by names, etc.). The **lifetime of these objects is not determined by the reference counter**, they provide the mechanism of weak references, so you can check whether an object was deleted or not. To delete such objects you should use *[deleteLater()](../../api/library/common/class.ptr_cpp.md#deleteLater_void)* or a corresponding manager's method (e.g.: *[Materials::removeMaterial()](../../api/library/rendering/class.materials_cpp.md#removeMaterial_UGUID_int_int_int)*). ```cpp NodePtr node; void somefunc1(){ // creating a new dummy node node = NodeDummy::create(); } void somefunc2(){ // checking whether the node exists if (node) Log::message("The node is alive\n"); // deleting the node node.deleteLater(); } ```


Instead of managing references for nodes manually, you can simply choose lifetime management policy for it:


- **World-managed** � in this case a node shall be deleted when the world is closed. This policy is used by default for each new node.
- **Engine-managed** � in this case the node shall be deleted automatically on Engine shutdown (can be used for nodes that should be kept when changing worlds).


> **Notice:** Lifetime of each node in the hierarchy is defined by its root (either parent or possessor). Setting lifetime management type for a child node different from the one set for the root has no effect.


## Upcasting and Downcasting


Sometimes (e.g. when we use *World::getNodeByName()*, etc. ) we get a *NodePtr* value, which is a pointer to the base class, but in order to perform operations with certain object (e.g. *ObjectMeshDynamicPtr*) we need to perform **downcasting** (i.e. convert from a pointer-to-base to a pointer-to-derived). The following methods were introduced:


- **static_ptr_cast** � static casting without any checks (in accordance with C++ semantics)
- **checked_ptr_cast** � downcasting with automatic type checking performed
- **dynamic_ptr_cast** � dynamic casting (in accordance with C++ semantics)


Sometimes you may also need to perform **upcasting** (i.e. convert from a pointer-to-derived to a pointer-to-base) this type of casting is performed automatically.


> **Notice:** Implicit type conversion for UNIGINE smart pointers is not allowed.


The code samples below demonstrate the points described above.


**Example 1**


```cpp
#include <UnigineEditor.h>
using namespace Unigine;
/* .. */

// find a pointer to node by a given name
NodePtr baseptr = World::getNodeByName("my_meshdynamic");

// cast a pointer-to-derived from pointer-to-base with automatic type checking
ObjectMeshDynamicPtr derivedptr = checked_ptr_cast<ObjectMeshDynamic>(baseptr);

// static cast: pointer-to-derived (File) from pointer-to-base (Stream)
if(stream->getType() == Stream::FILE)
    FilePtr file = static_ptr_cast<File>(stream);

// upcast to the pointer to the Object class which is a base class for ObjectMeshDynamic
ObjectPtr object = derivedptr;

// upcast to the pointer to the Node class which is a base class for all scene objects
NodePtr node = derivedptr;

```


## Deleting Objects


A smart pointer has the ***[clear()](../../api/library/common/class.ptr_cpp.md#clear_void)*** destructor intended for *[ownership](#ownership_object)* objects clearing the pointer and deleting the object only in case if the smart pointer calling this method is the last one pointing to the object (*interface*, in this case). This should be taken into account.


As for *[non-ownership](#non_ownership_object)* objects, they can be deleted via one of the following methods:


- ***[deleteLater()](../../api/library/common/class.ptr_cpp.md#deleteLater_void)*** � performs delayed deletion, in this case the object will be deleted during the next *[swap()](../../code/fundamentals/execution_sequence/main_loop.md)* stage of the main loop (rendering of the object ceases immediately, but it still exists in memory for a while, so you can get it from its parent, for example). This method simplifies object deletion from a secondary thread, so you can call it and forget about the details, letting the Engine take control over the process of deletion, which can be used for future optimizations;
- ***[deleteForce()](../../api/library/common/class.ptr_cpp.md#deleteForce_void)*** � performs immediate deletion, which might be necessary in some cases. Calling this method for main-loop-dependent objects (e.g., nodes) is safe only when performed from the Main thread.


Both these methods can be safely called more than once for a single object (as well as after an object has been deleted by the Engine) without causing a double deletion. So, no worries, call it whenever an object is no longer needed.


## See Also


- For more information on the methods of the *Ptr* class, see *[Ptr class](../../api/library/common/class.ptr_cpp.md)* page.
