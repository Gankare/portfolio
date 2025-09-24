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
For the menu in VR Party, I used the arcade machine I got from our artists, players interact using two guns attached to the machine. The guns work as raycasters, so when you grab one and aim it at the canvas placed on the arcade screen it shoots out a linerenderer that looks like a beam from the guns point. A Graphic Raycaster on the canvas detects clicks when the guns are fired.

Picture of the model i got and what i made from it:
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/OldArcadeMachine.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Menu/MenuClose.png" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Guns and Interaction*

The guns are grabbable objects with a fixed hand pose, so when picked up they’re always held the right way. They’re connected to the arcade machine with joints acting like wires, so the player can move them around but never pull them completely away.

To make sure the guns stay in place, I wrote a script that checks if a gun moves too far from the arcade machine, this is done with a distance check script. If the gun goes past the limit, it force releases from the player’s hand as you can see in the Gif below. 

The red gizmo circles is how far you can pull a gun without it getting dropped:
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/MenuPistolRange.png" width="385" height="350" /></td>
     <td><img src="/VR_Party/Images/Menu/MenuPistolRange_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Player System*
Players enter their names on the arcade screen using a custom virtual keyboard I made. Names are displayed in a player list, and duplicate names are not allowed.

Supports any number of players.

Player names and total count are saved using PlayerPrefs, keeping the setup persistent between sessions.

#### *Game Modes*
Once a minimum of two players is added, a game can start. The PartyManager script handles game initialization:
UI locks after mode selection to prevent further changes.
A fade animation plays using a black canvas transition.
The PartyManager checks if Challenge Mode is active and triggers the corresponding SceneDirector function to load the level.

Available modes on the arcade machine:
Party Mode 
Tournament Mode 
Practice Mode 
Challenge Modes – harder versions of the main modes.

#### *Settings*

The menu also includes a settings screen where players can adjust music and ambient audio with sliders. The sliders connect to Unity’s AudioMixer, so changes happen instantly. Settings are also stored with PlayerPrefs, and there’s an option to reset everything to default values.

<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/MenuSettings_Gif.gif" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Menu/MenuAddPlayer_Gif.gif" width="385" height="350" /></td>
  </tr>
</table> 

---

<details>  
<summary>Menu example script</summary>   
  
![Menu Script](/) 
</details>  

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
