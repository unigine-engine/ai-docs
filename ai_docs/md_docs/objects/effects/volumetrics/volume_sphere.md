# Volume Sphere


*Volume Sphere* has adjustable radii along three axes, so it can take a shape of an ellipsoid. *Volume Sphere* is used to create:


- [Fog](../../../content/materials/library/volume_fog_base/index.md) haze or mist that hides objects behind it. If spheres with fog intersect, denser fog is created.
- [Spheres of light](../../../content/materials/library/volume_light_base/index.md) around point light sources, for example, a bulb or a candle. These spheres are visible when the light illuminates dust and other particles floating in the air. A light material is always rendered as a regular sphere.


![Volume Sphere with a light material](sphere_light.jpg)

*Volume Sphere with a light material around light sources*


![Volume Sphere with a light material](sphere_wireframe.jpg)

*Volume Sphere with a fog material*


### See also


- The *[ObjectVolumeSphere](../../../api/library/objects/class.objectvolumesphere_cpp.md)* class to edit *Volume Sphere* objects via API


## Creating a Volume Sphere Object


To create a *Volume Sphere* object, perform the following steps:


1. On the Menu bar, click *Create -> Volume -> Sphere*. ![](volume_sphere_create.png)
2. Place the *Volume Sphere* object somewhere in the world.
3. Specify the *Volume Sphere* object [parameters](#volume_sphere_parameters).


## Volume Sphere Parameters


In the *Volume Sphere* section (*[Parameters](../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of *Volume Sphere*:


![](volume_sphere_params.png)


| Edit Size | Toggles the editing mode for the *Volume Sphere* node. When enabled, *Volume Sphere* can be resized along the axes: each axis is highlighted with the colored circle. To change the radius along the axis, drag the corresponding circle. ![](editing_volume_sphere.jpg) |
|---|---|
| Radius | Scale of *Volume Sphere* along X, Y, and Z axes respectively. > **Notice:** If a *[volume_light](../../../content/materials/library/volume_light_base/index.md)* material is assigned to *Volume Sphere*, it cannot be of an ellipsoid shape. *Volume Sphere* is rendered based only on the X-axis radius value. If its radii along Y or Z axes are smaller, then the object is cut along them. |
