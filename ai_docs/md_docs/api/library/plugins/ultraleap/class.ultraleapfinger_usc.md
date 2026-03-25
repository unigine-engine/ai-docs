# Unigine::Plugins::UltraleapFinger Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This structure represents a [finger](../../../../code/plugins/ultraleap/index_usc.md#fingers) of a [hand](../../../../api/library/plugins/ultraleap/class.ultraleaphand_usc.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


## UltraleapFinger Class

### Members

---

## int getType ( )

Returns the type of the finger.
### Return value

The finger type. One of the [ULTRALEAP_FINGER_TYPE_*](#TYPE_THUMB) values.
## int isExtended ( )

Returns a value indicating if the finger is extended.
### Return value

**1** if the finger is extended; otherwise, **0**.
## double getLength ( )

Returns the length of the finger, in meters.
### Return value

The length of the finger, in meters.
## UltraleapHand getHand ( )

Returns the object for the hand.
### Return value

The object for the hand.
## UltraleapBone getBoneMetacarpal ( )

Returns the object for the metacarpal bone.
### Return value

The object for the metacarpal bone.
## UltraleapBone getBoneProximal ( )

Returns the object for the proximal phalange bone.
### Return value

The object for the proximal phalange bone.
## UltraleapBone getBoneIntermediate ( )

Returns the object for the intermediate phalange bone.
### Return value

The object for the intermediate phalange bone.
## UltraleapBone getBoneDistal ( )

Returns the object for the distal phalange bone.
### Return value

The object for the distal phalange bone.
