# *LightBound Together*

![LightBound Logo](/LightBound_Together/Images/AI_Logo.png)   

## *Game description*  

**LightBound Together** is a physics-based Co-op multiplayer demo inspired by Human: Fall Flat, designed for 2–4 players. Like its inspiration, it features quirky physics where players can grab, throw, and carry objects to solve puzzles and navigate parkour-style challenges.

The twist is in the atmosphere: instead of being lighthearted, Lightbound leans into an eerie, tense mood. The game is set at night, where players must stay within the safety of the light to survive—the shadows slowly creep in if you wander too far. This mechanic adds cooperation and urgency to puzzle-solving. For example, one player might need to hold a torch to provide light while another carries a crucial object to progress.

By combining slapstick physics with a dark survival twist, Lightbound turns a familiar gameplay formula into something fresh and unsettling.

---

## *My contributions to this project*

All the features have been implemented by me. 

---  

##  *Why i made this game*

I created this demo as my final thesis project at a vocational game development school. I thought the concept was fun and unique, and it gave me the opportunity to explore an idea I was genuinely excited about. At the same time, I wanted to challenge myself by learning more about multiplayer development, since it adds an extra layer of complexity and teamwork to game design.

---  

##  *Networking/Multiplayer plugins*
For the multiplayer system in my Unity project, I chose to use Netcode for GameObjects (NGO) combined with Unity Relay.
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/NGO_Asset.png" width="500" height="600" /></td>
    <td><img src="/LightBound_Together/Images/Relay_Asset.png" width="500" height="600" /></td>
  </tr>
</table>

#### *Netcode for GameObjects*  
I picked NGO because it is Unity’s first-party networking solution designed to work directly with GameObjects, which made it a natural fit for my project. It handles core multiplayer features like spawning, ownership, and synchronization of objects across clients. Since my game is built with a GameObject workflow rather than DOTS/ECS, NGO provided a straightforward and well-integrated way to add multiplayer functionality.

#### *Unity Relay*  
Relay works together with NGO by solving the issue of direct peer-to-peer connections. Normally, players behind NAT or firewalls cannot host or join easily. Relay lets clients connect to a Unity-hosted server endpoint that forwards traffic between players. This way, I didn’t need to set up or pay for dedicated servers, but players could still connect to each other reliably. Relay doesn’t simulate or run game logic itself – it only routes the traffic – which means it pairs perfectly with NGO’s networking layer.

#### *Smooth Sync*  
To improve the player experience, I added Smooth Sync, which interpolates and predicts the movement of networked objects. NGO provides the base synchronization, but Smooth Sync makes the motion appear much smoother and responsive by reducing visible latency and jitter. This was important in my project since player movement and interactions needed to feel natural.

<table>
  <tr>
    <td><img src="/LightBound_Together/Images/SmoothSync_Asset.png" width="500" height="600" /></td>
    <td><img src="/LightBound_Together/Images/MultiplayerTools_Asset.png" width="500" height="600" /></td>
  </tr>
</table>

Together, NGO handles the multiplayer logic, Relay ensures players can always connect, and Smooth Sync makes everything feel fluid. No extra plugins are strictly required beyond these, though Unity also offers Lobby (for matchmaking) and Vivox (for voice chat) if you want to expand functionality further, but there was no need for that in this demo.

---  

##  *Menus, Hosting and Joning*
To support multiplayer with Netcode for GameObjects and Unity Relay, I built a system that handles everything from starting a lobby to unlocking levels.

#### *LobbyCheck*  
For the menus, I made a script called LobbyCheck. This script decides whether the player should see the main menu or the level select menu depending on if they are connected to Relay. It also moves the player to the correct spawn point in the lobby and makes sure only the host can pick levels, while clients have to wait.

<details>  
<summary>LobbyCheck Script</summary>   
  
![LobbyCheck Scrip](/LightBound_Together/Code/LobbyCheck_Script.png) 
</details>  

---  

#### *LevelCheck*  
I also wrote a script called LevelCheck which keeps track of which levels are unlocked using PlayerPrefs. It updates the menu buttons so players can only enter levels they’ve completed, and it requires at least two players to be connected before levels become interactable. It also syncs the menus when new clients join so everyone sees the same thing.

<details>  
<summary>LevelCheck Script</summary>   
  
![LevelCheck Scrip](/LightBound_Together/Code/LevelCheck_Script.png) 
</details>  

---  

#### *RelayManager*  
To actually get players connected, I made a RelayManager. This script handles hosting and joining games through Unity Relay. When hosting, it creates a Relay allocation and generates a join code that clients can use to connect. It also sets up Unity Transport (UTP) so Netcode for GameObjects can communicate properly through Relay. On top of that, I added feedback in the UI, like showing status text and the join code, so the process feels clear to the player.

<details>  
<summary>RelayManager Script</summary>   
  
![RelayManager Scrip](/LightBound_Together/Code/RelayManager_Script.png) 
</details>  

---  

#### *RelaySceneManager*  
For changing scenes, I created a RelaySceneManager. This makes sure only the host can load new levels and includes methods for starting the Tutorial, Level 1, and Level 2. It also handles quitting and leaving the game by shutting down Relay and sending players back to the menu when needed.

<details>  
<summary>RelaySceneManager Script</summary>   
  
![RelaySceneManager Scrip](/LightBound_Together/Code/RelaySceneManager_Script.png) 
</details>  

---  

#### *GameManager*  
Finally, I wrote a GameManager that ties everything together. It makes sure only two players can connect at once (one host and one client), and it updates the player count when someone joins or leaves. It also makes sure the host’s join code and level button states are shared with all clients. On top of that, it handles saving progress across the multiplayer session, like when the tutorial or a level is completed.

<details>  
<summary>GameManager Script</summary>   
  
![GameManager Scrip](/LightBound_Together/Code/GameManager_Script.png) 
</details>  

---  

##  *Menu UI*

####  *Main menu*
I made a very simple UI where the player can either host a game or connect as a client to a friend who is hosting by using a join code that the hosting player sees in their lobby.

Here’s how the relay menu looks:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/MainMenuUI.png" width="500" height="600" /></td>
  </tr>
</table>

---  

####  *Lobby menu*
This is how the hosting player sees the join code along with the 3D level selection menu. From here, the host can share the code with a friend and then start the levels once everyone is connected. 
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/Lobby3DUI.png" width="500" height="600" /></td>
  </tr>
</table>

To use the 3D menu I put a box collider that checks when the player is near the menu, where the grass stops in the picture above. This script unlocks the mouse and stops the camera from following the mouse while inside the collider, so the player can interact with the menu. When the player leaves the collider, the mouse is locked again and the camera goes back to following, making the transition between gameplay and menu smooth and automatic.
<details>  
<summary>Cursor script</summary>   
  
![Cursor script](/LightBound_Together/Code/LockCursor_Script.png) 
</details>  


To make it easier for the host to share the join code, I added a script that copies the randomized code directly to the clipboard when the player clicks on the code sign.
<details>  
<summary>Copy to Clipboard script</summary>   
  
![Copy to clipboard script](/LightBound_Together/Code/CopyToClipboard_Script.png) 
</details>  

---  

####  *Pause menu*
I also made a simple pause menu with the essentials: leaving the game or lobby, checking the controls, restart option in case the level bugs out and the option to go to settings where you can adjust the volume, camera speed and a toggle for fullscreen.

This is the script for the adjustable settings in the settings menu:
<details>  
<summary>SettingsManager script</summary>   
  
![SettingsManager script](/LightBound_Together/Code/SettingsManager_Script.png) 
</details>  

Here’s how the pause menu and controls looks like:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/PauseMenuUI.png" width="500" height="600" /></td>
    <td><img src="/LightBound_Together/Images/ControlsUI.png" width="500" height="600" /></td>
  </tr>
</table>

---

##  *Player*

After spending more than half the project building menus, fixing the lobby, and making sure the multiplayer connections worked, I realized I also had to create a ragdoll-based player. Since this was my first time making a real online multiplayer game and the project was only 8 weeks long, I didn’t have enough time to build a physics-based multiplayer character completely from scratch.

Instead, I bought an already working ragdoll player package (Image below) that was designed for singleplayer and then reworked it to function in multiplayer. This meant rewriting the way the physics were handled so that actions were sent to the server and synchronized across clients. When I first downloaded the package, only the local player could see the ragdoll movement, but after my changes both players could see and interact with the physics correctly.

<table>
  <tr>
    <td><img src="/LightBound_Together/Images/PhysicsPacakage.png" width="500" height="600" /></td>
  </tr>
</table>

---  

##  *Camera*
For the camera system, I used Unity’s Cinemachine package. I went with the FreeLook option and spent time tweaking the settings until I got the movement and feel I wanted. 
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/Camera_Asset.png" width="500" height="600" /></td>
  </tr>
</table>

Since the package didn’t include zoom by default, I also added my own zoom functionality to give players more control over the view.
<details>  
<summary>Camera zoom script</summary>   
  
![CameraZoom script](/LightBound_Together/Code/CameraZoom_Script.png) 
</details>  

I added the camera directly to the player prefab. To make sure only the local player keeps the camera (so multiple players don’t spawn multiple cameras in multiplayer), I wrote a small script that removes the camera for all non-local players and sets up the Cinemachine FreeLook camera to follow and look at the correct transform.
<details>  
<summary>Local player camera script</summary>   
  
![LocalPlayerCamera script](/LightBound_Together/Code/LocalCamera_Script.png) 
</details>  

---  

##  *Lightning*
Because Lightbound Together revolves around light and shadows, I decided to use Unity’s HDRP since it gives me the highest quality lighting, fog, and overall atmosphere. To achieve the look I wanted, I used a lot of light sources in my levels. For example, a single lantern uses six different lights to spread the glow evenly.

I know this isn’t the most performance-friendly approach, but I solved that by using a script that only renders what the camera actually sees, so the game doesn’t lag. If the lanterns had transparent materials, I could’ve achieved the same result with just one light in the center, but this setup gave me the best balance of visuals and functionality for now.

Lightsorces in level: 
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/LightSorcesInLevel.png" width="450" height="250" /></td> 
    <td><img src="/LightBound_Together/Images/FireflyLight_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

Point lights on gameobjects:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/LanternLight_Gif.gif" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/RespawnRockLight_Gif.gif" width="450" height="250" /></td> 
  </tr>
</table>

Volumetric directional lights for sky and moon:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/VolumetricSkyLight_Gif.gif" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/SkyLight_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

---  

##  *shadow shader*
What makes my game stand out from other co-op physics-based puzzle games is the light and darkness system. Instead of just solving puzzles, players also have to manage their survival — stepping outside the light causes the darkness to slowly consume them.

I made a DarknessController script that constantly checks if the player is close enough to a light source (i did this by adding colliders to every light sorce that fits the area of the light). If they are, the screen stays clear and safe. If they move away, a custom post-processing effect (the DarknessOverlay) begins to shrink the player’s “safe radius,” adding shadows, pulsing, and distortion that make the screen feel like it’s closing in. Stay in the darkness too long, and the screen fully closes, the player hears whispers, and they’re eventually killed and respawned at a spawn point.
<details>  
<summary>DarknessController script</summary>   
  
![DarknessController script](/LightBound_Together/Code/DarknessController_Script.png) 
</details>  

The DarknessOverlay itself is a custom post-processing volume I wrote. It handles all the visual parts of the effect (shrinking radius, opacity, wobble, pulse, and noise) to make the darkness feel alive and unsettling. The script is linked to a shader that applies these effects in real-time as the player moves in and out of the light.
<details>  
<summary>DarknessOverlay script</summary>   
  
![DarknessOverlay script](/LightBound_Together/Code/DarknessOverlay_Script.png) 
</details>  

The visual effect of the shadows creeping in looks like this:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/Shadow_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

---  

##  *Level design*
Since I only had 8 weeks for the whole project, I only had time to create one tutorial level to introduce the mechanics and one main level as a proper challenge. My focus was more on building the multiplayer systems, menus, and unique gameplay mechanics rather than producing a large number of levels.

####  *Tutorial*
In the tutorial I introduce the basic mechanics through simple challenges like jumping over logs and picking up pumpkins. To guide the player, I added floating text instructions in the world. These messages fade in when the player gets close and fade out when they move away, so they don’t clutter the screen.

<details>  
<summary>Text render range script</summary>   
  
![TextRenderRange script](/LightBound_Together/Code/TextRenderRange_Script.png) 
</details>  

<table>
  <tr>
    <td><img src="/LightBound_Together/Images/Tutorial_Gif.gif" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/TurorialComplete_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

---  

####  *Level 1*
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/PumpkinSpinner_Gif.gif" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/Wall_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

In Level 1 I added a few simple obstacles to test physics interactions across the network. Since this is a multiplayer game, I used ServerRPC calls to make sure all the physics-based events triggered by one player (like pushing or activating something) were correctly synchronized so the other player could see the same result. This let me test how reliable physics replication was in a real gameplay scenario.

####  *Obstacles in Level 1*
The first obstacle I added was two cauldrons that the players must fill with pumpkins in order to open a gate. This introduces teamwork and object handling since both players need to collect and carry pumpkins to progress.
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/PumpkinGate.png" width="450" height="250" /></td>
  </tr>
</table>

---  

Bridge Puzzle
The second obstacle is a cooperative bridge puzzle. One player has to carry a wooden plank and place it to build a bridge, while the other player holds a light to prevent both from being consumed by the darkness. When the bridge is finished, it leads to a pressure plate. By standing on it, one player raises another spinning bridge, allowing their partner to jump across the water and progress further into the level.

Images of the plank bridge, pressure plate and the spinning bridge:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/Bridge.png" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/SpinnerDown.png" width="450" height="250" /></td>
  </tr>
</table>
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/SpinnerUp.png" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/SpinnerUp2.png" width="450" height="250" /></td>
  </tr>
</table>

---

Breakable Wall
The next challenge is a destructible wall that can only be broken by applying enough force. I added this mechanic because many physics-based co-op games feature some form of breakable barrier, and I wanted to see if I could implement it myself. The wall reacts to strong impacts and eventually collapses, allowing the players to move forward.

Destructible wall & grabbable weapons to destroy the wall:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/Wall_Gif.gif" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/Destruction_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

---  

The final challenge of the level is a cooperative parkour section. One player must step on pressure plates that temporarily push stones out of the wall, creating platforms for the other player to climb. Each stone remains extended for only one second after the pressure plate is released. At the top, the climbing player can grab a lantern, which is then used to burn away the shadows blocking the cave entrance.
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/PressurePlate_Gif.gif" width="450" height="250" /></td>
    <td><img src="/LightBound_Together/Images/EndFire_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

---  

##  *Gameplay, physics & interactions*

---  

##  *Bugs and fixes*

---  
