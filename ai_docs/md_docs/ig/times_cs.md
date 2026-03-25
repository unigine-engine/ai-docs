# Working With Time via API (CS)


There is a set of "times" that you can get via API using different classes, so you might get confused - which one to use and when. The goal of this small article is to get rid of the ambiguity.


## Time


***[Game.Time](../api/library/engine/class.game_cs.md#getTime_float)*** - time of the game. This method is the least accurate, based on internal *Engine::time* it ignores spikes and freezes. It is suitable for creating games. Moreover, you can change the speed of this timer using *[Game.Scale](../api/library/engine/class.game_cs.md#setScale_float_void)* and *[Game.Enabled](../api/library/engine/class.game_cs.md#setEnabled_int_void)*. That is, after a game pause, the game state will remain where it was before the pause, without shifting far away - animations, particles, etc. will resume from the same position.


**[Stopwatch.GetTimestamp()](https://learn.microsoft.com/en-us/dotnet/api/system.diagnostics.stopwatch.gettimestamp?view=net-8.0#system-diagnostics-stopwatch-gettimestamp)** method (from the standard **System.Diagnostics** module) is the most accurate and closest to wall-clock time. It returns seconds as a double precision, allowing operation with microseconds/nanoseconds. It ignores spikes and freezes. Can be used for any application independent time calculations.


In case you don't need time accuracy that high, you can simply use the standard and convenient **[DateTime.Now](https://learn.microsoft.com/en-us/dotnet/api/system.datetime.now?view=net-8.0)** property.


***[Unigine.Plugins.Syncker.Syncker.Time](../api/library/plugins/syncker/class.syncker_syncker_cs.md#getTime_double)*** *property* returns seconds as a *double* value. Based on *Time*, it also ignores spikes but may be shifted forward or backward in case of synchronization disruption between the *Master* and *Slaves*. Should be used for critical animations and logic synchronized through *[Syncker](../code/plugins/syncker/index.md)* mechanisms.


***[Unigine.Plugins.IG.Manager.InterpolationTime](../api/library/plugins/ig/api/class.managerinterface_cs.md#getInterpolationTime_double)*** *property* can also be shifted forward or backward in case of disruption of *IG-Host* synchronization. Between host-frames, it uses *[Unigine.Plugins.Syncker.Syncker.Time](../api/library/plugins/syncker/class.syncker_syncker_cs.md#getTime_double)*, so it can also be shifted in case of disruption of *Master-Slave* synchronization. This is used only for interpolating motion of entities obtained with timestamps from the host.


## Delta Time (a.k.a. IFps)


With regards to game engines, ***Delta Time*** means the amount of time that has elapsed since the previous frame. In UNIGINE this thing is called ***Inverse FPS*** or shorter ***IFps***. Similar to the times described above, there are several *'delta times'* you can meet as well.


***[Engine.IFps](../api/library/engine/class.engine_cs.md#getIFps_float)*** - time spent to complete the last frame (time between the last frame and the current one). It returns seconds as a *float* value, so precision after the decimal point is not guaranteed. It is normal to deliberately ignore any spikes and freezes of the application. You can call ***[Engine.StartFps()](../api/library/engine/class.engine_cs.md#startFps_void)* / *[Engine.StopFps()](../api/library/engine/class.engine_cs.md#stopFps_void)*** to ignore (exclude from being taken into account) a certain spike that you're going to make (e.g., process some heavy non-rendering tasks) or in case the application window is hidden.


***[Game.IFps](../api/library/engine/class.game_cs.md#getIFps_float)*** - similar to ***[Engine.IFps](../api/library/engine/class.engine_cs.md#getIFps_float)***, it's the time between the last frame of the game and the current one (the time in seconds it took to complete the last frame). It is suitable for creating games. Usually this time is the same as the Engine's *IFps*, but you can change the scale of this timer using *[Game.Scale](../api/library/engine/class.game_cs.md#setScale_float_void)* and even stop it for a while via *[Game.Enabled](../api/library/engine/class.game_cs.md#setEnabled_int_void)*. After a game pause, the game state will remain where it was before the pause - animations/expression will continue from the same position and state, etc. Moreover, you can use ***[Game.IFps](../api/library/engine/class.game_cs.md#setIFps_float_void)*** to set your own *IFps* value when necessary.


***[Unigine.Plugins.Syncker.Syncker.IFps](../api/library/plugins/syncker/class.syncker_syncker_cs.md#getIFps_double)*** and ***[Unigine.Plugins.IG.Manager.IFps](../api/library/plugins/ig/api/class.managerinterface_cs.md#getIFps_float)*** *properties* will both give you the actual time difference between the last subsequent frames (previous and current), without an option to tweak or ignore anything. Should be used for critical animations and logic synchronization through *[Syncker](../code/plugins/syncker/index.md)* mechanisms on different computers, without being afraid of sync disruption.
