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

<details>  
<summary>SnapStarter script</summary>   
  
![SnapStarter Scrip](/VR_Party/Code/Menu/SnapStarter_Script.png) 
</details>  

I created the wires using a plugin called WireBuilder. [WireBuilder - nicogarcia.s.dev's website](https://www.patreon.com/posts/wirebuilder-1-0-77014259)
<table>
  <tr>
    <td><img src="/VR_Party/Images/Menu/WireBuilder.png" width="700" height="550" /></td>
  </tr>
</table>

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

Each minigame includes both a normal mode and a challenge mode, with the challenge mode designed to be slightly more difficult.

---

### *Basketball minigame*
#### *Normal mode*
The first minigame I created after building the menu was a basketball minigame. I wanted it to be simple but still offer a bit of challenge.

A Minigame script is placed on every minigame to handle the start, end, and scoring logic, ensuring each game integrates consistently with the overall system.

<details>  
<summary>Basketball minigame script</summary>   
  
![Minigame Script](/VR_Party/Code/Basketball/BasketMiniGame_Script.png) 
</details> 

I started by creating spheres to serve as basketballs and made them grabbable using the Oculus Grabbable Interactable component. I then wrote scripts to handle scoring and added a particle effect to play whenever a goal was made.

<details>  
<summary>Goal script</summary>   
  
![BasketHit Script](/VR_Party/Code/Basketball/BasketHit_Script.png) 
</details> 

Since real basketball hoops have nets, I downloaded a net model and applied Unity’s Cloth component, which simulates fabric-like behavior. To achieve a realistic effect, I enabled continuous collision and adjusted the constraint points by setting different maximum distances. As shown in the image below, red points are locked with zero movement, while green points are more flexible, creating progressively looser constraints toward the bottom of the net.

Finally, I added a collision detection script to the net. When a basketball touches the net, the script reduces the ball’s velocity to replicate the realistic slowdown of hitting a basketball net.

<details>  
<summary>Cloth net script</summary>   
  
![ClothNetTrigger Script](/VR_Party/Code/Basketball/ClothNetTrigger_Script.png) 
</details> 

Once I received the finalized models from the artists, I integrated them into the project, resulting in this:
<table>
  <tr>
    <td><img src="/VR_Party/Images/Basketball/NetWeight.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Basketball/BasketballPrefab.png" width="385" height="350" /></td>
  </tr>
</table>

I wrote a script that automatically returns basketballs to the stand two seconds after hitting the ground.
<details>  
<summary>Return basketball script</summary>   
  
![ReturnBasketball Script](/VR_Party/Code/Basketball/ReturnBasketball_Script.png) 
</details> 

I also created a bounce sound script, which plays a sound whenever the ball collides with an object. The volume scales with the impact force, making collisions feel more realistic and dynamic, with harder bounces producing louder sounds.
<details>  
<summary>Bounce sound script</summary>   
  
![BounceSoundTrigger Script](/VR_Party/Code/Basketball/BounceSoundTrigger_Script.png) 
</details> 

<table>
  <tr>
    <td><img src="/VR_Party/Images/Basketball/BasketNormal_Gif.gif" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Basketball/BasketBallBounce_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*
To make the basketball minigame more challenging, I positioned the hoop farther away from the player at the start. Additionally, the hoop changes position every time it’s hit, preventing players from getting too comfortable with a single spot.

<details>  
<summary>Change pos script</summary>   
  
![BasketChangePos Script](/VR_Party/Code/Basketball/BasketChangePos_Script.png) 
</details> 

<table>
  <tr>
    <td><img src="/VR_Party/Images/Basketball/BasketChallenge1_Gif.gif" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Basketball/BasketChallenge2_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Color match minigame*
#### *Normal mode*

<details>  
<summary>Colormatch minigame script</summary>   
  
![ColorMatchMiniGame Script](/VR_Party/Code/ColorMatch/ColorMatchMiniGame_Script.png) 
</details> 

The ColorMatch Minigame challenges players to adjust RGB values using physical levers until a cube matches a randomly generated target color shown on a sphere above it. I built the system using two core scripts that work together to handle color input, feedback, and scoring.

#### *SetObjectRandomColor script*
This script handles the goal system and scoring, At the start of each round, it generates a random target color and displays it on the sphere. It then continuously compares the player’s cube color to the target. If the difference is below a set threshold: the player gets points, a particle effect and sound are triggered for feedback, a new target color is generated, and scoring is temporarily locked to prevent spamming.

<details>  
<summary>SetObjectRandomColor script</summary>   
  
![SetObjectRandomColor Script](/VR_Party/Code/ColorMatch/SetObjectRandomColor_Script.png) 
</details> 

#### *LeverColorControl script*
This script is for the levers, each lever in the minigame controls a single color channel (R, G, or B). The lever’s rotation angle is read every frame. That angle is mapped to a 0–1 range using Mathf.InverseLerp. The corresponding color channel of the material is updated in real time.

This system allows players to physically interact with the levers and directly control how much red, green, or blue is added to the cube object.

<details>  
<summary>LeverColorControl script</summary>   
  
![LeverColorControl Script](/VR_Party/Code/ColorMatch/LeverColorControl_Script.png) 
</details> 

#### *DisplayColorInfo script* 
In normal mode, I added UI meters to show how far each lever has been pulled, making it easier for players to see how much of each RGB channel they’ve applied.

The script retrieves the current material color from the player’s cube, normalizes the R, G, and B values between 0.00 and 1.00, rounds them for readability, and displays them in TextMeshPro fields, as shown in the GIFs below.

<details>  
<summary>DisplayColorInfo script</summary>   
  
![DisplayColorInfo Script](/VR_Party/Code/ColorMatch/DisplayColorInfo_Script.png) 
</details> 

<table>
  <tr>
    <td><img src="/VR_Party/Images/ColorMatch/ColorMeter.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/ColorMatch/ColorMatchNormal_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*
To make the ColorMatch minigame more challenging, I reduced the color similarity threshold between the cube and the target sphere, requiring players to be more precise with their RGB adjustments. I also removed the UI meters that displayed lever positions, making it progressively harder for players to match the colors accurately.
<table>
  <tr>
    <td><img src="/VR_Party/Images/ColorMatch/ColorMatchPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/ColorMatch/ColormatchChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Slingshot minigame*
#### *Normal mode*
<details>  
<summary>SlingShot minigame script</summary>   
  
![SlingShotMiniGame Script](/VR_Party/Code/SlingShot/SlingShotMiniGame_Script.png) 
</details> 

This minigame was the most challenging to develop. Creating a satisfying and intuitive slingshot that feels good to use was not easy, but I can confidently say that I successfully achieved it.

I developed a modular system of scripts to handle ammo snapping, aiming, shooting, scoring, and respawning, making the gameplay smooth and immersive.

#### *Ammo handling*
The AutoSnapAmmo and ToggleSlingSnap scripts manage snapping the ammo to the slingshot, allowing players to transition seamlessly from loading to shooting without needing to release their grab. These scripts enable or disable the snap interactable and grab logic depending on whether ammo is available. 

Ammo is loaded using a Snap Zone on the slingshot, and each ammo object must have a Snap Interactor component for this system to work. This setup ensures smooth interactions, letting the player pick up ammo, snap it to the slingshot, and shoot in one motion.

<details>  
<summary>AutoSnapAmmo script</summary>   
  
![AutoSnapAmmo Script](/VR_Party/Code/SlingShot/AutoSnapAmmo_Script.png) 
</details> 

<details>  
<summary>ToggleSlingSnap script</summary>   
  
![ToggleSlingSnap Script](/VR_Party/Code/SlingShot/ToggleSlingSnap_Script.png) 
</details> 

The ReturnAmmo script ensures ammo return to their original position after hitting the ground or a can, ready for reuse.

<details>  
<summary>ReturnAmmo script</summary>   
  
![ReturnAmmo Script](/VR_Party/Code/SlingShot/ReturnAmmo_Script.png) 
</details> 

---

#### *Shooting and aiming*
The AimSlingShoot script calculates the slingshot’s pull amount based on how far the player stretches the rubber band, which is implemented using a LineRenderer. The player aims by dragging a grabbable collider constrained to a set positions shown in the image below, allowing movement only backwards, up, and down. The pull distance determines the launch force of the projectile.

<table>
  <tr>
    <td><img src="/VR_Party/Images/SlingShot/AimConstraints.png" width="385" height="350" /></td>
  </tr>
</table>

When the pull exceeds a defined threshold, the projectile is launched with a force proportional to the pull distance. If the pull does not exceed the threshold, the slingshot automatically returns to its starting position while keeping the ammo loaded, allowing the player to try again without needing to reload.

<details>  
<summary>AimSlingShoot script</summary>   
  
![AimSlingShoot Script](/VR_Party/Code/SlingShot/AimSlingShoot_Script.png) 
</details> 

The ReturnAim script handles the visual line renderer for the slingshot and smoothly returns the slingshot to its resting position after release. The linerenderer follows the grabb interactable object making it look like you are draging the line. 

<details>  
<summary>ReturnAim script</summary>   
  
![ReturnAim Script](/VR_Party/Code/SlingShot/ReturnAim_Script.png) 
</details> 

The SnapGrabController script, attached to each ammo object, ensures that the correct interactor is used when grabbing the slingshot.

<details>  
<summary>SnapGrabController script</summary>   
  
![SnapGrabController Script](/VR_Party/Code/SlingShot/SnapGrabController_Script.png) 
</details> 

---

#### *Scoring and cans*
The CanHit script handles collisions between cans and ammo or the ground. It plays audio feedback, awards points, and tracks whether each can has fallen. 

<details>  
<summary>CanHit script</summary>   
  
![CanHit Script](/VR_Party/Code/SlingShot/CanHit_Script.png) 
</details> 

The RespawnObjectGroup script manages groups of cans, automatically resetting them once all have been knocked down, ensuring continuous gameplay. This script is used exclusively in normal mode, where cans are organized into groups.

<details>  
<summary>RespawnObjectGroup script</summary>   
  
![RespawnObjectGroup Script](/VR_Party/Code/SlingShot/RespawnObjectGroup_Script.png) 
</details> 

The aiming/pulling of the slingshots grab interactable includes a threshold that triggers an force release of the grab when the player pulls the slingshot all the way back. This means the entire action can be completed in a single grab: the player picks up the ammo, brings it near the slingshot, and pulls back to shoot—all in one smooth motion. This design creates a seamless and highly satisfying interaction, eliminating the need for manual release. as I hope you can se in this Gif:
<table>
  <tr>
    <td><img src="/VR_Party/Images/SlingShot/SlingshotNormalPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/SlingShot/SlingShotNormal_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*
To make the Slingshot minigame more challenging, I arranged the cans one by one instead of stacking them as in normal mode, requiring the player to aim more precisely. Additionally, I increased the points awarded—the farther the cans are, the more points the player earns.
<table>
  <tr>
    <td><img src="/VR_Party/Images/SlingShot/SlingshotChallengePrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/SlingShot/SlingShotChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Egg-knife minigame*
#### *Normal mode*
At this stage of the project, I was balancing several responsibilities: updating the main menu, assisting other programmers with their minigames, updating all maps with shaders and models, and developing my own minigames. Therefore I wanted to create something quick but fun, I drew inspiration from a childhood game where you balance an egg on a spoon and race from one point to another without dropping it. Since our minigames were limited to one minute, I adapted the idea into a version where the goal is to place as many eggs as possible into a basket within the time limit.

The challenge with using a spoon model was achieving accurate collision so the egg would sit naturally inside the spoon. This required a non-convex Mesh Collider, but the One Grab Physics Joint Transformer component—which we applied to all grabbable objects to ensure realistic physics and prevent clipping—does not support non-convex colliders. To overcome this limitation, I redesigned the gameplay: instead of a spoon, the player uses two knives like chopsticks to move the eggs into the basket. This solution maintained the fun and skill-based challenge while avoiding the collider restriction.

Vissual reason why i did not use a spoon: 

This displays the error if using non convex mesh collider and the spoon collider if using the a convex collider:
<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/ErrorSpoon.png" width="800" height="500"/></td>
  </tr>
</table>
<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/SpoonCollider.png" width="800" height="500" /></td>
  </tr>
</table>

<details>  
<summary>EggKnife minigame script</summary>   
  
![EggKnifeMinigame Script](/VR_Party/Code/EggKnife/EggKnifeMinigame_Script.png) 
</details> 

#### *EggAddScore script*
Handles scoring when an egg enters the basket. It awards points, triggers a particle effect for feedback, and calls the ReturnEgg script to reset the egg.

<details>  
<summary>EggAddScore script</summary>   
  
![EggAddScore Script](/VR_Party/Code/EggKnife/EggAddScore_Script.png) 
</details> 

#### *ReturnEgg script*
Resets the egg to its starting position when it collides with either the basket or the ground. It also restores its physics state so the egg can be reused smoothly.

<details>  
<summary>ReturnEgg script</summary>   
  
![ReturnEgg Script](/VR_Party/Code/EggKnife/ReturnEgg_Script.png) 
</details> 


The knifes looks a bit laggy because I was recording and playing at the same time. Eggknife is not my proudest work, it's kinda wonky but still fun to play.
<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeNormalPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeNormal1_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*
to make the EggKnife minigame more challenging, I redesigned the map by removing the edges that previously prevented eggs from falling, and I raised the basket height to require both horizontal and vertical movement. I also added eyes to the eggs and made them jump randomly as if they were alive. These changes made the gameplay more fun and challenging at the same time.

<details>  
<summary>RandomJump script</summary>   
  
![RandomJump Script](/VR_Party/Code/EggKnife/RandomJump_Script.png) 
</details> 

<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeChallengePrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

Epic trickshot:
<table>
  <tr>
    <td><img src="/VR_Party/Images/EggKnife/EggKnifeChallenge2_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

### *Sort minigame*
#### *Normal mode*
The sort minigame is also simple, balls spawn with random colors and the player’s goal is to place as many balls as possible into their corresponding colored bowls within the time limit.

<details>  
<summary>Sort minigame script</summary>   
  
![SortMiniGame Script](/VR_Party/Code/Sort/SortMiniGame_Script.png) 
</details> 

#### *BowlColorAddScore script*
This script is attached to each bowl, it detects when balls enter the trigger area. Uses a color enum to identify the bowl’s color and checks the ball’s tag for a match. If a ball matches the bowl color, it calls the BallController script to deactivate the ball, award a point and remove the ball from play. This system ensures that only correctly matched balls contribute to the player’s score.

<details>  
<summary>BowlColorAddScore script</summary>   
  
![BowlColorAddScore Script](/VR_Party/Code/Sort/BowlColorAddScore_Script.png) 
</details>

#### *BallController script*
Attached to each ball, this script manages interaction and scoring. When a ball enters the correct bowl, it is deactivated to prevent double scoring. The script also disables the ball’s collider and grab interaction, ensuring players cannot repeatedly score with the same ball.

<details>  
<summary>BallController script</summary>   
  
![BallController Script](/VR_Party/Code/Sort/BallController_Script.png) 
</details>

#### *SpawnBalls script*
This script manages spawning of balls during the minigame. Spawns batches of balls at a set interval and within a defined area around a central spawn point. Randomly selects ball prefabs from a list, allowing multiple colors.

<details>  
<summary>SpawnBalls script</summary>   
  
![SpawnBalls Script](/VR_Party/Code/Sort/SpawnBalls_Script.png) 
</details>

<table>
  <tr>
    <td><img src="/VR_Party/Images/Sort/SortNormalPrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Sort/SortNormal_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

#### *Challenge Mode*
To make the Sort minigame more challenging, I increased the variety of ball colors beyond the number of bowls and raised the ball spawn rate. This fast-paced gameplay overwhelms the player with balls, many of which are the wrong colors, making the experience both intense and challenging.

<table>
  <tr>
    <td><img src="/VR_Party/Images/Sort/SortChallengePrefab.png" width="385" height="350" /></td>
    <td><img src="/VR_Party/Images/Sort/SortChallenge_Gif.gif" width="385" height="350" /></td>
  </tr>
</table>

---

## *Cel Shader(maps & minigames)*
At the start of the project, our team decided that the game should have a colorful, cartoon style, so we opted to use a cel shader. a cel shader creates a stylized, cartoon-like look by using discrete bands of color for shadows instead of smooth gradients. Typically, it applies two or more distinct shades to define lighting and shadow, giving objects a bold, graphic appearance.

My mission was to use the cel shader to create a variety of materials and apply them across the game’s maps. I also placed models and configured post-processing settings to define the overall visual style, ensuring the game had a cohesive, colorful, and stylized look. 

As shown in the minigames above, I applied the cel shader to all of them. Additionally, I added an outline effect to every material using the cel shader, enhancing the cartoony, stylized look of the game.

---

#### *Jump castle map*
Left image is what I started with and right is the final look when shader and game platoe is added:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/CastleMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/CastleMap.png" /></td>
  </tr>
  <table>

These settings is placed on every map, setting the spawnpoint and type of map. Scripts explained further down:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/CastleSettings.png" /></td>
  </tr>
</table>

---

#### *Lake forest map*
These are the models I got from the artists and also the settings for this map:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/ForestMapModels.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/ForestSettings.png" /></td>
  </tr>
</table>

Left image is what I started with and right is the final look:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/ForestMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/ForestLakeMap.png" /></td>
  </tr>
</table>

---

#### *Mesa normal & water map*
This map evolved into two versions: the original map and a water-themed variant. For the water version, I added blue post-processing, a semi-transparent water layer above and air bubbles particles. Resulting in the effect of being submerged underwater.

The map foundation and models I got from the artists:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/DesertMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/DesertMapModels.png" /></td>
  </tr>
  <table>

Final look for both versions of the map:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/DesertMap.png" /></td> 
    <td><img src="/VR_Party/Images/MapSelect/WaterMap.png" /></td>
  </tr>
</table>

---

#### *Room map*
You can't se much difference on these pictures but basically I had to recreate all the materials for all the models in this room and like the other maps i put out spawnpositions and added the right settings. When playing, you notice that everything has outlines but this pictures where taken to far away to display that.

Left image is what I started with and right is the final look:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/RoomMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/RoomMap.png" /></td>
  </tr>
  <table>

---

#### *Moon map*
For this map I created a little universe around the moon with the planet models. I also used postprocessing on this map prefab to make it feel more like you are in space. If you have seen this map on the gameplay Gifs above, the post processing was of on those Gifs. The images below displays how it looks when postprocessing is on.

I also added a rotation script to all the planets with a adjustable speed, so they rotate a different speeds making it feel like the enviroment is more alive.

The map and models I got from the artists:
<table>
  <tr>
    <td><img src="/VR_Party/Images/MapSelect/MoonMapOld.png" /></td>
    <td><img src="/VR_Party/Images/MapSelect/MoonMapModels.png" /></td>
  </tr>
  <table>

It's hard to show in images but when playing in VR it looks really good.

Final look of the map from different angles:
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
To control which maps each minigame could be played on, and to define the spawn points or game plateaus where the player appears, I created a map management system built around three core scripts.

#### *RandomMapSpawner* 
This script randomly selects and spawns a map from a predefined list so you can have different maps for different minigames, this script is placed on the minigame prefabs.

<details>  
<summary>RandomMapSpawner script</summary>   
  
![RandomMapSpawner Script](/VR_Party/Code/MapSelect/RandomMapSpawner_Script.png) 
</details>

#### *MapSpawnPoints* 
The script handles player spawn locations within each map, picking a random point from multiple options. You can have how many spawn positions as you like, in this project each map had between 1 and 4.

<details>  
<summary>MapSpawnPoints script</summary>   
  
![MapSpawnPoints Script](/VR_Party/Code/MapSelect/MapSpawnPoints_Script.png) 
</details>

#### *MapIdentifier* 
This script labels each map with its type (e.g., Castle, Forest, Desert, Water) so other systems know which one is active, this is used for music in this project so that a music script checks what map type it is and from a list chooses a song that fits that map.

<details>  
<summary>MapIdentifier script</summary>   
  
![MapIdentifier Script](/VR_Party/Code/MapSelect/MapIdentifier_Script.png) 
</details>

Together, these scripts ensure that maps are flexible, randomized, and reusable across different minigames.

