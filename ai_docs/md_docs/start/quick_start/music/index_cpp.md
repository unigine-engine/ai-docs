# Playing Background Music (CPP)


The game must output some audio besides the bullet hit sound effect. To play the background music we will use the component system once again.


Let's create the node with a **Music Player** component that plays the looped music from the game start.


1. Open your IDE, create a new C++ component, and call it **MusicPlayer**.
2. Copy the code below and paste it to the corresponding files in your project and save them in your IDE. Build and run the solution to generate the **MusicPlayer** property. <details> <summary>MusicPlayer.h | Close</summary> ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UnigineSounds.h> class MusicPlayer :	public Unigine::ComponentBase { public: // declare constructor and destructor for our class and define a property name. COMPONENT_DEFINE(MusicPlayer, ComponentBase) // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); COMPONENT_SHUTDOWN(shutdown); // background music asset PROP_PARAM(File, background_music); protected: void init(); void shutdown(); private: Unigine::AmbientSourcePtr music; }; ``` </details> <details> <summary>MusicPlayer.cpp | Close</summary> ```cpp #include "MusicPlayer.h" REGISTER_COMPONENT(MusicPlayer); using namespace Unigine; void MusicPlayer::init() { music = AmbientSource::create(background_music); music->setLoop(1); music->setGain(0.5f); // start playing the music on initialization music->play(); } void MusicPlayer::shutdown() { if (music) music.deleteLater(); } ``` </details>
3. Create a new *Dummy Node*, rename it to **"music_player"** and place it somewhere in the world.
4. Assign the *MusicPlayer* component to the *music_player* node.
5. Assign the imported music asset (`programming_quick_start/music/ost.mp3`) to the *Background Music* field of the **MusicPlayer** component. ![](background_music_cpp.png)
6. Save changes to the world, go to *File->Save World* or press **Ctrl+S** hotkey.
7. Run the project in your IDE to check out the background music.
