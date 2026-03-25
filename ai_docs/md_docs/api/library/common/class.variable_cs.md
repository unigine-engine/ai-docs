# Unigine::Variable Class (CS)


Universal variable for functors.


## Variable Class

### Properties

## guid GUID

The [UGUID](../../../api/library/filesystem/class.uguid_cs.md) value.
## 🔒︎ bool IsGUID

The value indicating if the variable is a [UGUID](../../../api/library/filesystem/class.uguid_cs.md) value.
## int Int

The integer value.
## 🔒︎ bool IsInt

The value indicating if the variable is an integer value.
## double Double

The double value of the variable.
## 🔒︎ bool IsDouble

The value indicating if the variable is a double value.
## float Float

The float value of the variable.
## 🔒︎ bool IsFloat

The value indicating if the variable is a float value.
## string String

The string value of the variable.
## 🔒︎ bool IsString

The value indicating if the variable is a string value.
## vec2 Vec2

The two-component vector value of the variable.
## 🔒︎ bool IsVec2

The value indicating if the variable is a two-component vector.
## vec3 Vec3

The three-component vector value of the variable.
## 🔒︎ bool IsVec3

The value indicating if the variable is a three-component vector.
## vec4 Vec4

The four-component vector value of the variable.
## 🔒︎ bool IsVec4

The value indicating if the variable is a four-component vector.
## ivec2 IVec2

The two-component vector of integer values.
## 🔒︎ bool IsIVec2

The value indicating if the variable is a two-component vector of integer values.
## ivec3 IVec3

The three-component vector of integer values.
## 🔒︎ bool IsIVec3

The value indicating if the variable is a three-component vector of integer values.
## ivec4 IVec4

The four-component vector of integer values.
## 🔒︎ bool IsIVec4

The value indicating if the variable is a four-component vector of integer values.
## quat Quat

The quaternion value of the variable.
## 🔒︎ bool IsQuat

The value indicating if the variable is a quaternion.
## mat4 Mat4

The 4x4 matrix value of the variable.
## 🔒︎ bool IsMat4

The value indicating if the variable is a 4x4 matrix.
## dmat4 DMat4

The 3x4 matrix value of the variable.
## 🔒︎ bool IsDMat4

The value indicating if the variable is a 3x4 matrix.
### Members

---

## Variable ( )

Default constructor.
## Variable ( Variable v )

Copy constructor.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the variable.

## Variable ( int v )

Explicit constructor for a variable of int type.
### Arguments

- *int* **v** - The value of the variable.

## Variable ( long long v )

Explicit constructor for a variable of long long type.
### Arguments

- *long long* **v** - The value of the variable.

## Variable ( float v )

Explicit constructor for a variable of float type.
### Arguments

- *float* **v** - The value of the variable.

## Variable ( double v )

Explicit constructor for a variable of double type.
### Arguments

- *double* **v** - The value of the variable.

## Variable ( vec2 v )

Explicit constructor for a variable of vec2 type.
### Arguments

- *vec2* **v** - The value of the variable.

## Variable ( vec3 v )

Explicit constructor for a variable of vec3 type.
### Arguments

- *vec3* **v** - The value of the variable.

## Variable ( vec4 v )

Explicit constructor for a variable of vec4 type.
### Arguments

- *vec4* **v** - The value of the variable.

## Variable ( dvec2 v )

Explicit constructor for a variable of dvec2 type.
### Arguments

- *dvec2* **v** - The value of the variable.

## Variable ( dvec3 v )

Explicit constructor for a variable of dvec3 type.
### Arguments

- *dvec3* **v** - The value of the variable.

## Variable ( dvec4 v )

Explicit constructor for a variable of dvec4 type.
### Arguments

- *dvec4* **v** - The value of the variable.

## Variable ( ivec2 v )

Explicit constructor for a variable of ivec2 type.
### Arguments

- *ivec2* **v** - The value of the variable.

## Variable ( ivec3 v )

Explicit constructor for a variable of ivec3 type.
### Arguments

- *ivec3* **v** - The value of the variable.

## Variable ( ivec4 v )

Explicit constructor for a variable of ivec4 type.
### Arguments

- *ivec4* **v** - The value of the variable.

## Variable ( mat4 m )

Explicit constructor for a variable of mat4 type.
### Arguments

- *mat4* **m** - The value of the variable.

## Variable ( dmat4 m )

Explicit constructor for a variable of dmat4 type.
### Arguments

- *dmat4* **m** - The value of the variable.

## Variable ( quat q )

Explicit constructor for a variable of quad type.
### Arguments

- *quat* **q** - The value of the variable.

## Variable ( string s )

Explicit constructor for a variable of string type.
### Arguments

- *string* **s** - The value of the variable.

## Variable ( IntPtr interpreter , string type_name , IntPtr object , int append , int manage )

External class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *string* **type_name** - Name of the external class object type.
- *IntPtr* **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Controls controls , int append , int manage )

Controls smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Controls](../../../api/library/controls/class.controls_cs.md)* **controls** - Controls smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Decal decal , int append , int manage )

Decal smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Decal](../../../api/library/decals/class.decal_cs.md)* **decal** - Decal smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Gui gui , int append , int manage )

Gui smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - Gui smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Image image , int append , int manage )

Image smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Light light , int append , int manage )

Light smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Light](../../../api/library/lights/class.light_cs.md)* **light** - Light smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Material material , int append , int manage )

Material smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Mesh mesh , int append , int manage )

Mesh smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Node node , int append , int manage )

Node smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Object object , int append , int manage )

Object smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Path path , int append , int manage )

Path smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Path](../../../api/library/common/class.path_cs.md)* **path** - Path smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Player player , int append , int manage )

Player smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Player](../../../api/library/players/class.player_cs.md)* **player** - Player smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Stream stream , int append , int manage )

Stream smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Property property , int append , int manage )

Property smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , TypeInfo type_info , IntPtr object , int append , int manage )

External class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *TypeInfo* **type_info** - Type information.
- *IntPtr* **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Widget widget , int append , int manage )

Widget smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Widget smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Variable ( IntPtr interpreter , Xml xml , int append , int manage )

XML smart pointer class object constructor.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - XML smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## void SetBody ( IntPtr interpreter , Body body , int append , int manage )

Sets a Body smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body smart pointer.
- *int* **append** - The script will take ownership of the Body and be responsible for deleting it.
- *int* **manage** - The script will manage the Body lifetime through reference counting.

## Body GetBody ( IntPtr interpreter )

Returns the current variable as a Body smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Body smart pointer.
## void SetCamera ( IntPtr interpreter , Camera camera , int append , int manage )

Sets a Camera smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera smart pointer.
- *int* **append** - The script will take ownership of the Camera and be responsible for deleting it.
- *int* **manage** - The script will manage the Camera lifetime through reference counting.

## Camera GetCamera ( IntPtr interpreter )

Returns the current variable as a Camera smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Camera smart pointer.
## void SetControls ( IntPtr interpreter , Controls controls , int append , int manage )

Sets a controls smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Controls](../../../api/library/controls/class.controls_cs.md)* **controls** - Controls smart pointer.
- *int* **append** - The script will take ownership of the controls and be responsible for deleting it.
- *int* **manage** - The script will manage the controls lifetime through reference counting.

## Controls GetControls ( IntPtr interpreter )

Returns the current variable as a controls smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Controls smart pointer.
## void SetDataset ( IntPtr interpreter , Dataset dataset , int append , int manage )

Sets a Dataset smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *Dataset* **dataset** - Dataset smart pointer.
- *int* **append** - The script will take ownership of the Dataset and be responsible for deleting it.
- *int* **manage** - The script will manage the Dataset lifetime through reference counting.

## Dataset GetDataset ( IntPtr interpreter )

Returns the current variable as a Dataset smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Dataset smart pointer.
## void SetDecal ( IntPtr interpreter , Decal decal , int append , int manage )

Sets a decal smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Decal](../../../api/library/decals/class.decal_cs.md)* **decal** - Decal smart pointer.
- *int* **append** - The script will take ownership of the decal and be responsible for deleting it.
- *int* **manage** - The script will manage the decal lifetime through reference counting.

## Decal GetDecal ( IntPtr interpreter )

Returns the current variable as a decal smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetEllipsoid ( IntPtr interpreter , Ellipsoid ellipsoid , int append , int manage )

Sets a ellipsoid smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Ellipsoid](../../../api/library/geodetics/class.ellipsoid_cs.md)* **ellipsoid** - A smart pointer to Ellipsoid.
- *int* **append** - The script will take ownership of the ellipsoid and be responsible for deleting it.
- *int* **manage** - The script will manage the ellipsoid lifetime through reference counting.

## Ellipsoid GetEllipsoid ( IntPtr interpreter )

Returns the current variable as an ellipsoid smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

A smart pointer to Ellipsoid.
## void SetExternClassObject ( IntPtr interpreter , string type_name , IntPtr object , int append , int manage )

Sets an external class object for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *string* **type_name** - Name of the external class object type.
- *IntPtr* **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## void SetExternClassObject ( IntPtr interpreter , TypeInfo type_info , IntPtr object , int append , int manage )

Sets an external class object for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *TypeInfo* **type_info** - Type information.
- *IntPtr* **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## void SetExternClassObject ( IntPtr interpreter , Type * object , int append , int manage )

Sets an external class object for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *Type ** **object** - Pointer to the object.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## IntPtr GetExternClassObject ( IntPtr interpreter , TypeInfo type_info )

Returns the external class object pointer.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *TypeInfo* **type_info** - Type information.

## Type * GetExternClassObject ( IntPtr interpreter )

Returns the type of the external class object.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Object type.
## TypeInfo GetExternClassType ( IntPtr interpreter )

Returns type information about the external class object stored in the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Type information.
## void SetGui ( IntPtr interpreter , Gui gui , int append , int manage )

Sets a gui smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - Gui smart pointer.
- *int* **append** - The script will take ownership of the gui data and be responsible for deleting it.
- *int* **manage** - The script will manage the gui data lifetime through reference counting.

## Gui GetGui ( IntPtr interpreter )

Returns the current variable as a gui smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetImage ( IntPtr interpreter , Image image , int append , int manage )

Sets an image smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image smart pointer.
- *int* **append** - The script will take ownership of the image and be responsible for deleting it.
- *int* **manage** - The script will manage the image lifetime through reference counting.

## Image GetImage ( IntPtr interpreter )

Returns the current variable as a image smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetLight ( IntPtr interpreter , Light light , int append , int manage )

Sets a light smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Light](../../../api/library/lights/class.light_cs.md)* **light** - Light smart pointer.
- *int* **append** - The script will take ownership of the light and be responsible for deleting it.
- *int* **manage** - The script will manage the light lifetime through reference counting.

## Light GetLight ( IntPtr interpreter )

Returns the current variable as a light smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetMaterial ( IntPtr interpreter , Material material , int append , int manage )

Sets a material smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.
- *int* **append** - The script will take ownership of the material and be responsible for deleting it.
- *int* **manage** - The script will manage the material lifetime through reference counting.

## Material GetMaterial ( IntPtr interpreter )

Returns the current variable as a material smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetMesh ( IntPtr interpreter , Mesh mesh , int append , int manage )

Sets a mesh smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh smart pointer.
- *int* **append** - The script will take ownership of the mesh data and be responsible for deleting it.
- *int* **manage** - The script will manage the mesh data lifetime through reference counting.

## Mesh GetMesh ( IntPtr interpreter )

Returns the current variable as a mesh smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetNode ( IntPtr interpreter , Node node , int append , int manage )

Sets a node smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node smart pointer.
- *int* **append** - The script will take ownership of the node and be responsible for deleting it.
- *int* **manage** - The script will manage the node lifetime through reference counting.

## Node GetNode ( IntPtr interpreter )

Returns the current variable as a node smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetObject ( IntPtr interpreter , Object object , int append , int manage )

Sets a object smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object smart pointer.
- *int* **append** - The script will take ownership of the object and be responsible for deleting it.
- *int* **manage** - The script will manage the object lifetime through reference counting.

## Object GetObject ( IntPtr interpreter )

Returns the current variable as an object smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetPath ( IntPtr interpreter , Path path , int append , int manage )

Sets a path smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Path](../../../api/library/common/class.path_cs.md)* **path** - Path smart pointer.
- *int* **append** - The script will take ownership of the path data and be responsible for deleting it.
- *int* **manage** - The script will manage the path data lifetime through reference counting.

## Path GetPath ( IntPtr interpreter )

Returns the current variable as a path smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetPlayer ( IntPtr interpreter , Player player , int append , int manage )

Sets a player smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Player](../../../api/library/players/class.player_cs.md)* **player** - Player smart pointer.
- *int* **append** - The script will take ownership of the player and be responsible for deleting it.
- *int* **manage** - The script will manage the player lifetime through reference counting.

## Player GetPlayer ( IntPtr interpreter )

Returns the current variable as a player smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetProperty ( IntPtr interpreter , Property property , int append , int manage )

Sets a property smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property smart pointer.
- *int* **append** - The script will take ownership of the property and be responsible for deleting it.
- *int* **manage** - The script will manage the property lifetime through reference counting.

## Property GetProperty ( IntPtr interpreter )

Returns the current variable as a property smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetShape ( IntPtr interpreter , Shape shape , int append , int manage )

Sets a Shape smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - Shape smart pointer.
- *int* **append** - The script will take ownership of the Shape and be responsible for deleting it.
- *int* **manage** - The script will manage the Shape lifetime through reference counting.

## Shape GetShape ( IntPtr interpreter )

Returns the current variable as a Shape, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

Shape smart pointer.
## int IsShape ( IntPtr interpreter )

Returns a value indicating if the variable is a Shape.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

**1** if the variable is a Shape; otherwise, **0**.
## void SetStream ( IntPtr interpreter , Stream stream , int append , int manage )

Sets a stream smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.
- *int* **append** - The script will take ownership of the stream data and be responsible for deleting it.
- *int* **manage** - The script will manage the stream data lifetime through reference counting.

## Stream GetStream ( IntPtr interpreter )

Returns the current variable as a stream smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## int GetType ( )

Returns the variable type.
### Return value

Variable type (see Unigine::Variable:: Enumeration).
## void SetUserClass ( int type , int number , int instance )

Sets a user class for the variable.
### Arguments

- *int* **type** - User class type ID.
- *int* **number** - User class number.
- *int* **instance** - User class instance.

## void SetWidget ( IntPtr interpreter , Widget widget , int append , int manage )

Sets a widget smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Widget smart pointer.
- *int* **append** - The script will take ownership of the widget and be responsible for deleting it.
- *int* **manage** - The script will manage the widget lifetime through reference counting.

## Widget GetWidget ( IntPtr interpreter )

Returns the current variable as a widget smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void SetXml ( IntPtr interpreter , Xml xml , int append , int manage )

Sets a XML smart pointer for the variable.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - XML smart pointer.
- *int* **append** - The script will take ownership of the XML data and be responsible for deleting it.
- *int* **manage** - The script will manage the XML data lifetime through reference counting.

## Xml GetXml ( IntPtr interpreter )

Returns the current variable as a XML smart pointer, if possible.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

### Return value

The value of the variable.
## void AppendExternClass ( IntPtr interpreter )

The script will take ownership of the object and be responsible for deleting it.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

## void ManageExternClass ( IntPtr interpreter )

The script will manage the object lifetime through reference counting.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

## int operator!= ( Variable v )

Variable not equal comparison.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator% ( Variable v )

Variable modulo operation.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator& ( Variable v )

Variable binary and.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator&& ( Variable v )

Variable logical and.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator* ( Variable v )

Variable multiplication.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator+ ( Variable v )

Variable addition.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator- ( Variable v )

Variable subtraction.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator/ ( Variable v )

Variable division.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator< ( Variable v )

Variable less than comparison.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator<< ( Variable v )

Variable binary left shift.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator<= ( Variable v )

Variable less than or equal to comparison.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable & operator= ( Variable v )

Assignment operator for the variable.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the variable.

## int operator== ( Variable v )

Variable equal comparison.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator> ( Variable v )

Variable greater than comparison.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator>= ( Variable v )

Variable greater than or equal to comparison.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator>> ( Variable v )

Variable binary right shift.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator^ ( Variable v )

Variable binary xor.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## Variable operator| ( Variable v )

Variable binary or.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## int operator|| ( Variable v )

Variable logical or.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - The value of the second variable.

### Return value

The resulting variable.
## void releaseExternClass ( IntPtr interpreter )

The script will drop ownership of the object and clear all references to it.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.

## void removeExternClass ( IntPtr interpreter )

The script will drop ownership of the object and be not responsible for deleting it.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
