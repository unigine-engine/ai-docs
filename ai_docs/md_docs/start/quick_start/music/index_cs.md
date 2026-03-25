# Playing Background Music (CS)


The game must output some audio besides the bullet hit sound effect. To play the background music we will use the component system once again.


Let's create the node with a **Music Player** component that plays the looped music from the game start.


1. Create a new C# component and call it **MusicPlayer**. Open your IDE and copy the code below. Save your code in the IDE to ensure it's automatic compilation on switching back to UnigineEditor. <details> <summary>MusicPlayer.cs | Close</summary> ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class MusicPlayer : Component { public AssetLink backgroundMusic; AmbientSource music; void Init() { // check if the backgroundMusic is set and the file asset exists if (backgroundMusic.IsFileExist) { music = new AmbientSource(backgroundMusic.Path); music.Loop = 1; music.Gain = 0.5f; // start playing the music on initialization music.Play(); } } void Shutdown() { if (music.IsValidPtr) music.DeleteLater(); } } ``` </details>
2. Create a new *Dummy Node*, rename it to **"music_player"**, and place it somewhere in the world.
3. Add the *MusicPlayer* component to the *music_player* node.
4. Assign the imported music asset (`programming_quick_start/music/ost.mp3`) to the *Background Music* field of the **MusicPlayer** component. ![](background_music.png)
5. Save changes to the world, go to *File->Save World* or press **Ctrl+S** hotkey.
6. Run the project in the UnigineEditor to check out the background music. ![](run_game.png)
