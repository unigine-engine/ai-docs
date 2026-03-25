# Unigine.DecalProj Class (CS)

**Inherits from:** Decal


This class describes how to create and modify [projected decals](../../../objects/decals/proj/index.md).


### Creating a Projected Decal


The following code illustrates how to create a projected decal, set its parameters and add the node to UnigineEditor.


```csharp
using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
        private DecalProj decal_proj;

        public override bool Init()
        {

			// create an proj decal and setting its radius to 10, fov to 60, aspect to 1.0f, material to "decal_base"
			decal_proj = new DecalProj();
			decal_proj.Radius = 10.0f;
			decal_proj.Fov = 60.0f;
			decal_proj.Aspect = 1.0f;

			// set the name and position of the decal
            decal_proj.Name = "Proj Decal";
            decal_proj.WorldPosition = new Vec3(0.0f, 0.0f, 5.0f);

            return true;
		}
	}
}

```


## DecalProj Class

### Properties

## float ZNear

The distance to the near clipping plane of the decal.
## float Fov

The current field of view of the decal's projector.
## float Aspect

The current aspect ratio of the decal.
## 🔒︎ mat4 Projection

The projection matrix.
### Members

---

## DecalProj ( )

Constructor. Creates a new projected decal with default parameters.
## static int type ( )

Returns the type of the node.
### Return value

[Decal](../../../api/library/decals/class.decal_cs.md) type identifier.
