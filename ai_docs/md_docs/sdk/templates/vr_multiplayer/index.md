# VR Multiplayer C++ Template


[![VR Multiplayer C++ Template](img/vr_mr_template_sm.png)](img/vr_mr_template.png)


A configurable C++ project template that provides a practical **foundation for developing networked VR and desktop multiplayer applications** with UNIGINE. Built on [**Steam Networking**](https://partner.steamgames.com/doc/features/multiplayer/networking), it demonstrates how to integrate networking with the Engine and synchronize multiplayer state across connected peers, serving as a reference implementation you can use as the base for your own multiplayer architecture.


**The template provides:**


- Steam-based multiplayer: lobby, state replication, and late-join support.
- Support for both VR players (OpenXR / OpenVR / Varjo) and desktop keyboard + mouse players **within the same session**.
- A complete free-for-all deathmatch sample with networked weapons, avatars, and shared object interactions.
- Proximity voice chat and public/private text chat.
- Reusable interactive objects and VR controls.


Built on top of the *[VR Template](../../../sdk/templates/vr/index.md)*, it adds a networking layer over ready-to-use VR interaction mechanics: controllers, grabbing, teleportation, and interactive objects. The reusable building blocks it provides can be adapted for multiplayer training simulators, collaborative VR applications, and other interactive real-time experiences.


## Features


The template features a networked VR/PC deathmatch designed to demonstrate key multiplayer features that can be configured to meet the requirements of a wide range of VR applications.


**Key Features:**


- **Networking (Steam):**

  - Main menu and lobby with Host Game / Join Game (Steam Lobby matchmaking)
  - Separation of reliable gameplay events (hits, ownership changes, chat messages, session snapshots) from continuously streamed data (avatar poses, object transforms, voice), so each uses the best-suited delivery strategy: critical events are delivered reliably and in order, while frequent updates prioritize low latency over perfect delivery
  - Steam relay network (SDR) enabled by default - no port forwarding, no IP exposure
  - Versioned network protocol with codec-based message serialization
  - Late-join support: a new player receives a room snapshot and immediately sees the correct world state
  - Graceful degradation: runs in a local no-networking sandbox when Steam is unavailable
- **Platforms, precision, and launch modes:**

  - VR runtimes: OpenXR, OpenVR, Varjo
  - Desktop / no-VR mode: a full keyboard + mouse player in the same session
  - Windows x64 and Linux x64
  - float and double build precision
  - Runs in UnigineEditor (D3D12 / Vulkan)
- **Players and avatars:**

  - Networked VR avatar (head, two hands, body) and PC avatar
  - HP bar and nickname billboard above each avatar
  - Per-player paint color, chosen in the menu and replicated to everyone
- **Combat:**

  - Pistol (one-handed) and rifle (two-handed accuracy stabilization)
  - Fire modes: hitscan (instant ray) and projectile (physical bullet)
  - Rate-of-fire modes: automatic and burst (rifle)
  - Health and body-part damage (head / body)
  - Visual feedback: muzzle flash, tracer, impact decals, and damage vignette
- **Game loop (deathmatch):**

  - Free-for-all deathmatch with no teams or rounds
  - Instant respawn at a random spawn point
  - Kill/death scoreboard, replicated to all players
- **Communication:**

  - Push-to-talk proximity voice with 3D positional playback and distance culling
  - Public and private (@user_nickname) text chat
- **Item ownership and replication:**

  - Per-entity ownership: one authoritative owner per shared item, transferred on grab
  - Replication of VR handles, levers, valves, sliders, and doors
- **Core VR interaction components:**

  - Object manipulation using VR controllers
  - Grabbable and movable objects
  - Rotatable and translatable handles (levers, valves, sliders, doors), replicated across peers
  - Physical cables
  - Teleportation and free movement within the scene


## Launching the Template


You can run the template in **desktop mode** (keyboard and mouse, no headset) or in [**VR mode**](../../../vr_development/index.md#vr_quick_start) with a connected headset.


![](img/vr_mp_scene.png)


### Enabling Network


**Networking** is powered by Steam and depends on an optional `steam_api64.dll` library. If the library is missing, the template runs in a local sandbox with no network functionality: you can explore the scene, but lobbies, rooms, replication, or voice chat are unavailable. For the multiplayer features to work properly, do the following:


1. Run the Steam client and sign in. Make sure `steam_appid.txt` is present in the project's `bin` folder - it holds the Steam application ID the template runs under. ![Run the Steam Client](img/vrmp_steamclient.png)
2. Open *[https://partner.steamgames.com/downloads/list](https://partner.steamgames.com/downloads/list)* and download *Steamworks SDK **v1.65***. Copy the `redistributable_bin/win64/steam_api64.dll` file in the project's `bin` folder.


### Enabling Voice Chat


**Proximity voice chat** additionally requires the `fmod.dll` library in the `bin` folder:


1. Go to *[https://www.fmod.com/download](https://www.fmod.com/download)*, select **FMOD Engine 2.03.08** from the list and install it.
2. Copy the `FMOD SoundSystem\FMOD Studio API Windows\api\core\lib\x64\fmod.dll` file into your project's `bin` folder.


Without this library the template runs normally without voice chat support.


> **Notice:** **Alternatively**, you can lay the SDKs out under `source/SteamworksSDK/` *(redistributable_bin/win64/steam_api64.dll)* and `source/FMODSDK/` *(core/lib/x64/fmod.dll)* and rebuild the project. The build then copies the libraries into the `bin` folder automatically.


On **Linux**, use the corresponding `.so` libraries (`libsteam_api.so` for networking and `libfmod.so.14` for voice chat support). Steam must be installed as the native package: with a snap or flatpak install, the Steamworks SDK cannot reach the Steam client and the template starts without networking.


## Using the VR Multiplayer Template


[![](img/vr_mr_template_gr_sm.png)](img/vr_mr_template_gr.png)


1. Set your nickname and paint color in the main menu. ![](img/vrmp_lobby.png)
2. Host or join a lobby to enter the deathmatch room.
3. Move around the room, take a pistol or rifle, and shoot the other players. ![](img/vr_mr_template_weapons_sm.png)
4. Switch the weapon between two fire modes (hitscan or projectile) with the button in the room. ![](img/vr_mr_template_damage.png) *Two fire modes: hitscan leaves an impact mark on the surface, projectile bursts into a splatter of the shooter's paint color*
5. When you are defeated, you respawn instantly at a random spawn point.
6. See everyone's kills and deaths on the scoreboard in the room. Talk to nearby players by voice, or send text messages. ![](img/vr_mp_chart.png)


### Controls (Desktop / No-VR Mode)


The desktop player is controlled with the keyboard and mouse:


- **WASD** - move
- **Mouse** - look around
- **LMB** - take objects and interact with the scene
- **RMB** - zoom in
- **U** - fire the held weapon
- **V** - hold to talk (push-to-talk voice)


### Controls (VR Mode)


In VR, you move and interact with the standard VR controller buttons. Hold the **Menu** button on either controller to talk over voice chat.


### Voice Chat


Voice chat is push-to-talk and works by distance. Hold the talk button (**V** on desktop, or the **Menu** button on a controller in VR) and speak. Only players who are close to you can hear you, and the sound comes from the speaking player's avatar.


> **Notice:** Voice chat needs `fmod.dll`. If this file is missing, voice is turned off, but everything else still works.


### Text Chat


![](img/vrmp_chat.png)


Type a message and press **Enter** to send it to everyone in the room. To send a private message to one player, start the message with `@user_nickname` followed by a space and your text.


> **Notice:** The template is a readability-first reference demo, not production competitive code. It uses a trust-based synchronization model: the host is authoritative over shared game state such as health and the scoreboard, while item ownership is claimed directly between peers, and a shooter's hit detection is trusted without server-side re-validation or anti-cheat. This is a deliberate simplification.
