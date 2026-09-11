# Unigine::AnimationBindRuntime Class (CS)

**Inherits from:** AnimationBind


This binding points a channel at an object that has no place in the scene tree, such as a widget, a viewport or a physical body. Objects like these cannot be addressed by a node identifier or an asset GUID, so the binding holds the object itself.


The pointer is not saved to the file: your code sets it when the world is loaded. Make sure the object outlives the player, or reset the binding before the object is destroyed.


## AnimationBindRuntime Class

### Properties

## Widget Widget

The widget animated through this binding.
## Gui Gui

The GUI animated through this binding.
## EngineWindow Window

The engine window animated through this binding.
## Viewport Viewport

The viewport animated through this binding.
## Body Body

The physical body animated through this binding.
## Joint Joint

The joint animated through this binding.
## Shape Shape

The shape animated through this binding.
## Camera Camera

The camera animated through this binding.
## LightLensFlare LensFlare

The lens flare of a light source animated through this binding.
## ParticleModifier ParticleModifier

The particle modifier animated through this binding.
## AmbientSource AmbientSource

The ambient sound source animated through this binding.
## AnimScript AnimScript

The animation script animated through this binding.
## AnimationSequence Sequence

The sequence animated through this binding.
## Property Property

The property animated through this binding.
## RenderEnvironmentPreset RenderEnvironmentPreset

The render environment preset animated through this binding.
### Members

---

## AnimationBindRuntime ( )

Constructor. Creates an empty runtime binding.
