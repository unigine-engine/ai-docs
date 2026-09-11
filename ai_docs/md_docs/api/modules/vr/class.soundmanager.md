# SoundManager Class

**Inherits from:** Unigine::WorldLogic


SoundManager provides a singleton service for playing positional 3D sounds in **VR**. It handles one-shot impact sounds and looping slide sounds, with support for sound groups that randomly select from variations.


Sound groups allow automatic randomization between similar sounds (e.g., impact_01.wav, impact_02.wav). The manager also provides volume control for sound effects and music channels.


### See Also


- **Unigine::SoundSource**


## SoundManager Class

---

## static get ( )

Returns the singleton SoundManager instance.
### Return value

Singleton instance.
## void addSoundGroup ( )

Registers a sound group by searching for numbered sound file variants.
### Arguments

## void playSound ( )

Plays a one-shot 3D sound at a position.
### Arguments

## void playLoopSound ( )

Plays a looping sound attached to a node.
### Arguments

## void setSoundsVolume ( )

Sets the volume for all sound effects.
### Arguments

## void setMusicVolume ( )

Sets the volume for music.
### Arguments

## void addSoundGroup ( )

Registers a sound group from a node's parameter value.
### Arguments

## getSoundGroup ( )

Returns a vector of sound files matching the pattern (e.g., sound_01.wav, sound_02.wav).
### Arguments

### Return value

Vector of sound file paths in the group.
## void warmAllSounds ( )

Preloads all registered sounds to prevent loading delays during playback.
## void setVolume ( )

Sets the master volume with optional delay.
### Arguments

## getVolume ( )

Returns the current master volume level.
### Return value

Current master volume.
## getSoundVolume ( )

Returns the current sound effects volume level.
### Return value

Current sound effects volume.
## getMusicVolume ( )

Returns the current music volume level.
### Return value

Current music volume.
