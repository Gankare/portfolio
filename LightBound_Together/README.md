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
I also made a simple pause menu with the essentials: leaving the game or lobby, checking the controls, adjusting settings like volume and camera speed, and a restart option in case the level bugs out.

Here’s how the pause menu and controls looks like:
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/PauseMenuUI.png" width="500" height="600" /></td>
    <td><img src="/LightBound_Together/Images/ControlsUI.png" width="500" height="600" /></td>
  </tr>
</table>

---

##  *Player*

---  

##  *Camera*

---  

##  *shadow shader*

---  

##  *Physics & interactions*

---  

##  *Level design*

---  

##  *Environment & Lightning*

---  

##  *Bugs and fixes*

---  
