# Unigine::Plugins::FMOD::DSPType Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Pre-defined types of FMOD registered DSP units.


## DSPType Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Was created via a non-FMOD plugin and has an unknown purpose. |
| **MIXER** = 1 | Does not process the signal, acts as a unit purely for mixing inputs. |
| **OSCILLATOR** = 2 | Generates sine/square/saw/triangle or noise tones. |
| **LOWPASS** = 3 | Filters sound using a high quality, resonant lowpass filter algorithm but consumes more CPU time. Deprecated and will be removed in a future release. |
| **ITLOWPASS** = 4 | Filters sound using a resonant lowpass filter algorithm that is used in Impulse Tracker, but with limited cutoff range (0 to 8060 Hz). |
| **HIGHPASS** = 5 | Filters sound using a resonant highpass filter algorithm. Deprecated and will be removed in a future release. |
| **ECHO** = 6 | Produces an echo on the sound and fades out at the desired rate. |
| **FADER** = 7 | Pans and scales the volume of a signal. |
| **FLANGE** = 8 | Produces a flange effect on the sound. |
| **DISTORTION** = 9 | Distorts the sound. |
| **NORMALIZE** = 10 | Normalizes or amplifies the sound to a certain level. |
| **LIMITER** = 11 | Limits the sound to a certain level. |
| **PARAMEQ** = 12 | Attenuates or amplifies a selected frequency range. Deprecated and will be removed in a future release. |
| **PITCHSHIFT** = 13 | Bends the pitch of a sound without changing the speed of playback. |
| **CHORUS** = 14 | Produces a chorus effect on the sound. |
| **VSTPLUGIN** = 15 | Allows the use of Steinberg VST plugins. |
| **WINAMPPLUGIN** = 16 | Allows the use of Nullsoft Winamp plugins. |
| **ITECHO** = 17 | Produces an echo on the sound and fades out at the desired rate as is used in Impulse Tracker. |
| **COMPRESSOR** = 18 | Dynamic compression (linked/unlinked multichannel, wideband). |
| **SFXREVERB** = 19 | I3DL2 reverb effect. |
| **LOWPASS_SIMPLE** = 20 | Filters sound using a simple lowpass with no resonance, but has flexible cutoff and is fast. Deprecated and will be removed in a future release. |
| **DELAY** = 21 | Produces different delays on individual channels of the sound. |
| **TREMOLO** = 22 | Produces a tremolo / chopper effect on the sound. |
| **LADSPAPLUGIN** = 23 | Unsupported / Deprecated. |
| **SEND** = 24 | Sends a copy of the signal to a return DSP anywhere in the DSP tree. |
| **RETURN** = 25 | Receives signals from a number of send DSPs. |
| **HIGHPASS_SIMPLE** = 26 | Filters sound using a simple highpass with no resonance, but has flexible cutoff and is fast. Deprecated and will be removed in a future release. |
| **PAN** = 27 | Pans the signal in 2D or 3D, possibly upmixing or downmixing as well. |
| **THREE_EQ** = 28 | Three-band equalizer. |
| **FFT** = 29 | Analyzes the signal and provides spectrum information back through getParameter. |
| **LOUDNESS_METER** = 30 | Analyzes the loudness and true peak of the signal. |
| **ENVELOPEFOLLOWER** = 31 | Tracks the envelope of the input/sidechain signal. Deprecated and will be removed in a future release. |
| **CONVOLUTIONREVERB** = 32 | Convolution reverb. |
| **CHANNELMIX** = 33 | Provides per channel gain, channel grouping of the input signal which also sets the speaker format for the output signal, and customizable input to output channel routing. |
| **TRANSCEIVER** = 34 | 'Sends' and 'receives' from a selection of up to 32 different slots. It is like a send/return but it uses global slots rather than returns as the destination. Multiple transceivers can receive from a single channel, or multiple transceivers can send to a single channel, or a combination of both. |
| **OBJECTPAN** = 35 | Spatializes input signal by passing it to an external object mixer. |
| **MULTIBAND_EQ** = 36 | Five band parametric equalizer. |
| **MAX** = 37 | Maximum number of pre-defined DSP types. |
