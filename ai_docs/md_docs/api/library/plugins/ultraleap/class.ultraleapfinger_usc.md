# Unigine::Plugins::UltraleapFinger Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This structure represents a [finger](../../../../code/plugins/ultraleap/index_usc.md#fingers) of a [hand](../../../../api/library/plugins/ultraleap/class.ultraleaphand_usc.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


## UltraleapFinger Class

### Members

## int getType () const

Returns the current type of the finger. One of the [TYPE_*](#TYPE_THUMB) values.
### Return value

Current type of the finger
## int isExtended () const

Returns the current value indicating if the finger is extended.
### Return value

Current the finger is extended
## double getLength () const

Returns the current length of the finger, in meters.
### Return value

Current length of the finger, in meters
## UltraleapHand getHand () const

Returns the current object for the hand.
### Return value

Current object for the hand
## UltraleapBone getBoneMetacarpal () const

Returns the current object for the metacarpal bone.
### Return value

Current object for the metacarpal bone
## UltraleapBone getBoneProximal () const

Returns the current object for the proximal phalange bone.
### Return value

Current object for the proximal phalange bone
## UltraleapBone getBoneIntermediate () const

Returns the current object for the intermediate phalange bone.
### Return value

Current object for the intermediate phalange bone
## UltraleapBone getBoneDistal () const

Returns the current object for the distal phalange bone.
### Return value

Current object for the distal phalange bone
