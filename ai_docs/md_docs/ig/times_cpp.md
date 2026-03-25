# Working With Time via API (CPP)


There is a set of "times" that you can get via API using different classes, so you might get confused - which one to use and when. The goal of this small article is to get rid of the ambiguity.


## Time


***[Game::getTime()](../api/library/engine/class.game_cpp.md#getTime_float)*** - time of the game. This method is the least accurate, based on internal *Engine::time* it ignores spikes and freezes. It is suitable for creating games. Moreover, you can change the speed of this timer using *[Game::setScale()](../api/library/engine/class.game_cpp.md#setScale_float_void)* and *[Game::setEnabled()](../api/library/engine/class.game_cpp.md#setEnabled_int_void)*. That is, after a game pause, the game state will remain where it was before the pause, without shifting far away - animations, particles, etc. will resume from the same position.


***[Time::getSeconds()](../api/library/common/class.time_cpp.md#getSeconds_double)*** method is the most accurate and closest to wall-clock time. It returns seconds as a *double* value, allowing operation with microseconds/nanoseconds. It does not take any spikes and freezes into account (uses *QueryPerformanceCounter* for Windows; *gettimeofday* for Linux/Unix inside). Can be used for any application independent time calculations.


***[Unigine::Plugins::Syncker::Syncker::getTime()](../api/library/plugins/syncker/class.syncker_syncker_cpp.md#getTime_double)*** *method* returns seconds as a *double* value. Based on *Time*, it also ignores spikes but may be shifted forward or backward in case of synchronization disruption between the *Master* and *Slaves*. Should be used for critical animations and logic synchronized through *[Syncker](../code/plugins/syncker/index.md)* mechanisms.


***[Unigine::Plugins::IG::Manager::getInterpolationTime()](../api/library/plugins/ig/api/class.managerinterface_cpp.md#getInterpolationTime_double)*** *method* can also be shifted forward or backward in case of disruption of *IG-Host* synchronization. Between host-frames, it uses *[Unigine::Plugins::Syncker::Syncker::getTime()](../api/library/plugins/syncker/class.syncker_syncker_cpp.md#getTime_double)*, so it can also be shifted in case of disruption of *Master-Slave* synchronization. This is used only for interpolating motion of entities obtained with timestamps from the host.


## Delta Time (a.k.a. IFps)


With regards to game engines, ***Delta Time*** means the amount of time that has elapsed since the previous frame. In UNIGINE this thing is called ***Inverse FPS*** or shorter ***IFps***. Similar to the times described above, there are several *'delta times'* you can meet as well.


***[Engine::getIFps()](../api/library/engine/class.engine_cpp.md#getIFps_float)*** - time spent to complete the last frame (time between the last frame and the current one). It returns seconds as a *float* value, so precision after the decimal point is not guaranteed. It is normal to deliberately ignore any spikes and freezes of the application. You can call ***[Engine::startFps()](../api/library/engine/class.engine_cpp.md#startFps_void)* / *[Engine::stopFps()](../api/library/engine/class.engine_cpp.md#stopFps_void)*** to ignore (exclude from being taken into account) a certain spike that you're going to make (e.g., process some heavy non-rendering tasks) or in case the application window is hidden.


***[Game::getIFps()](../api/library/engine/class.game_cpp.md#getIFps_float)*** - similar to ***[Engine::getIFps()](../api/library/engine/class.engine_cpp.md#getIFps_float)***, it's the time between the last frame of the game and the current one (the time in seconds it took to complete the last frame). It is suitable for creating games. Usually this time is the same as the Engine's *IFps*, but you can change the scale of this timer using *[Game::setScale()](../api/library/engine/class.game_cpp.md#setScale_float_void)* and even stop it for a while via *[Game::setEnabled()](../api/library/engine/class.game_cpp.md#setEnabled_int_void)*. After a game pause, the game state will remain where it was before the pause - animations/expression will continue from the same position and state, etc. Moreover, you can use ***[Game::setIFps()](../api/library/engine/class.game_cpp.md#setIFps_float_void)*** to set your own *IFps* value when necessary.


***[Unigine::Plugins::Syncker::Syncker::getIFps()](../api/library/plugins/syncker/class.syncker_syncker_cpp.md#getIFps_double)*** and ***[Unigine::Plugins::IG::Manager::getIFps()](../api/library/plugins/ig/api/class.managerinterface_cpp.md#getIFps_float)*** *methods* will both give you the actual time difference between the last subsequent frames (previous and current), without an option to tweak or ignore anything. Should be used for critical animations and logic synchronization through *[Syncker](../code/plugins/syncker/index.md)* mechanisms on different computers, without being afraid of sync disruption.
