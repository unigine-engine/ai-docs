# Unigine::AnimationBindRuntime Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This binding points a channel at an object that has no place in the scene tree, such as a widget, a viewport or a physical body. Objects like these cannot be addressed by a node identifier or an asset GUID, so the binding holds the object itself.


The pointer is not saved to the file: your code sets it when the world is loaded. Make sure the object outlives the player, or reset the binding before the object is destroyed.


## AnimationBindRuntime Class

### Members

## void setWidget ( const Ptr < Widget >& widget )

Sets a new widget animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../../api/library/gui/class.widget_cpp.md)>&* **widget** - The widget animated through this binding

## Ptr < Widget > getWidget () const

Returns the current widget animated through this binding.
### Return value

Current widget animated through this binding
## void setGui ( const Ptr < Gui >& gui )

Sets a new GUI animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../../api/library/gui/class.gui_cpp.md)>&* **gui** - The GUI animated through this binding

## Ptr < Gui > getGui () const

Returns the current GUI animated through this binding.
### Return value

Current GUI animated through this binding
## void setWindow ( const Ptr < EngineWindow >& window )

Sets a new engine window animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../../api/library/gui/class.enginewindow_cpp.md)>&* **window** - The engine window animated through this binding

## Ptr < EngineWindow > getWindow () const

Returns the current engine window animated through this binding.
### Return value

Current engine window animated through this binding
## void setViewport ( const Ptr < Viewport >& viewport )

Sets a new viewport animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Viewport](../../../../api/library/rendering/class.viewport_cpp.md)>&* **viewport** - The viewport animated through this binding

## Ptr < Viewport > getViewport () const

Returns the current viewport animated through this binding.
### Return value

Current viewport animated through this binding
## void setBody ( const Ptr < Body >& body )

Sets a new physical body animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Body](../../../../api/library/physics/class.body_cpp.md)>&* **body** - The physical body animated through this binding

## Ptr < Body > getBody () const

Returns the current physical body animated through this binding.
### Return value

Current physical body animated through this binding
## void setJoint ( const Ptr < Joint >& joint )

Sets a new joint animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Joint](../../../../api/library/physics/class.joint_cpp.md)>&* **joint** - The joint animated through this binding

## Ptr < Joint > getJoint () const

Returns the current joint animated through this binding.
### Return value

Current joint animated through this binding
## void setShape ( const Ptr < Shape >& shape )

Sets a new shape animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../../api/library/physics/class.shape_cpp.md)>&* **shape** - The shape animated through this binding

## Ptr < Shape > getShape () const

Returns the current shape animated through this binding.
### Return value

Current shape animated through this binding
## void setCamera ( const Ptr < Camera >& camera )

Sets a new camera animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../../api/library/rendering/class.camera_cpp.md)>&* **camera** - The camera animated through this binding

## Ptr < Camera > getCamera () const

Returns the current camera animated through this binding.
### Return value

Current camera animated through this binding
## void setLensFlare ( const Ptr < LightLensFlare >& flare )

Sets a new lens flare of a light source animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LightLensFlare](../../../../api/library/lights/class.lightlensflare_cpp.md)>&* **flare** - The lens flare of a light source animated through this binding

## Ptr < LightLensFlare > getLensFlare () const

Returns the current lens flare of a light source animated through this binding.
### Return value

Current lens flare of a light source animated through this binding
## void setParticleModifier ( const Ptr <ParticleModifier>& modifier )

Sets a new particle modifier animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ParticleModifier>&* **modifier** - The particle modifier animated through this binding

## Ptr <ParticleModifier> getParticleModifier () const

Returns the current particle modifier animated through this binding.
### Return value

Current particle modifier animated through this binding
## void setAmbientSource ( const Ptr < AmbientSource >& source )

Sets a new ambient sound source animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AmbientSource](../../../../api/library/sounds/class.ambientsource_cpp.md)>&* **source** - The ambient sound source animated through this binding

## Ptr < AmbientSource > getAmbientSource () const

Returns the current ambient sound source animated through this binding.
### Return value

Current ambient sound source animated through this binding
## void setAnimScript ( const Ptr < AnimScript >& script )

Sets a new animation script animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimScript](../../../../api/library/animations/skeletal/class.animscript_cpp.md)>&* **script** - The animation script animated through this binding

## Ptr < AnimScript > getAnimScript () const

Returns the current animation script animated through this binding.
### Return value

Current animation script animated through this binding
## void setSequence ( const Ptr < AnimationSequence >& sequence )

Sets a new sequence animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md)>&* **sequence** - The sequence animated through this binding

## Ptr < AnimationSequence > getSequence () const

Returns the current sequence animated through this binding.
### Return value

Current sequence animated through this binding
## void setProperty ( const Ptr < Property >& property )

Sets a new property animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Property](../../../../api/library/common/class.property_cpp.md)>&* **property** - The property animated through this binding

## Ptr < Property > getProperty () const

Returns the current property animated through this binding.
### Return value

Current property animated through this binding
## void setRenderEnvironmentPreset ( const Ptr < RenderEnvironmentPreset >& preset )

Sets a new render environment preset animated through this binding.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[RenderEnvironmentPreset](../../../../api/library/rendering/class.renderenvironmentpreset_cpp.md)>&* **preset** - The render environment preset animated through this binding

## Ptr < RenderEnvironmentPreset > getRenderEnvironmentPreset () const

Returns the current render environment preset animated through this binding.
### Return value

Current render environment preset animated through this binding
---

## AnimationBindRuntime ( )

Constructor. Creates an empty runtime binding.
