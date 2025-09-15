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

##  *Multiplayer plugins*
For the multiplayer system in my Unity project, I chose to use Netcode for GameObjects (NGO) combined with Unity Relay.
<table>
  <tr>
    <td><img src="/LightBound_Together/Images/NGO_Asset.png" width="500" height="600" /></td>
    <td><img src="/LightBound_Together/Images/Relay_Asset.png" width="500" height="600" /></td>
  </tr>
</table>

#### *Netcode for GameObjects: *  
I picked NGO because it is Unity’s first-party networking solution designed to work directly with GameObjects, which made it a natural fit for my project. It handles core multiplayer features like spawning, ownership, and synchronization of objects across clients. Since my game is built with a GameObject workflow rather than DOTS/ECS, NGO provided a straightforward and well-integrated way to add multiplayer functionality.

#### *Unity Relay: *  
Relay works together with NGO by solving the issue of direct peer-to-peer connections. Normally, players behind NAT or firewalls cannot host or join easily. Relay lets clients connect to a Unity-hosted server endpoint that forwards traffic between players. This way, I didn’t need to set up or pay for dedicated servers, but players could still connect to each other reliably. Relay doesn’t simulate or run game logic itself – it only routes the traffic – which means it pairs perfectly with NGO’s networking layer.

#### *Smooth Sync: *  
To improve the player experience, I added Smooth Sync, which interpolates and predicts the movement of networked objects. NGO provides the base synchronization, but Smooth Sync makes the motion appear much smoother and responsive by reducing visible latency and jitter. This was important in my project since player movement and interactions needed to feel natural.

<table>
  <tr>
    <td><img src="/LightBound_Together/Images/SmoothSync_Asset.png" width="500" height="600" /></td>
    <td><img src="/LightBound_Together/Images/MultiplayerTools_Asset.png" width="500" height="600" /></td>
  </tr>
</table>

Together, NGO handles the multiplayer logic, Relay ensures players can always connect, and Smooth Sync makes everything feel fluid. No extra plugins are strictly required beyond these, though Unity also offers Lobby (for matchmaking) and Vivox (for voice chat) if you want to expand functionality further.

---  

##  *Networking*

---  

##  *Player*

---  

##  *Physics & interactions*

---  

##  *Menus*

---  

##  *Lighting & shadow shader*

---  

##  *Camera*

---  

##  *Level design*

---  

##  *Bugs and fixes*

---  
