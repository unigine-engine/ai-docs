# Unigine::Variable Class (CPP)

**Header:** #include <UnigineInterpreter.h>


Universal variable for functors.


## Variable Class

### Members

---

## Variable ( )

Default constructor.
## Variable ( const Variable & v )

Copy constructor.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( int v )

Explicit constructor for a variable of int type.
### Arguments

- *int* **v** - The value of the variable.

## explicit Variable ( long long v )

Explicit constructor for a variable of long long type.
### Arguments

- *long long* **v** - The value of the variable.

## explicit Variable ( float v )

Explicit constructor for a variable of float type.
### Arguments

- *float* **v** - The value of the variable.

## explicit Variable ( double v )

Explicit constructor for a variable of double type.
### Arguments

- *double* **v** - The value of the variable.

## explicit Variable ( const vec2 & v )

Explicit constructor for a variable of vec2 type.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const vec3 & v )

Explicit constructor for a variable of vec3 type.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const vec4 & v )

Explicit constructor for a variable of vec4 type.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const dvec2 & v )

Explicit constructor for a variable of dvec2 type.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const dvec3 & v )

Explicit constructor for a variable of dvec3 type.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const dvec4 & v )

Explicit constructor for a variable of dvec4 type.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const ivec2 & v )

Explicit constructor for a variable of ivec2 type.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const ivec3 & v )

Explicit constructor for a variable of ivec3 type.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const ivec4 & v )

Explicit constructor for a variable of ivec4 type.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v** - The value of the variable.

## explicit Variable ( const mat4 & m )

Explicit constructor for a variable of mat4 type.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the variable.

## explicit Variable ( const dmat4 & m )

Explicit constructor for a variable of dmat4 type.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the variable.

## explicit Variable ( const quat & q )

Explicit constructor for a variable of quad type.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - The value of the variable.

## explicit Variable ( const char * s )

Explicit constructor for a variable of string type.
### Arguments

- *const char ** **s** - The value of the variable.

## Variable ( void * interpreter , const char * type_name , void * object , int append , int manage )

External class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const char ** **type_name** - Name of the external class object type.
- *void ** **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Body Ptr & body , int append , int manage )

Body smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Body](../../../api/library/physics/class.body_cpp.md)Ptr &* **body** - Body smart pointer.
- *int* **append** - The script will take ownership of the Body and be responsible for deleting it.
- *int* **manage** - The script will manage the Body lifetime through reference counting.

## Variable ( void * interpreter , const Camera Ptr & camera , int append , int manage )

Camera smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Camera](../../../api/library/rendering/class.camera_cpp.md)Ptr &* **camera** - Camera smart pointer.
- *int* **append** - The script will take ownership of the camera and be responsible for deleting it.
- *int* **manage** - The script will manage the camera lifetime through reference counting.

## Variable ( void * interpreter , const Controls Ptr & controls , int append , int manage )

Controls smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Controls](../../../api/library/controls/class.controls_cpp.md)Ptr &* **controls** - Controls smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const DatasetPtr & dataset , int append , int manage )

Dataset smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const DatasetPtr &* **dataset** - Dataset smart pointer.
- *int* **append** - The script will take ownership of the Dataset and be responsible for deleting it.
- *int* **manage** - The script will manage the Dataset lifetime through reference counting.

## Variable ( void * interpreter , const Decal Ptr & decal , int append , int manage )

Decal smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Decal](../../../api/library/decals/class.decal_cpp.md)Ptr &* **decal** - Decal smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Ellipsoid Ptr & ellipsoid , int append , int manage )

Ellipsoid smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Ellipsoid](../../../api/library/geodetics/class.ellipsoid_cpp.md)Ptr &* **ellipsoid** - Ellipsoid smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Gui Ptr & gui , int append , int manage )

Gui smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Gui](../../../api/library/gui/class.gui_cpp.md)Ptr &* **gui** - Gui smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Image Ptr & image , int append , int manage )

Image smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Image](../../../api/library/common/class.image_cpp.md)Ptr &* **image** - Image smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Light Ptr & light , int append , int manage )

Light smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Light](../../../api/library/lights/class.light_cpp.md)Ptr &* **light** - Light smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Material Ptr & material , int append , int manage )

Material smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Material](../../../api/library/rendering/class.material_cpp.md)Ptr &* **material** - Material smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Mesh Ptr & mesh , int append , int manage )

Mesh smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Mesh](../../../api/library/rendering/class.mesh_cpp.md)Ptr &* **mesh** - Mesh smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Node Ptr & node , int append , int manage )

Node smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Node](../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Object Ptr & object , int append , int manage )

Object smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Object](../../../api/library/objects/class.object_cpp.md)Ptr &* **object** - Object smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Path Ptr & path , int append , int manage )

Path smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Path](../../../api/library/common/class.path_cpp.md)Ptr &* **path** - Path smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Player Ptr & player , int append , int manage )

Player smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Player](../../../api/library/players/class.player_cpp.md)Ptr &* **player** - Player smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Shape Ptr & shape , int append , int manage )

Shape smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Shape](../../../api/library/physics/class.shape_cpp.md)Ptr &* **shape** - Shape smart pointer.
- *int* **append** - The script will take ownership of the Shape and be responsible for deleting it.
- *int* **manage** - The script will manage the Shape lifetime through reference counting.

## Variable ( void * interpreter , const Stream Ptr & stream , int append , int manage )

Stream smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Stream](../../../api/library/common/class.stream_cpp.md)Ptr &* **stream** - Stream smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Property Ptr & property , int append , int manage )

Property smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Property](../../../api/library/common/class.property_cpp.md)Ptr &* **property** - Property smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const PropertyParameter Ptr & property_parameter , int append , int manage )

PropertyParameter smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [PropertyParameter](../../../api/library/common/class.propertyparameter_cpp.md)Ptr &* **property_parameter** - PropertyParameter smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const RenderEnvironmentPreset Ptr & preset , int append , int manage )

RenderEnvironmentPreset smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [RenderEnvironmentPreset](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md)Ptr &* **preset** - RenderEnvironmentPreset smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const TerrainGlobalDetail Ptr & detail , int append , int manage )

TerrainGlobalDetail smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalDetail](../../../api/library/objects/class.terrainglobaldetail_cpp.md)Ptr &* **detail** - TerrainGlobalDetail smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalDetail and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalDetail lifetime through reference counting.

## Variable ( void * interpreter , const TerrainGlobalLodHeight Ptr & lod , int append , int manage )

TerrainGlobalLodHeight smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalLodHeight](../../../api/library/objects/class.terraingloballodheight_cpp.md)Ptr &* **lod** - TerrainGlobalLodHeight smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalLodHeight and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalLodHeight lifetime through reference counting.

## Variable ( void * interpreter , const TerrainGlobalLod Ptr & lod , int append , int manage )

TerrainGlobalLod smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cpp.md)Ptr &* **lod** - TerrainGlobalLod smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalLod and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalLod lifetime through reference counting.

## Variable ( void * interpreter , const TerrainGlobalLods Ptr & lods , int append , int manage )

TerrainGlobalLods smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalLods](../../../api/library/objects/class.terraingloballods_cpp.md)Ptr &* **lods** - TerrainGlobalLods smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalLods and be responsible for deleting it.
- *int* **manage**

## Variable ( void * interpreter , const TypeInfo & type_info , void * object , int append , int manage )

External class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **type_info** - Type information.
- *void ** **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Widget Ptr & widget , int append , int manage )

Widget smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Widget](../../../api/library/gui/class.widget_cpp.md)Ptr &* **widget** - Widget smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( void * interpreter , const Xml Ptr & xml , int append , int manage )

XML smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Xml](../../../api/library/common/class.xml_cpp.md)Ptr &* **xml** - XML smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( const UGUID & g )

[UGUID](../../../api/library/filesystem/class.uguid_cpp.md) smart pointer class object constructor.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) smart pointer.

## Variable ( void * interpreter , const Joint Ptr & joint , int append , int manage )

[Joint](../../../api/library/physics/class.joint_cpp.md) smart pointer class object constructor.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Joint](../../../api/library/physics/class.joint_cpp.md)Ptr &* **joint** - Joint smart pointer.
- *int* **append** - The script will take ownership of the Joint and be responsible for deleting it.
- *int* **manage** - The script will manage the Joint lifetime through reference counting.

## void set ( const Variable & v )

Sets a variable.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the variable.

## const Variable & get ( ) const

Returns the current variable.
### Return value

The value of the variable.
## void setBody ( void * interpreter , const Body Ptr & body , int append , int manage )

Sets a Body smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Body](../../../api/library/physics/class.body_cpp.md)Ptr &* **body** - Body smart pointer.
- *int* **append** - The script will take ownership of the Body and be responsible for deleting it.
- *int* **manage** - The script will manage the Body lifetime through reference counting.

## const Body Ptr & getBody ( void * interpreter )

Returns the current variable as a Body smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Body smart pointer.
## int isBody ( void * interpreter )

Returns a value indicating if the variable is a Body.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a Body; otherwise, **0**.
## void setCamera ( void * interpreter , const Camera Ptr & camera , int append , int manage )

Sets a Camera smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Camera](../../../api/library/rendering/class.camera_cpp.md)Ptr &* **camera** - Camera smart pointer.
- *int* **append** - The script will take ownership of the Camera and be responsible for deleting it.
- *int* **manage** - The script will manage the Camera lifetime through reference counting.

## const Camera Ptr & getCamera ( void * interpreter )

Returns the current variable as a Camera smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Camera smart pointer.
## int isCamera ( void * interpreter )

Returns a value indicating if the variable is a Camera.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a Camera; otherwise, **0**.
## void setControls ( void * interpreter , const Controls Ptr & controls , int append , int manage )

Sets a controls smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Controls](../../../api/library/controls/class.controls_cpp.md)Ptr &* **controls** - Controls smart pointer.
- *int* **append** - The script will take ownership of the controls and be responsible for deleting it.
- *int* **manage** - The script will manage the controls lifetime through reference counting.

## const Controls Ptr & getControls ( void * interpreter ) const

Returns the current variable as a controls smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Controls smart pointer.
## int isControls ( void * interpreter ) const

Returns a value indicating if the variable is a controls.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a controls; otherwise, **0**.
## Variable::VariableData * getData ( )

## void setDataset ( void * interpreter , const DatasetPtr & dataset , int append , int manage )

Sets a Dataset smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const DatasetPtr &* **dataset** - Dataset smart pointer.
- *int* **append** - The script will take ownership of the Dataset and be responsible for deleting it.
- *int* **manage** - The script will manage the Dataset lifetime through reference counting.

## const DatasetPtr & getDataset ( void * interpreter )

Returns the current variable as a Dataset smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Dataset smart pointer.
## int isDataset ( void * interpreter )

Returns a value indicating if the variable is a Dataset.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a Dataset; otherwise, **0**.
## void setDecal ( void * interpreter , const Decal Ptr & decal , int append , int manage )

Sets a decal smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Decal](../../../api/library/decals/class.decal_cpp.md)Ptr &* **decal** - Decal smart pointer.
- *int* **append** - The script will take ownership of the decal and be responsible for deleting it.
- *int* **manage** - The script will manage the decal lifetime through reference counting.

## const Decal Ptr & getDecal ( void * interpreter ) const

Returns the current variable as a decal smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isDecal ( void * interpreter ) const

Returns a value indicating if the variable is a decal.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Returns **1** if the variable is a decal; otherwise, **0**.
## void setDVec2 ( const dvec2 & v )

Sets a two component vector for the variable.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the variable.

## const dvec2 & getDVec2 ( )

Returns the current variable as a two component vector, if possible.
### Return value

The value of the variable.
## int isDVec2 ( )

Returns a value indicating if the variable is a three component vector.
### Return value

**1** if the variable is a two component vector; otherwise, **0**.
## void setDVec3 ( const dvec3 & v )

Sets a three component vector for the variable.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the variable.

## const dvec3 & getDVec3 ( ) const

Returns the current variable as a three component vector, if possible.
### Return value

The value of the variable.
## int isDVec3 ( ) const

Returns a value indicating if the variable is a three component vector.
### Return value

**1** if the variable is a three component vector; otherwise, **0**.
## void setDVec4 ( const dvec4 & v )

Sets a four component vector for the variable.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the variable.

## const dvec4 & getDVec4 ( ) const

Returns the current variable as a four component vector, if possible.
### Return value

The value of the variable.
## int isDVec4 ( ) const

Returns a value indicating if the variable is a four component vector.
### Return value

Returns **1** if the variable is a four component vector; otherwise, **0**.
## void setEllipsoid ( void * interpreter , const Ellipsoid Ptr & ellipsoid , int append , int manage )

Sets a ellipsoid smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Ellipsoid](../../../api/library/geodetics/class.ellipsoid_cpp.md)Ptr &* **ellipsoid** - A smart pointer to Ellipsoid.
- *int* **append** - The script will take ownership of the ellipsoid and be responsible for deleting it.
- *int* **manage** - The script will manage the ellipsoid lifetime through reference counting.

## const Ellipsoid Ptr & getEllipsoid ( void * interpreter )

Returns the current variable as an ellipsoid smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

A smart pointer to Ellipsoid.
## int isEllipsoid ( void * interpreter )

Returns a value indicating if the variable is an ellipsoid.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is an ellipsoid; otherwise, **0**.
## int isExternClass ( ) const

Returns a value indicating if the variable belongs to the external class.
### Return value

1 is the variable belongs to the external class; otherwise, 0.
## void setExternClassObject ( void * interpreter , const char * type_name , void * object , int append , int manage )

Sets an external class object for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const char ** **type_name** - Name of the external class object type.
- *void ** **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## void setExternClassObject ( void * interpreter , const TypeInfo & type_info , void * object , int append , int manage )

Sets an external class object for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **type_info** - Type information.
- *void ** **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## void setExternClassObject ( void * interpreter , Type * object , int append , int manage )

Sets an external class object for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *Type ** **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## void * getExternClassObject ( void * interpreter , const TypeInfo & type_info ) const

Returns the external class object pointer.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **type_info** - Type information.

## Type * getExternClassObject ( void * interpreter ) const

Returns the type of the external class object.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Object type.
## int isExternClassObject ( void * interpreter ) const

Returns a value indicating if the object belongs to the external class.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

1 is the variable belongs to the external class; otherwise, 0.
## Type & getExternClassObjectRef ( void * interpreter ) const

Returns the type of the external class object stored in the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Object type.
## TypeInfo getExternClassType ( void * interpreter ) const

Returns type information about the external class object stored in the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Type information.
## void setGui ( void * interpreter , const Gui Ptr & gui , int append , int manage )

Sets a gui smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Gui](../../../api/library/gui/class.gui_cpp.md)Ptr &* **gui** - Gui smart pointer.
- *int* **append** - The script will take ownership of the gui data and be responsible for deleting it.
- *int* **manage** - The script will manage the gui data lifetime through reference counting.

## const Gui Ptr & getGui ( void * interpreter ) const

Returns the current variable as a gui smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isGui ( void * interpreter ) const

Returns a value indicating if the variable is a gui.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Returns **1** if the variable is a gui; otherwise, **0**.
## void setImage ( void * interpreter , const Image Ptr & image , int append , int manage )

Sets an image smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Image](../../../api/library/common/class.image_cpp.md)Ptr &* **image** - Image smart pointer.
- *int* **append** - The script will take ownership of the image and be responsible for deleting it.
- *int* **manage** - The script will manage the image lifetime through reference counting.

## const Image Ptr & getImage ( void * interpreter ) const

Returns the current variable as a image smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isImage ( void * interpreter ) const

Returns a value indicating if the variable is an image.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Returns **1** if the variable is an image; otherwise, **0**.
## void setJoint ( void * interpreter , const Joint Ptr & joint , int append , int manage )

Sets a [Joint](../../../api/library/physics/class.joint_cpp.md) smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Joint](../../../api/library/physics/class.joint_cpp.md)Ptr &* **joint** - [Joint](../../../api/library/physics/class.joint_cpp.md) smart pointer.
- *int* **append** - The script will take ownership of the Joint and be responsible for deleting it.
- *int* **manage** - The script will manage the Joint lifetime through reference counting.

## const Joint Ptr & getJoint ( void * interpreter )

Returns the current variable as a [Joint](../../../api/library/physics/class.joint_cpp.md) smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Joint smart pointer.
## int isJoint ( void * interpreter )

Returns a value indicating if the variable is a [Joint](../../../api/library/physics/class.joint_cpp.md).
### Arguments

- *void ** **interpreter**

### Return value

**1** if the variable is a Joint; otherwise, **0**.
## void setLight ( void * interpreter , const Light Ptr & light , int append , int manage )

Sets a light smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Light](../../../api/library/lights/class.light_cpp.md)Ptr &* **light** - Light smart pointer.
- *int* **append** - The script will take ownership of the light and be responsible for deleting it.
- *int* **manage** - The script will manage the light lifetime through reference counting.

## const Light Ptr & getLight ( void * interpreter ) const

Returns the current variable as a light smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isLight ( void * interpreter ) const

Returns a value indicating if the variable is a light.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a light; otherwise, **0**.
## void setLong ( long long v )

Sets a long long value for the variable.
### Arguments

- *long long* **v** - The value of the variable.

## long long getLong ( ) const

Returns the current variable as a long long value, if possible.
### Return value

The value of the variable.
## int isLong ( ) const

Returns a value indicating if the variable is a long long value.
### Return value

**1** if the variable is a long long value; otherwise, **0**.
## void setMaterial ( void * interpreter , const Material Ptr & material , int append , int manage )

Sets a material smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Material](../../../api/library/rendering/class.material_cpp.md)Ptr &* **material** - Material smart pointer.
- *int* **append** - The script will take ownership of the material and be responsible for deleting it.
- *int* **manage** - The script will manage the material lifetime through reference counting.

## const Material Ptr & getMaterial ( void * interpreter ) const

Returns the current variable as a material smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isMaterial ( void * interpreter ) const

Returns a value indicating if the variable is a material.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a material; otherwise, **0**.
## void setMesh ( void * interpreter , const Mesh Ptr & mesh , int append , int manage )

Sets a mesh smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Mesh](../../../api/library/rendering/class.mesh_cpp.md)Ptr &* **mesh** - Mesh smart pointer.
- *int* **append** - The script will take ownership of the mesh data and be responsible for deleting it.
- *int* **manage** - The script will manage the mesh data lifetime through reference counting.

## const Mesh Ptr & getMesh ( void * interpreter ) const

Returns the current variable as a mesh smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isMesh ( void * interpreter ) const

Returns a value indicating if the variable is a mesh.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a mesh; otherwise, **0**.
## void setNode ( void * interpreter , const Node Ptr & node , int append , int manage )

Sets a node smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Node](../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node smart pointer.
- *int* **append** - The script will take ownership of the node and be responsible for deleting it.
- *int* **manage** - The script will manage the node lifetime through reference counting.

## const Node Ptr & getNode ( void * interpreter ) const

Returns the current variable as a node smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isNode ( void * interpreter ) const

Returns a value indicating if the variable is a node.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Returns **1** if the variable is a node; otherwise, **0**.
## int isNull ( ) const

Returns a value indicating if the variable is a null value.
### Return value

**1** if the variable is a null value; otherwise, **0**.
## void setObject ( void * interpreter , const Object Ptr & object , int append , int manage )

Sets a object smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Object](../../../api/library/objects/class.object_cpp.md)Ptr &* **object** - Object smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## const Object Ptr & getObject ( void * interpreter ) const

Returns the current variable as an object smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isObject ( void * interpreter ) const

Returns a value indicating if the variable is an object.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is an object; otherwise, **0**.
## void setPath ( void * interpreter , const Path Ptr & path , int append , int manage )

Sets a path smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Path](../../../api/library/common/class.path_cpp.md)Ptr &* **path** - Path smart pointer.
- *int* **append** - The script will take ownership of the path data and be responsible for deleting it.
- *int* **manage** - The script will manage the path data lifetime through reference counting.

## const Path Ptr & getPath ( void * interpreter ) const

Returns the current variable as a path smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isPath ( void * interpreter ) const

Returns a value indicating if the variable is a path.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a path; otherwise, **0**.
## void setPlayer ( void * interpreter , const Player Ptr & player , int append , int manage )

Sets a player smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Player](../../../api/library/players/class.player_cpp.md)Ptr &* **player** - Player smart pointer.
- *int* **append** - The script will take ownership of the player and be responsible for deleting it.
- *int* **manage** - The script will manage the player lifetime through reference counting.

## const Player Ptr & getPlayer ( void * interpreter ) const

Returns the current variable as a player smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isPlayer ( void * interpreter ) const

Returns a value indicating if the variable is a player.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a player; otherwise, **0**.
## void setProperty ( void * interpreter , const Property Ptr & property , int append , int manage )

Sets a property smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Property](../../../api/library/common/class.property_cpp.md)Ptr &* **property** - Property smart pointer.
- *int* **append** - The script will take ownership of the property and be responsible for deleting it.
- *int* **manage** - The script will manage the property lifetime through reference counting.

## const Property Ptr & getProperty ( void * interpreter ) const

Returns the current variable as a property smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isProperty ( void * interpreter ) const

Returns a value indicating if the variable is a property.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a property; otherwise, **0**.
## void setPropertyParameter ( void * interpreter , const PropertyParameter Ptr & property_parameters , int append , int manage )

Sets a property parameter smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [PropertyParameter](../../../api/library/common/class.propertyparameter_cpp.md)Ptr &* **property_parameters** - PropertyParameter smart pointer.
- *int* **append** - The script will take ownership of the property parameter and be responsible for deleting it.
- *int* **manage** - The script will manage the property parameter lifetime through reference counting.

## const PropertyParameter Ptr & getPropertyParameter ( void * interpreter )

Returns the current variable as a property parameter smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isPropertyParameter ( void * interpreter )

Returns a value indicating if the variable is a property parameter.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a property parameter; otherwise, **0**.
## void setRenderEnvironmentPreset ( void * interpreter , const RenderEnvironmentPreset Ptr & preset , int append , int manage )

Sets a RenderEnvironmentPreset smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [RenderEnvironmentPreset](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md)Ptr &* **preset**
- *int* **append** - The script will take ownership of the RenderEnvironmentPreset and be responsible for deleting it.
- *int* **manage** - The script will manage the RenderEnvironmentPreset lifetime through reference counting.

## const RenderEnvironmentPreset Ptr & getRenderEnvironmentPreset ( void * interpreter )

Returns the current variable as a RenderEnvironmentPreset smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

RenderEnvironmentPreset smart pointer.
## int isRenderEnvironmentPreset ( void * interpreter )

Returns a value indicating if the variable is a RenderEnvironmentPreset.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a RenderEnvironmentPreset; otherwise, **0**.
## void setShape ( void * interpreter , const Shape Ptr & shape , int append , int manage )

Sets a Shape smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Shape](../../../api/library/physics/class.shape_cpp.md)Ptr &* **shape** - Shape smart pointer.
- *int* **append** - The script will take ownership of the Shape and be responsible for deleting it.
- *int* **manage** - The script will manage the Shape lifetime through reference counting.

## const Shape Ptr & getShape ( void * interpreter )

Returns the current variable as a Shape, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Shape smart pointer.
## int isShape ( void * interpreter )

Returns a value indicating if the variable is a Shape.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a Shape; otherwise, **0**.
## void setStream ( void * interpreter , const Stream Ptr & stream , int append , int manage )

Sets a stream smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Stream](../../../api/library/common/class.stream_cpp.md)Ptr &* **stream** - Stream smart pointer.
- *int* **append** - The script will take ownership of the stream data and be responsible for deleting it.
- *int* **manage** - The script will manage the stream data lifetime through reference counting.

## const Stream Ptr & getStream ( void * interpreter ) const

Returns the current variable as a stream smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isStream ( void * interpreter ) const

Returns a value indicating if the variable is a stream.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Returns **1** if the variable is a stream; otherwise, **0**.
## void setTerrainGlobalLod ( void * interpreter , const TerrainGlobalLod Ptr & lod , int append , int manage )

Sets a TerrainGlobalLod smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cpp.md)Ptr &* **lod** - TerrainGlobalLod smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalLod and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalLod lifetime through reference counting.

## const TerrainGlobalLod Ptr & getTerrainGlobalLod ( void * interpreter )

Returns the current variable as a TerrainGlobalLod smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

TerrainGlobalLod smart pointer.
## int isTerrainGlobalLod ( void * interpreter )

Returns a value indicating if the variable is a TerrainGlobalLod.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

1 if the variable is a TerrainGlobalLod; otherwise, 0.
## void setTerrainGlobalLods ( void * interpreter , const TerrainGlobalLods Ptr & lods , int append , int manage )

Sets a TerrainGlobalLods smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalLods](../../../api/library/objects/class.terraingloballods_cpp.md)Ptr &* **lods** - TerrainGlobalLods smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalLods and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalLods lifetime through reference counting.

## const TerrainGlobalLods Ptr & getTerrainGlobalLods ( void * interpreter )

Returns the current variable as a TerrainGlobalLods smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

TerrainGlobalLods smart pointer.
## int isTerrainGlobalLods ( void * interpreter )

Returns a value indicating if the variable is a TerrainGlobalLods.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

1 if the variable is a TerrainGlobalLods; otherwise, 0.
## void setTerrainGlobalLodHeight ( void * interpreter , const TerrainGlobalLodHeight Ptr & lod , int append , int manage )

Sets a TerrainGlobalLodHeight smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalLodHeight](../../../api/library/objects/class.terraingloballodheight_cpp.md)Ptr &* **lod** - TerrainGlobalLodHeight smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalLodHeight and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalLodHeight lifetime through reference counting.

## const TerrainGlobalLodHeight Ptr & getTerrainGlobalLodHeight ( void * interpreter )

Returns the current variable as a TerrainGlobalLodHeight smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

TerrainGlobalLodHeight smart pointer.
## int isTerrainGlobalLodHeight ( void * interpreter )

Returns a value indicating if the variable is a TerrainGlobalLodHeight.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

1 if the variable is a TerrainGlobalLodHeight; otherwise, 0.
## void setTerrainGlobalDetail ( void * interpreter , const TerrainGlobalDetail Ptr & detail , int append , int manage )

Sets a TerrainGlobalDetail smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [TerrainGlobalDetail](../../../api/library/objects/class.terrainglobaldetail_cpp.md)Ptr &* **detail** - TerrainGlobalDetail smart pointer.
- *int* **append** - The script will take ownership of the TerrainGlobalDetail and be responsible for deleting it.
- *int* **manage** - The script will manage the TerrainGlobalDetail lifetime through reference counting.

## const TerrainGlobalDetail Ptr & getTerrainGlobalDetail ( void * interpreter )

Returns the current variable as a TerrainGlobalDetail smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

TerrainGlobalDetail smart pointer.
## int isTerrainGlobalDetail ( void * interpreter )

Returns a value indicating if the variable is a TerrainGlobalDetail.
### Arguments

- *void ** **interpreter**

### Return value

1 if the variable is a TerrainGlobalDetail; otherwise, 0.
## int getType ( ) const

Returns the variable type.
### Return value

Variable type (see Unigine::Variable:: Enumeration).
## String getTypeInfo ( ) const

Returns the variable type info.
### Return value

Variable type info string.
## String getTypeName ( ) const

Returns the variable type name.
### Return value

Variable type name string.
## void setUserClass ( int type , int number , int instance )

Sets a user class for the variable.
### Arguments

- *int* **type** - User class type ID.
- *int* **number** - User class number.
- *int* **instance** - User class instance.

## int isUserClass ( ) const

Returns a value indicating if the variable is an user class.
### Return value

Returns **1** if the variable is an user class; otherwise, **0**.
## int getUserClassInstance ( ) const

Returns user class instance.
### Return value

User class instance.
## int getUserClassNumber ( ) const

Returns user class number.
### Return value

User class number.
## int getUserClassType ( ) const

Returns user class type.
### Return value

User class type ID.
## void setWidget ( void * interpreter , const Widget Ptr & widget , int append , int manage )

Sets a widget smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Widget](../../../api/library/gui/class.widget_cpp.md)Ptr &* **widget** - Widget smart pointer.
- *int* **append** - The script will take ownership of the widget and be responsible for deleting it.
- *int* **manage** - The script will manage the widget lifetime through reference counting.

## const Widget Ptr & getWidget ( void * interpreter ) const

Returns the current variable as a widget smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isWidget ( void * interpreter ) const

Returns a value indicating if the variable is a widget.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a widget; otherwise, **0**.
## void setXml ( void * interpreter , const Xml Ptr & xml , int append , int manage )

Sets a XML smart pointer for the variable.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Xml](../../../api/library/common/class.xml_cpp.md)Ptr &* **xml** - XML smart pointer.
- *int* **append** - The script will take ownership of the XML data and be responsible for deleting it.
- *int* **manage** - The script will manage the XML data lifetime through reference counting.

## const Xml Ptr & getXml ( void * interpreter ) const

Returns the current variable as a XML smart pointer, if possible.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int isXml ( void * interpreter ) const

Returns a value indicating if the variable is an XML.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

### Return value

Returns **1** if the variable is an XML; otherwise, **0**.
## void appendExternClass ( void * interpreter ) const

The script will take ownership of the object and be responsible for deleting it.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

## void manageExternClass ( void * interpreter ) const

The script will manage the object lifetime through reference counting.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

## int operator!= ( const Variable & v ) const

Variable not equal comparison.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator% ( const Variable & v ) const

Variable modulo operation.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator& ( const Variable & v ) const

Variable binary and.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator&& ( const Variable & v ) const

Variable logical and.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator* ( const Variable & v ) const

Variable multiplication.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator+ ( const Variable & v ) const

Variable addition.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator- ( const Variable & v ) const

Variable subtraction.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator/ ( const Variable & v ) const

Variable division.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator< ( const Variable & v ) const

Variable less than comparison.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator<< ( const Variable & v ) const

Variable binary left shift.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator<= ( const Variable & v ) const

Variable less than or equal to comparison.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable & operator= ( const Variable & v )

Assignment operator for the variable.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the variable.

## int operator== ( const Variable & v ) const

Variable equal comparison.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator> ( const Variable & v ) const

Variable greater than comparison.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator>= ( const Variable & v ) const

Variable greater than or equal to comparison.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator>> ( const Variable & v ) const

Variable binary right shift.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator^ ( const Variable & v ) const

Variable binary xor.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator| ( const Variable & v ) const

Variable binary or.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator|| ( const Variable & v ) const

Variable logical or.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - The value of the second variable.

### Return value

The resulting variable.
## void releaseExternClass ( void * interpreter ) const

The script will drop ownership of the object and clear all references to it.
### Arguments

- *void ** **interpreter** - Interpreter pointer.

## void removeExternClass ( void * interpreter ) const

The script will drop ownership of the object and be not responsible for deleting it.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
