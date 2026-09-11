# Usage


Unigine supports two types of coordinate precision:


- [Single precision](#single_precision) coordinates
- [Double precision](#double_precision) coordinates


You can create and use all data types for your custom functions no matter what engine build is used. But script functions that deal with coordinates will take and return only the definite type of arguments. See [below](#support_both) how to support both single and double precision at the same time.


> **Notice:** The only function that can cause data loss when using a single-precision build is:
> - [Save world](../../code/console/index.md#world_save)
>
> If used, coordinates of saved nodes will be rewritten by single-precision floating-point data.


### Single precision coordinates


Single precision coordinates are suitable for not very large worlds where all meshes are positioned relatively close to the zero of coordinates. Depending on the size of meshes (small objects are more prone to precision artifacts) single precision allows to render worlds up to 10-20 thousands units from the center.
 In case of single coordinates precision, script functions that deal with coordinates take and return the following arguments (see the list of functions [below](#function_diffs)):


- [float](../../code/uniginescript/language/data_types.md#float)
- [vec3](../../code/uniginescript/language/data_types.md#vec3)
- [vec4](../../code/uniginescript/language/data_types.md#vec4)
- [mat4](../../code/uniginescript/language/data_types.md#mat4)


### Double precision coordinates


Double precision coordinates allows to create large worlds without any imprecision artifacts or jittering due to big distance from the center of coordinates. The created worlds can be virtually limitless. However, it is more costly from performance point of view.
 In case of double coordinates precision, script functions that deal with coordinates in most cases take and return arguments that can hold bigger values:


- [double](../../code/uniginescript/language/data_types.md#double)
- [dvec3](../../code/uniginescript/language/data_types.md#dvec3)
- [dvec4](../../code/uniginescript/language/data_types.md#dvec4)
- [dmat4](../../code/uniginescript/language/data_types.md#dmat4)


## How to Use Double Precision Coordinates


1. By default, all provided UNIGINE Engine libraries use single precision coordinates. To use double precision, you need to copy all necessary libraries from `<UnigineSDK>/lib/double_precision/` folder into `<UnigineSDK>/lib/`. To check what build is used, see **Features** line in the console or in the log file (look for **Double** in the list).
2. Replace arguments for functions that deal with coordinates (see [below](#function_diffs)) with double precision data types or special data types to support both variants of precision (see [below](#support_both)). > **Notice:** In case of using special **Scalar**, **Vec3**, etc. data types, include `core/unigine.h` header in your scripts. > ```cpp > #include <core/unigine.h> > ```


## How to Manage Your Code to Support Both Single and Double Precision


If you want your code to support both single and double precision builds, use the following data types that start with the capital letter. The engine will automatically substitute these types with appropriate ones in runtime, without having to handle it manually in code.


- **Scalar** for either *float* (single precision) or *double* (double precision)
- **Vec3** for either *vec3* or *dvec3*
- **Vec4** for either *vec4* or *dvec4*
- **Mat4** for either *mat4* or *dmat4*


## Functions Argument Differences


Here is a list of functions that take and return different types of arguments depending on the run build. Functions listed above the line correspond to single precision build, while the bottom ones are used in the double precision build.


```bash
Object engine.world.getIntersection(vec3,vec3,int,int);
Object engine.world.getIntersection(vec3,vec3,int,int,int);
---
Object engine.world.getIntersection(dvec3,dvec3,int,int);
Object engine.world.getIntersection(dvec3,dvec3,int,int,int);

Node engine.editor.getIntersection(vec3,vec3,int);
Node engine.editor.getIntersection(vec3,vec3,int,int);
---
Node engine.editor.getIntersection(dvec3,dvec3,int);
Node engine.editor.getIntersection(dvec3,dvec3,int,int);

void engine.visualizer.setModelview(mat4);
mat4 engine.visualizer.getModelview();
float engine.visualizer.getScale(vec3);
---
void engine.visualizer.setModelview(dmat4);
dmat4 engine.visualizer.getModelview();
float engine.visualizer.getScale(dvec3);

void engine.visualizer.renderPoint3D(vec3,float,vec4);
---
void engine.visualizer.renderPoint3D(dvec3,float,vec4);

void engine.visualizer.renderLine3D(vec3,vec3,vec4);
---
void engine.visualizer.renderLine3D(dvec3,dvec3,vec4);

void engine.visualizer.renderTriangle3D(vec3,vec3,vec3,vec4);
---
void engine.visualizer.renderTriangle3D(dvec3,dvec3,dvec3,vec4);

void engine.visualizer.renderQuad3D(vec3,vec3,vec3,vec3,vec4);
void engine.visualizer.renderVector(vec3,vec3,vec4);
void engine.visualizer.renderDirection(vec3,vec3,vec4);
void engine.visualizer.renderBox(vec3,mat4,vec4);
void engine.visualizer.renderFrustum(mat4,mat4,vec4);
void engine.visualizer.renderCircle(float,mat4,vec4);
void engine.visualizer.renderSector(float,float,mat4,vec4);
void engine.visualizer.renderCone(float,float,mat4,vec4);
void engine.visualizer.renderSphere(float,mat4,vec4);
void engine.visualizer.renderCapsule(float,float,mat4,vec4);
void engine.visualizer.renderCylinder(float,float,mat4,vec4);
void engine.visualizer.renderEllipsoid(vec3,mat4,vec4);
void engine.visualizer.renderSolidBox(vec3,mat4,vec4);
void engine.visualizer.renderSolidSphere(float,mat4,vec4);
void engine.visualizer.renderSolidCapsule(float,float,mat4,vec4);
void engine.visualizer.renderSolidCylinder(float,float,mat4,vec4);
void engine.visualizer.renderBoundBox(vec3,vec3,mat4,vec4);
void engine.visualizer.renderBoundSphere(vec3,float,mat4,vec4);
---
void engine.visualizer.renderQuad3D(dvec3,dvec3,dvec3,dvec3,vec4);
void engine.visualizer.renderVector(dvec3,dvec3,vec4);
void engine.visualizer.renderDirection(dvec3,vec3,vec4);
void engine.visualizer.renderBox(vec3,dmat4,vec4);
void engine.visualizer.renderFrustum(mat4,dmat4,vec4);
void engine.visualizer.renderCircle(float,dmat4,vec4);
void engine.visualizer.renderSector(float,float,dmat4,vec4);
void engine.visualizer.renderCone(float,float,dmat4,vec4);
void engine.visualizer.renderSphere(float,dmat4,vec4);
void engine.visualizer.renderCapsule(float,float,dmat4,vec4);
void engine.visualizer.renderCylinder(float,float,dmat4,vec4);
void engine.visualizer.renderEllipsoid(vec3,dmat4,vec4);
void engine.visualizer.renderSolidBox(vec3,dmat4,vec4);
void engine.visualizer.renderSolidSphere(float,dmat4,vec4);
void engine.visualizer.renderSolidCapsule(float,float,dmat4,vec4);
void engine.visualizer.renderSolidCylinder(float,float,dmat4,vec4);
void engine.visualizer.renderBoundBox(vec3,vec3,dmat4,vec4);
void engine.visualizer.renderBoundSphere(vec3,float,dmat4,vec4);

void engine.visualizer.renderMessage3D(vec3,string,vec4,int);
---
void engine.visualizer.renderMessage3D(dvec3,string,vec4,int);

Obstacle engine.game.getIntersection(vec3,vec3,float,int,int);
Obstacle engine.game.getIntersection(vec3,vec3,float,int,int,int);
---
Obstacle engine.game.getIntersection(dvec3,dvec3,float,int,int);
Obstacle engine.game.getIntersection(dvec3,dvec3,float,int,int,int);

Object engine.physics.getIntersection(vec3,vec3,int,int);
---
Object engine.physics.getIntersection(dvec3,dvec3,int,int);

void setBasis(mat4);
mat4 getBasis();
void setTransform(mat4);
mat4 getTransform();
---
void setBasis(dmat4);
dmat4 getBasis();
void setTransform(dmat4);
dmat4 getTransform();

void setPosition(vec3);
---
void setPosition(dvec3);

void setWorldTransform(mat4);
mat4 getWorldTransform();
mat4 getIWorldTransform();
void setWorldPosition(vec3);
---
void setWorldTransform(dmat4);
dmat4 getWorldTransform();
dmat4 getIWorldTransform();
void setWorldPosition(dvec3);

vec3 getWorldVelocity(vec3);
---
vec3 getWorldVelocity(dvec3);

vec3 getWorldBoundMin();
vec3 getWorldBoundMax();
vec3 getWorldBoundCenter();
float getWorldBoundRadius();
---
dvec3 getWorldBoundMin();
dvec3 getWorldBoundMax();
dvec3 getWorldBoundCenter();
double getWorldBoundRadius();

vec3 getWorldBoundMin(int);
vec3 getWorldBoundMax(int);
vec3 getWorldBoundCenter(int);
float getWorldBoundRadius(int);
---
dvec3 getWorldBoundMin(int);
dvec3 getWorldBoundMax(int);
dvec3 getWorldBoundCenter(int);
double getWorldBoundRadius(int);

void setWorldBoneTransform(int,mat4);
void setWorldBoneChildsTransform(int,mat4);
mat4 getWorldBoneTransform(int);
---
void setWorldBoneTransform(int,dmat4);
void setWorldBoneChildsTransform(int,dmat4);
dmat4 getWorldBoneTransform(int);

void addEmitterSpark(vec3,vec3,vec3);
---
void addEmitterSpark(dvec3,vec3,vec3);

void setForceTransform(int,mat4);
mat4 getForceTransform(int);
---
void setForceTransform(int,dmat4);
dmat4 getForceTransform(int);

void setDeflectorTransform(int,mat4);
mat4 getDeflectorTransform(int);
---
void setDeflectorTransform(int,dmat4);
dmat4 getDeflectorTransform(int);

vec3 getContactPoint(int);
---
dvec3 getContactPoint(int);

void setModelview(mat4);
mat4 getModelview();
mat4 getIModelview();
void setOldModelview(mat4);
mat4 getOldModelview();
---
void setModelview(dmat4);
dmat4 getModelview();
dmat4 getIModelview();
void setOldModelview(dmat4);
dmat4 getOldModelview();

void create2D(vec3,vec3,int);
void create3D(vec3,vec3,int);
---
void create2D(dvec3,dvec3,int);
void create3D(dvec3,dvec3,int);

vec3 getPoint(int);
---
dvec3 getPoint(int);

void setTransform(mat4);
void setPreserveTransform(mat4);
void setVelocityTransform(mat4);
mat4 getTransform();
---
void setTransform(dmat4);
void setPreserveTransform(dmat4);
void setVelocityTransform(dmat4);
dmat4 getTransform();

Shape getIntersection(vec3,vec3,int);
Shape getIntersection(vec3,vec3,int,int);
---
Shape getIntersection(dvec3,dvec3,int);
Shape getIntersection(dvec3,dvec3,int,int);

vec3 getWorldCenterOfMass();
---
dvec3 getWorldCenterOfMass();

void addWorldForce(vec3,vec3);
void addWorldTorque(vec3,vec3);
void addWorldImpulse(vec3,vec3);
vec3 getWorldVelocity(vec3);
---
void addWorldForce(dvec3,vec3);
void addWorldTorque(dvec3,vec3);
void addWorldImpulse(dvec3,vec3);
vec3 getWorldVelocity(dvec3);

mat4 getBoneTransform(int);
---
dmat4 getBoneTransform(int);

int createSlicePieces(vec3,vec3);
int createCrackPieces(vec3,vec3,int,int,float);
---
int createSlicePieces(dvec3,vec3);
int createCrackPieces(dvec3,vec3,int,int,float);

void setParticlePosition(int,vec3);
vec3 getParticlePosition(int);
---
void setParticlePosition(int,dvec3);
dvec3 getParticlePosition(int);

int getIntersection(vec3,vec3);
int getIntersection(vec3,vec3,int);
---
int getIntersection(dvec3,dvec3);
int getIntersection(dvec3,dvec3,int);

void setAnchor0(vec3);
vec3 getAnchor0();
void setAnchor1(vec3);
vec3 getAnchor1();
void setWorldAnchor(vec3);
vec3 getWorldAnchor();
---
void setAnchor0(dvec3);
dvec3 getAnchor0();
void setAnchor1(dvec3);
dvec3 getAnchor1();
void setWorldAnchor(dvec3);
dvec3 getWorldAnchor();

JointFixed(Body,Body,vec3);
---
JointFixed(Body,Body,dvec3);

JointBall(Body,Body,vec3);
JointBall(Body,Body,vec3,vec3);
---
JointBall(Body,Body,dvec3);
JointBall(Body,Body,dvec3,vec3);

JointHinge(Body,Body,vec3,vec3);
---
JointHinge(Body,Body,dvec3,vec3);

JointPrismatic(Body,Body,vec3,vec3);
---
JointPrismatic(Body,Body,dvec3,vec3);

JointCylindrical(Body,Body,vec3,vec3);
---
JointCylindrical(Body,Body,dvec3,vec3);

JointSuspension(Body,Body,vec3,vec3,vec3);
---
JointSuspension(Body,Body,dvec3,vec3,vec3);

JointWheel(Body,Body,vec3,vec3,vec3);
---
JointWheel(Body,Body,dvec3,vec3,vec3);

JointPin(Body,Body,vec3,vec3);
---
JointPin(Body,Body,dvec3,vec3);

vec3 getContactPoint(int);
---
dvec3 getContactPoint(int);

```
