# Unigine.DecalOrtho Class (CS)

**Inherits from:** Decal


This class describes how to create and modify [orthographic decals](../../../objects/decals/ortho/index.md).


### Creating an Orthographic Decal


The following code illustrates how to create an orthographic decal, set its parameters and add the node to UnigineEditor.


```csharp
using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
        private DecalOrtho decal_ortho;

        public override bool Init()
        {

			// create an ortho decal and setting its radius to 10, width and height to 2
			decal_ortho = new DecalOrtho();
			decal_ortho.Radius = 10.0f;
			decal_ortho.Width = 2.0f;
			decal_ortho.Height = 2.0f;

			// set the name and position of the decal
            decal_ortho.Name = "Ortho Decal";
            decal_ortho.WorldPosition = new Vec3(0.0f, 0.0f, 5.0f);

            return true;
        }

	}
}

```


## DecalOrtho Class

### Properties

## float ZNear

The value of the near clipping plane.
## float Width

The current length of the projection box along the x axis, in units.
## float Height

The current length of the projection box along the y axis.
## 🔒︎ mat4 Projection

The projection matrix.
### Members

---

## DecalOrtho ( )

Constructor. Creates a new orthographic decal with default parameters.
## static int type ( )

Returns a type identifier.
### Return value

Type identifier.
