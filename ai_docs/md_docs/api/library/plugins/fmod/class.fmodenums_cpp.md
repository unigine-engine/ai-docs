# Unigine::Plugins::FMOD::FMODEnums Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Enums used in FMOD Plugin API.


## FMODEnums Class

### Enums

## FMOD_MODE

| Name | Description |
|---|---|
| **DEFAULT** = 0x00000000 | Default for all modes listed below. [LOOP_OFF](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#LOOP_OFF), [_2D](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#_2D), [_3D_WORLDRELATIVE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#_3D_WORLDRELATIVE), [_3D_INVERSEROLLOFF](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#_3D_INVERSEROLLOFF). |
| **LOOP_OFF** = 0x00000001 | For non looping sounds. (DEFAULT). Overrides [LOOP_NORMAL](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#LOOP_NORMAL) / [LOOP_BIDI](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#LOOP_BIDI). |
| **LOOP_NORMAL** = 0x00000002 | For forward looping sounds. |
| **LOOP_BIDI** = 0x00000004 | For bidirectional looping sounds. (only works on software mixed static sounds). |
| **_2D** = 0x00000008 | Ignores any 3D processing. (DEFAULT). |
| **_3D** = 0x00000010 | Makes the sound positionable in 3D. Overrides [_2D](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#_2D). |
| **CREATESTREAM** = 0x00000080 | Decompress at runtime, streaming from the source provided (i.e. from disk). Overrides [CREATESAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATESAMPLE) and [CREATECOMPRESSEDSAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATESAMPLE). Note a stream can only be played once at a time due to a stream only having 1 stream buffer and file handle. Open multiple streams to have them play concurrently. |
| **CREATESAMPLE** = 0x00000100 | Decompress at loadtime, decompressing or decoding whole file into memory as the target sample format (i.e. PCM). Fastest for playback and most flexible. |
| **CREATECOMPRESSEDSAMPLE** = 0x00000200 | Load MP2/MP3/FADPCM/IMAADPCM/Vorbis/AT9 or XMA into memory and leave it compressed. Vorbis/AT9/FADPCM encoding only supported in the .FSB container format. During playback the FMOD software mixer will decode it in realtime as a 'compressed sample'. Overrides [CREATESAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATESAMPLE). If the sound data is not one of the supported formats, it will behave as if it was created with [CREATESAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATESAMPLE) and decode the sound into PCM. |
| **OPENUSER** = 0x00000400 | Opens a user created static sample or stream. |
| **OPENMEMORY** = 0x00000800 | "name_or_data" will be interpreted as a pointer to memory instead of filename for creating sounds. If used with [CREATESAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATESAMPLE) or [CREATECOMPRESSEDSAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATECOMPRESSEDSAMPLE), FMOD duplicates the memory into its own buffers. If used with [CREATESTREAM](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATESTREAM), FMOD will stream out of the buffer whose pointer you passed in. In this case, your own buffer should not be freed until you have finished with and released the stream. |
| **OPENMEMORY_POINT** = 0x10000000 | "name_or_data" will be interpreted as a pointer to memory instead of filename for creating sounds. This differs to [OPENMEMORY](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#OPENMEMORY) in that it uses the memory as is, without duplicating the memory into its own buffers. Will not work if the data is compressed and [CREATECOMPRESSEDSAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATECOMPRESSEDSAMPLE) is not used. |
| **OPENRAW** = 0x00001000 | Will ignore file format and treat as raw pcm. |
| **OPENONLY** = 0x00002000 | Just open the file, dont prebuffer or read. Good for fast opens for info. |
| **ACCURATETIME** = 0x00004000 | For accurate Sound::getLength / Channel::setPosition on VBR MP3, and MOD/S3M/XM/IT/MIDI files. Scans file first, so takes longer to open. [OPENONLY](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#OPENONLY) does not affect this. |
| **MPEGSEARCH** = 0x00008000 | For corrupted / bad MP3 files. This will search all the way through the file until it hits a valid MPEG header. Normally only searches for 4k. |
| **NONBLOCKING** = 0x00010000 | For opening sounds and getting streamed subsounds (seeking) asynchronously. |
| **UNIQUE** = 0x00020000 | Unique sound, can only be played one at a time. |
| **_3D_HEADRELATIVE** = 0x00040000 | Make the sound's position, velocity and orientation relative to the listener. |
| **_3D_WORLDRELATIVE** = 0x00080000 | Make the sound's position, velocity and orientation absolute (relative to the world). (DEFAULT) |
| **_3D_INVERSEROLLOFF** = 0x00100000 | This sound will follow the inverse rolloff model where mindistance = full volume, maxdistance = where sound stops attenuating, and rolloff is fixed according to the global rolloff factor. (DEFAULT) |
| **_3D_LINEARROLLOFF** = 0x00200000 | This sound will follow a linear rolloff model where mindistance = full volume, maxdistance = silence. |
| **_3D_LINEARSQUAREROLLOFF** = 0x00400000 | This sound will follow a linear-square rolloff model where mindistance = full volume, maxdistance = silence. |
| **_3D_INVERSETAPEREDROLLOFF** = 0x00800000 | This sound will follow the inverse rolloff model at distances close to mindistance and a linear-square rolloff close to maxdistance. |
| **_3D_CUSTOMROLLOFF** = 0x04000000 | This sound will follow a custom rolloff model. |
| **_3D_IGNOREGEOMETRY** = 0x40000000 | Is not affected by geometry occlusion. |
| **IGNORETAGS** = 0x02000000 | Skips id3v2/asf/etc tag checks when opening a sound, to reduce seek/read overhead when opening files. |
| **LOWMEM** = 0x08000000 | Removes some features from samples to give a lower memory overhead. |

## INIT_FLAGS

| Name | Description |
|---|---|
| **NORMAL** = 0x00000000 | Initialize normally. |
| **STREAM_FROM_UPDATE** = 0x00000001 | No stream thread is created internally. Mainly used with non-realtime outputs. |
| **MIX_FROM_UPDATE** = 0x00000002 | No mixer thread is created internally. |
| **_3D_RIGHTHANDED** = 0x00000004 | 3D calculations will be performed in right-handed coordinates. |
| **CHANNEL_LOWPASS** = 0x00000100 | Enables usage of ChannelControl::setLowPassGain, ChannelControl::set3DOcclusion, or automatic usage by the Geometry API. All voices will add a software lowpass filter effect into the DSP chain which is idle unless one of the previous functions/features are used. |
| **CHANNEL_DISTANCEFILTER** = 0x00000200 | All [_3D](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#_3D) based voices will add a software lowpass and highpass filter effect into the DSP chain which will act as a distance-automated bandpass filter. |
| **PROFILE_ENABLE** = 0x00010000 | Enable TCP/IP based host which allows FMOD Studio or FMOD Profiler to connect to it, and view memory, CPU and the DSP network graph in real-time. |
| **VOL0_BECOMES_VIRTUAL** = 0x00020000 | Any sounds that are 0 volume will go virtual and not be processed except for having their positions updated virtually. |
| **GEOMETRY_USECLOSEST** = 0x00040000 | With the geometry engine, only process the closest polygon rather than accumulating all polygons the sound to listener line intersects. |
| **PREFER_DOLBY_DOWNMIX** = 0x00080000 | Uses the Dolby Pro Logic II downmix algorithm instead of the default stereo downmix algorithm. |
| **THREAD_UNSAFE** = 0x00100000 | Disables thread safety for API calls. Only use this if FMOD is being called from a single thread, and if Studio API is not being used! |
| **PROFILE_METER_ALL** = 0x00200000 | Slower, but adds level metering for every single DSP unit in the graph. |
| **MEMORY_TRACKING** = 0x00400000 | Enables memory allocation tracking. Currently this is only useful when using the Studio API. Increases memory footprint and reduces performance. |

## TIME_UNIT

| Name | Description |
|---|---|
| **MS** = 0x00000001 | Milliseconds. |
| **PCM** = 0x00000002 | PCM samples, related to milliseconds * samplerate / 1000. |
| **PCMBYTES** = 0x00000004 | Bytes, related to PCM samples * channels * datawidth (ie 16bit = 2 bytes). |
| **RAWBYTES** = 0x00000008 | Raw file bytes of (compressed) sound data (does not include headers). Only used by [Sound::getLength](../../../../api/library/plugins/fmod/class.fmod_sound_cpp.md#getLength_int_uint) and [Channel::getPositionTimeLine](../../../../api/library/plugins/fmod/class.channel_cpp.md#getPositionTimeLine_uint_int_void). |
| **PCMFRACTION** = 0x00000010 | Fractions of 1 PCM sample. Unsigned int range 0 to 0xFFFFFFFF. Used for sub-sample granularity for DSP purposes. |
| **MODORDER** = 0x00000100 | MOD/S3M/XM/IT. Order in a sequenced module format. |
| **MODROW** = 0x00000200 | MOD/S3M/XM/IT. Current row in a sequenced module format. Cannot use with [Channel::setPositionTimeLine](../../../../api/library/plugins/fmod/class.channel_cpp.md#setPositionTimeLine_uint_int_void). [Sound::getLength](../../../../api/library/plugins/fmod/class.fmod_sound_cpp.md#getLength_int_uint) will return the number of rows in the currently playing or seeked to pattern. |
| **MODPATTERN** = 0x00000400 | MOD/S3M/XM/IT. Current pattern in a sequenced module format. Cannot use with [Channel::setPositionTimeLine](../../../../api/library/plugins/fmod/class.channel_cpp.md#setPositionTimeLine_uint_int_void). [Sound::getLength](../../../../api/library/plugins/fmod/class.fmod_sound_cpp.md#getLength_int_uint) will return the number of patterns in the song and [Channel::getPositionTimeLine](../../../../api/library/plugins/fmod/class.channel_cpp.md#getPositionTimeLine_uint_int_void) will return the currently playing pattern. |

## ERROR_TYPE

| Name | Description |
|---|---|
| **OK** = 0 | No errors. |
| **ERR_BADCOMMAND** = 1 | Tried to call a function on a data type that does not allow this type of functionality. |
| **ERR_CHANNEL_ALLOC** = 2 | Error trying to allocate a channel. |
| **ERR_CHANNEL_STOLEN** = 3 | The specified channel has been reused to play another sound. |
| **ERR_DMA** = 4 | DMA Failure. See debug output for more information. |
| **ERR_DSP_CONNECTION** = 5 | DSP connection error. Connection possibly caused a cyclic dependency or connected dsps with incompatible buffer counts. |
| **ERR_DSP_DONTPROCESS** = 6 | DSP return code from a DSP process query callback. Tells mixer not to call the process callback and therefore not consume CPU. Use this to optimize the DSP graph. |
| **ERR_DSP_FORMAT** = 7 | DSP Format error. A DSP unit may have attempted to connect to this network with the wrong format, or a matrix may have been set with the wrong size if the target unit has a specified channel map. |
| **ERR_DSP_INUSE** = 8 | DSP is already in the mixer's DSP network. It must be removed before being reinserted or released. |
| **ERR_DSP_NOTFOUND** = 9 | DSP connection error. Couldn't find the DSP unit specified. |
| **ERR_DSP_RESERVED** = 10 | DSP operation error. Cannot perform operation on this DSP as it is reserved by the system. |
| **ERR_DSP_SILENCE** = 11 | DSP return code from a DSP process query callback. Tells mixer silence would be produced from read, so go idle and not consume CPU. Use this to optimize the DSP graph. |
| **ERR_DSP_TYPE** = 12 | DSP operation cannot be performed on a DSP of this type. |
| **ERR_FILE_BAD** = 13 | Error loading file. |
| **ERR_FILE_COULDNOTSEEK** = 14 | Couldn't perform seek operation. This is a limitation of the medium (ie netstreams) or the file format. |
| **ERR_FILE_DISKEJECTED** = 15 | Media was ejected while reading. |
| **ERR_FILE_EOF** = 16 | End of file unexpectedly reached while trying to read essential data (truncated?). |
| **ERR_FILE_ENDOFDATA** = 17 | End of current chunk reached while trying to read data. |
| **ERR_FILE_NOTFOUND** = 18 | File not found. |
| **ERR_FORMAT** = 19 | Unsupported file or audio format. |
| **ERR_HEADER_MISMATCH** = 20 | There is a version mismatch between the FMOD header and either the FMOD Studio library or the FMOD Core library. |
| **ERR_HTTP** = 21 | A HTTP error occurred. This is a catch-all for HTTP errors not listed elsewhere. |
| **ERR_HTTP_ACCESS** = 22 | The specified resource requires authentication or is forbidden. |
| **ERR_HTTP_PROXY_AUTH** = 23 | Proxy authentication is required to access the specified resource. |
| **ERR_HTTP_SERVER_ERROR** = 24 | A HTTP server error occurred. |
| **ERR_HTTP_TIMEOUT** = 25 | The HTTP request timed out. |
| **ERR_INITIALIZATION** = 26 | FMOD was not initialized correctly to support this function. |
| **ERR_INITIALIZED** = 27 | Cannot call this command after System::init. |
| **ERR_INTERNAL** = 28 | An error occurred that wasn't supposed to. Contact support. |
| **ERR_INVALID_FLOAT** = 29 | Value passed in was a NaN, Inf or denormalized float. |
| **ERR_INVALID_HANDLE** = 30 | An invalid object handle was used. |
| **ERR_INVALID_PARAM** = 31 | An invalid parameter was passed to this function. |
| **ERR_INVALID_POSITION** = 32 | An invalid seek position was passed to this function. |
| **ERR_INVALID_SPEAKER** = 33 | An invalid speaker was passed to this function based on the current speaker mode. |
| **ERR_INVALID_SYNCPOINT** = 34 | The syncpoint did not come from this sound handle. |
| **ERR_INVALID_THREAD** = 35 | Tried to call a function on a thread that is not supported. |
| **ERR_INVALID_VECTOR** = 36 | The vectors passed in are not unit length, or perpendicular. |
| **ERR_MAXAUDIBLE** = 37 | Reached maximum audible playback count for this sound's soundgroup. |
| **ERR_MEMORY** = 38 | Not enough memory or resources. |
| **ERR_MEMORY_CANTPOINT** = 39 | Can't use FMOD_OPENMEMORY_POINT on non PCM source data, or non mp3/xma/adpcm data if FMOD_CREATECOMPRESSEDSAMPLE was used. |
| **ERR_NEEDS3D** = 40 | Tried to call a command on a 2d sound when the command was meant for 3d sound. |
| **ERR_NEEDSHARDWARE** = 41 | Tried to use a feature that requires hardware support. |
| **ERR_NET_CONNECT** = 42 | Couldn't connect to the specified host. |
| **ERR_NET_SOCKET_ERROR** = 43 | A socket error occurred. This is a catch-all for socket-related errors not listed elsewhere. |
| **ERR_NET_URL** = 44 | The specified URL couldn't be resolved. |
| **ERR_NET_WOULD_BLOCK** = 45 | Operation on a non-blocking socket could not complete immediately. |
| **ERR_NOTREADY** = 46 | Operation could not be performed because specified sound/DSP connection is not ready. |
| **ERR_OUTPUT_ALLOCATED** = 47 | Error initializing output device, but more specifically, the output device is already in use and cannot be reused. |
| **ERR_OUTPUT_CREATEBUFFER** = 48 | Error creating hardware sound buffer. |
| **ERR_OUTPUT_DRIVERCALL** = 49 | A call to a standard soundcard driver failed, which could possibly mean a bug in the driver or resources were missing or exhausted. |
| **ERR_OUTPUT_FORMAT** = 50 | Soundcard does not support the specified format. |
| **ERR_OUTPUT_INIT** = 51 | Error initializing output device. |
| **ERR_OUTPUT_NODRIVERS** = 52 | The output device has no drivers installed. If pre-init, FMOD_OUTPUT_NOSOUND is selected as the output mode. If post-init, the function just fails. |
| **ERR_PLUGIN** = 53 | An unspecified error has been returned from a plugin. |
| **ERR_PLUGIN_MISSING** = 54 | A requested output, dsp unit type or codec was not available. |
| **ERR_PLUGIN_RESOURCE** = 55 | A resource that the plugin requires cannot be found (i.e. the DLS file for MIDI playback). |
| **ERR_PLUGIN_VERSION** = 56 | A plugin was built with an unsupported SDK version. |
| **ERR_RECORD** = 57 | An error occurred trying to initialize the recording device. |
| **ERR_REVERB_CHANNELGROUP** = 58 | Reverb properties cannot be set on this channel because a parent ChannelGroup owns the reverb connection. |
| **ERR_REVERB_INSTANCE** = 59 | Specified instance in FMOD_REVERB_PROPERTIES couldn't be set. Most likely because it is an invalid instance number or the reverb doesn't exist. |
| **ERR_SUBSOUNDS** = 60 | The error occurred because the sound referenced contains subsounds when it shouldn't have, or it doesn't contain subsounds when it should have. The operation may also not be able to be performed on a parent sound. |
| **ERR_SUBSOUND_ALLOCATED** = 61 | This subsound is already being used by another sound, you cannot have more than one parent to a sound. Null out the other parent's entry first. |
| **ERR_SUBSOUND_CANTMOVE** = 62 | Shared subsounds cannot be replaced or moved from their parent stream, such as when the parent stream is an FSB file. |
| **ERR_TAGNOTFOUND** = 63 | The specified tag could not be found or there are no tags. |
| **ERR_TOOMANYCHANNELS** = 64 | The sound created exceeds the allowable input channel count. |
| **ERR_TRUNCATED** = 65 | The retrieved string is too long to fit in the supplied buffer and has been truncated. |
| **ERR_UNIMPLEMENTED** = 66 | Something in FMOD hasn't been implemented when it should be! contact support! |
| **ERR_UNINITIALIZED** = 67 | This command failed because System::init or System::setDriver was not called. |
| **ERR_UNSUPPORTED** = 68 | A command issued was not supported by this object. Possibly a plugin without certain callbacks specified. |
| **ERR_VERSION** = 69 | The version number of this file format is not supported. |
| **ERR_EVENT_ALREADY_LOADED** = 70 | The specified bank has already been loaded. |
| **ERR_EVENT_LIVEUPDATE_BUSY** = 71 | The live update connection failed due to the game already being connected. |
| **ERR_EVENT_LIVEUPDATE_MISMATCH** = 72 | The live update connection failed due to the game data being out of sync with the tool. |
| **ERR_EVENT_LIVEUPDATE_TIMEOUT** = 73 | The live update connection timed out. |
| **ERR_EVENT_NOTFOUND** = 74 | The requested event, parameter, bus or vca could not be found. |
| **ERR_STUDIO_UNINITIALIZED** = 75 | The Studio::System object is not yet initialized. |
| **ERR_STUDIO_NOT_LOADED** = 76 | The specified resource is not loaded, so it can't be unloaded. |
| **ERR_INVALID_STRING** = 77 | An invalid string was passed to this function. |
| **ERR_ALREADY_LOCKED** = 78 | The specified resource is already locked. |
| **ERR_NOT_LOCKED** = 79 | The specified resource is not locked, so it can't be unlocked. |
| **ERR_RECORD_DISCONNECTED** = 80 | The specified recording driver has been disconnected. |
| **ERR_TOOMANYSAMPLES** = 81 | The length provided exceeds the allowable limit. |
| **RESULT_FORCEINT** = 65536 |  |

## SOUND_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown or custom codec plugin. |
| **AIFF** = 1 | Audio Interchange File Format (.aif, .aiff). Uncompressed integer formats only. |
| **ASF** = 2 | Microsoft Advanced Systems Format (.asf, .wma, .wmv). Platform provided decoder, available only on Windows. |
| **DLS** = 3 | Downloadable Sound (.dls). Multi-sound bank format used by MIDI (.mid). |
| **FLAC** = 4 | Free Lossless Audio Codec (.flac). |
| **FSB** = 5 | FMOD Sample Bank (.fsb). Proprietary multi-sound bank format. Supported encodings: PCM16, FADPCM, Vorbis, AT9, XMA, Opus. |
| **IT** = 6 | Impulse Tracker (.it). |
| **MIDI** = 7 | Musical Instrument Digital Interface (.mid). |
| **MOD** = 8 | Protracker / Fasttracker Module File (.mod). |
| **MPEG** = 9 | Moving Picture Experts Group (.mp2, .mp3). Also supports .wav (RIFF) container format. |
| **OGGVORBIS** = 10 | Ogg Vorbis (.ogg). |
| **PLAYLIST** = 11 | Play list information container (.asx, .pls, .m3u, .wax). No audio, tags only. |
| **RAW** = 12 | Raw uncompressed PCM data (.raw). |
| **S3M** = 13 | ScreamTracker 3 Module (.s3m). |
| **USER** = 14 | User created sound. |
| **WAV** = 15 | Microsoft Waveform Audio File Format (.wav). Supported encodings: Uncompressed PCM, IMA ADPCM. Platform provided ACM decoder extensions, available only on Windows. |
| **XM** = 16 | FastTracker 2 Extended Module (.xm). |
| **XMA** = 17 | Microsoft XMA bit-stream supported by FSB (.fsb) container format. Platform provided decoder, available only on Xbox. |
| **AUDIOQUEUE** = 18 | Apple Audio Queue decoder (.mp4, .m4a, .mp3). Supported encodings: AAC, ALAC, MP3. Platform provided decoder, available only on iOS / tvOS devices. |
| **AT9** = 19 | Sony ATRAC9 bit-stream supported by FSB (.fsb) container format. Platform provided decoder, available only on PlayStation. |
| **VORBIS** = 20 | Vorbis bit-stream supported by FSB (.fsb) container format. |
| **MEDIA_FOUNDATION** = 21 | Microsoft Media Foundation decoder (.asf, .wma, .wmv, .mp4, .m4a). Platform provided decoder, available only on UWP. |
| **MEDIACODEC** = 22 | Google Media Codec decoder (.m4a, .mp4). Platform provided decoder, available only on Android. |
| **FADPCM** = 23 | FMOD Adaptive Differential Pulse Code Modulation bit-stream supported by FSB (.fsb) container format. |
| **OPUS** = 24 | Opus bit-stream supported by FSB (.fsb) container format. Platform provided decoder, available only on Xbox Series X\|S. |
| **MAX** = 25 | Maximum number of sound types supported. |

## SOUND_FORMAT

| Name | Description |
|---|---|
| **NONE** = 0 | Uninitalized / unknown. |
| **PCM8** = 1 | 8bit integer PCM data. |
| **PCM16** = 2 | 16bit integer PCM data. |
| **PCM24** = 3 | 24bit integer PCM data. |
| **PCM32** = 4 | 32bit integer PCM data. |
| **PCMFLOAT** = 5 | 32bit floating point PCM data. |
| **BITSTREAM** = 6 | Sound data is in its native compressed format. See [CREATECOMPRESSEDSAMPLE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#CREATECOMPRESSEDSAMPLE) |
| **FORMAT_MAX** = 7 | Maximum number of sound formats supported. |

## DSP_CONNECTION_TYPE

| Name | Description |
|---|---|
| **STANDARD** = 0 | Default connection type. Audio is mixed from the input to the output DSP's audible buffer. |
| **CONNECTION_TYPE_SIDECHAIN** = 1 | Sidechain connection type. Audio is mixed from the input to the output DSP's sidechain buffer. |
| **SEND** = 2 | Send connection type. Audio is mixed from the input to the output DSP's audible buffer, but the input is NOT executed, only copied from. A standard connection or sidechain needs to make an input execute to generate data. |
| **SEND_SIDECHAIN** = 3 | Send sidechain connection type. Audio is mixed from the input to the output DSP's sidechain buffer, but the input is NOT executed, only copied from. A standard connection or sidechain needs to make an input execute to generate data. |
| **CONNECTION_TYPE_MAX** = 4 | Maximum number of DSP connection types supported. |

## PARAMETER_DATA_TYPE

| Name | Description |
|---|---|
| **DATA_TYPE_USER** = 0 | Default data type. All user data types should be 0 or above. |
| **OVERALLGAIN** = -1 | Data type for FMOD_DSP_PARAMETER_OVERALLGAIN parameters. There should be a maximum of one per DSP. |
| **_3DATTRIBUTES** = -2 | Data type for FMOD_DSP_PARAMETER_3DATTRIBUTES parameters. There should be a maximum of one per DSP. |
| **SIDECHAIN** = -3 | Data type for FMOD_DSP_PARAMETER_SIDECHAIN parameters. There should be a maximum of one per DSP. |
| **FFT** = -4 | Data type for FMOD_DSP_PARAMETER_FFT parameters. There should be a maximum of one per DSP. |
| **_3DATTRIBUTES_MULTI** = -5 | Data type for FMOD_DSP_PARAMETER_3DATTRIBUTES_MULTI parameters. There should be a maximum of one per DSP. |
| **ATTENUATION_RANGE** = -6 | Data type for FMOD_DSP_PARAMETER_ATTENUATION_RANGE parameters. There should be a maximum of one per DSP. |

## DSP_PARAMETER_FLOAT_MAPPING_TYPE

| Name | Description |
|---|---|
| **DSP_PARAMETER_FLOAT_MAPPING_TYPE_LINEAR** = 0 | DSP float parameter mapping type where the values are mapped linearly across dials and automation curves. |
| **DSP_PARAMETER_FLOAT_MAPPING_TYPE_AUTO** = 1 | DSP float parameter mapping type where the mapping is automatically chosen based on range and units. This mode generates a mapping based on range and units. For example, if the units are in Hertz and the range is with-in the audio spectrum, a Bark scale will be chosen. Logarithmic scales may also be generated for ranges above zero spanning several orders of magnitude. |
| **DSP_PARAMETER_FLOAT_MAPPING_TYPE_PIECEWISE_LINEAR** = 2 | DSP float parameter mapping type where the values mapped in a piecewise linear fashion. |

## DSP_PARAMETER_TYPE

| Name | Description |
|---|---|
| **DSP_PARAMETER_TYPE_FLOAT** = 0 | The DSP parameter type is float. |
| **DSP_PARAMETER_TYPE_INT** = 1 | The DSP parameter type is integer. |
| **DSP_PARAMETER_TYPE_BOOL** = 2 | The DSP parameter type is boolean. |
| **DSP_PARAMETER_TYPE_DATA** = 3 | The DSP parameter type is data. |
| **DSP_PARAMETER_TYPE_MAX** = 4 | Maximum number of DSP parameter types. |
