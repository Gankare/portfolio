# *VR Party*
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/MenuClose.png" /></td>
  </tr>
</table> 
[VR Party Demo Trailer](https://www.youtube.com/watch?v=arceBJsaVkI)   

## *Game description*  

**VR Party** Is a local multiplayer VR game designed to bring fast-paced fun and competition into one headset. Players take turns completing a series of one-minute minigames, each aiming to rack up the highest score before passing the headset to the next challenger.

The game features a variety of minigames ranging from familiar challenges like basketball and slingshot target shooting to more unique ones such as piloting a zeppelin through rings. Each minigame can be played with different difficulties and game modes, keeping the experience fresh and adaptable to any group.

Since only one person plays at a time, there’s no player limit—making VR-Party perfect for groups of any size. The simple format, combined with quick rounds and escalating tension, makes every session a mix of lighthearted fun and serious competition to see who comes out on top.

---

## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---

## *Arcade Machine Menu System*
#### *Guns and Interaction*
For the VR Party menu, I used an arcade machine model provided by our artists. Players interact with it using two guns attached to the machine. Each gun fires a raycast from its tip: when a player grabs a gun and aims at the canvas on the arcade screen, a beam is emitted from the gun’s point. A Graphic Raycaster on the canvas detects these "shots" as clicks, allowing players to interact with the UI.

<details>  
<summary>Gun interaction script</summary>   
  
![GunMenu Scrip](/VR_Party/Code/Menu/GunMenu_Script.png) 
</details>  

Picture of the models i got and what i made from it:
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/OldArcadeMachine.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Menu/MenuClose.png" width="385" height="350" /></td>
  </tr>
</table>

The guns are grabbable objects with a fixed hand pose, ensuring they are always held correctly when picked up. Each gun starts in a Snap Interactable gun holder and can be snapped back into place at any time when released near or above the holder. The guns are also connected to the arcade machine using joints that act like wires, so the guns can never completely leave the machine. 

I created the wires using a plugin called WireBuilder. [WireBuilder - nicogarcia.s.dev's website](https://www.patreon.com/posts/wirebuilder-1-0-77014259)
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/WireBuilder.png" width="700" height="550" /></td>
  </tr>
</table>

<details>  
<summary>SnapStarter script</summary>   
  
![SnapStarter Scrip](/VR_Party/Code/Menu/SnapStarter_Script.png) 
</details>  

Initially, players could move the guns too far, causing the wires to glitch. To prevent this, I implemented a distance check script. If a gun exceeds the maximum allowed distance from the machine, it is forcefully released from the player’s hand, causing it to drop, as shown in the GIF below.

<details>  
<summary>GunAreaLimit script</summary>   
  
![GunAreaLimit Scrip](/VR_Party/Code/Menu/GrabAreaLimit_Script.png) 
</details> 

The red gizmo circles is how far you can pull a gun without it getting dropped:
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/MenuPistolRange.png" width="385" height="350" /></td>
     <td><img src="/VR_Party/Images/Menu/MenuPistolRange_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Player System*
Players enter their names on the arcade screen using a custom virtual keyboard I made. Names are displayed in a player list, and duplicate names are not allowed. Supports any number of players.

When the Add Player button is pressed, the PartyManager is triggered, visually instantiating a UI player prefab and adding a new player with the chosen name to the game system. The player data is then saved using PlayerPrefs. Using PlayerPrefs, keeps the setup persistent between sessions.

<details>  
<summary>Keyboard activator script, when inputfield is pressed</summary>   
  
![VirtualKeyboardActivator Script](/VR_Party/Code/Menu/VirtualKeyboardActivator_Script.png) 
</details>  

<details>  
<summary>Keyboard key script used on every key</summary>   
  
![Keyboard Scrip](/VR_Party/Code/Menu/KeyboardKey_Script.png) 
</details>  

<details>  
<summary>PartyManager script, responsible for the game menus</summary>   
  
![PartyManager Script](/VR_Party/Code/Menu/PartyManager_Script.png) 
</details>  

<details>  
<summary>SceneDirector script</summary>   
  
![SceneDirector Script](/VR_Party/Code/Menu/SceneDirector_Script.png) 
</details>  

<details>  
<summary>Visual name script on the UI prefab</summary>   
  
![Name Script](/VR_Party/Code/Menu/AddUIPlayer_Script.png) 
</details>  


#### *Game Modes*
Once a minimum of two players has been added, a game can start. The PartyManager script handles game initialization: after a mode is selected, the UI locks to prevent further changes, and a fade animation plays using a black canvas image transition. The PartyManager then checks if Challenge Mode is active and triggers the corresponding SceneDirector function to load the appropriate level. 

Available modes on the arcade machine: Party Mode, Tournament Mode, Practice Mode, and Challenge Modes, which are harder versions of the main modes.
Once a minimum of two players is added, a game can be started. 

#### *Settings*
The menu also includes a settings screen where players can adjust music and ambient audio with sliders. The sliders connect to Unity’s AudioMixer, so changes happen instantly. Settings are also stored with PlayerPrefs, and there’s an option to reset everything to default values.

<details>  
<summary>Settings script</summary>   
  
![SettingsMenu Script](/VR_Party/Code/Menu/SettingsMenu_Script.png) 
</details>  

<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/MenuSettings_Gif.gif" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Menu/MenuAddPlayer_Gif.gif" width="385" height="350" /></td>
  </tr>
</table> 

---

## *My miniGames*
The following section showcases the minigames I designed and programmed on my own. While I collaborated on other minigames, here I focus only on the projects where I was fully responsible for the implementation.

---

### *Basketball minigame*
#### *Normal mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/Basketball/BasketballPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Basketball/NetWeight.png" width="385" height="350" /></td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="/VR_Party/Images/Basketball/BasketNormal_Gif.gif" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Basketball/BasketBallBounce_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/Basketball/BasketChallenge1_Gif.gif" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Basketball/BasketChallenge2_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Color match minigame*
#### *Normal mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/ColorMatch/ColorMeter.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/ColorMatch/ColorMatchNormal_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/ColorMatch/ColorMatchPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/ColorMatch/ColormatchChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Slingshot minigame*
#### *Normal mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/SlingShot/SlingshotNormalPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/SlingShot/SlingShotNormal_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/SlingShot/SlingshotChallengePrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/SlingShot/SlingShotChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Egg-knife minigame*
#### *Normal mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeNormalPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeNormal1_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeChallengePrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeChallenge1_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Sort minigame*
#### *Normal mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/Sort/SortNormalPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Sort/SortNormal_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*

<table>
  <tr>
    <td><img src="/VR_Party/Images/Sort/SortChallengePrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Sort/SortChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

## *Cel Shader(maps & minigames)*

#### *Jump castle map*
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/CastleMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/CastleMap.png" /></td>
  </tr>
  <table>
    
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/CastleSettings.png" /></td>
  </tr>
</table>

#### *Lake forest map*
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/ForestMapModels.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/ForestSettings.png" /></td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/ForestMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/ForestLakeMap.png" /></td>
  </tr>
</table>

#### *Mesa normal & water map*
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/DesertMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/DesertMapModels.png" /></td>
  </tr>
  <table>
    
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/DesertMap.png" /></td> 
    <td><img src="/VR_Party/Images/MapSelect/WaterMap.png" /></td>
  </tr>
</table>

#### *Room map*
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/RoomMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/RoomMap.png" /></td>
  </tr>
  <table>

  #### *Moon map*
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/MoonMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/MoonMapModels.png" /></td>
  </tr>
  <table>

  <table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/MoonMap1.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/MoonMap2.png" /></td>
  </tr>
  <table>

  <table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/MoonMap3.png" /></td>
  </tr>
  <table>
    
---

## *Map selector*
