# ScrapBattle  
![ScrapBattle_Title](/ScrapBattle/Images/ScrapYard.png)  
## *A brief game description*

**Scrapbattle** was meant to be a VR robot fighting game where you build your own robot in a scrapyard and then battle other robots to earn new and better parts. The idea was inspired by the TV series Robot Wars.

We didn’t get that far in development though, so for now it’s more of a “build-a-robot simulator.” Still, the core concept was there, and the building system laid the groundwork for what could have become full robot battles.

---

## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---

## *Why this demo was made*
This little project was mainly for practicing VR game development. We did a couple of projects like this while working at VR World. Not many people at this internship were motivated to work, so I ended up doing most of the work on this and the other projects myself.

---


## *Stat System*
I built a dynamic, easy-to-use system where every robot part has its own stats. Each prefab part has the Part script, which determines the Part Type with Part Data, description and stats for that specific piece.

It can look like this in the inspector:
<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Core_Inspector.png" width="500" height="600" /></td>
  </tr>
</table>

There are four different part types:

Core – the essential starting block that every robot must have. It’s the foundation you build on.

Body Parts – extensions that let you expand your robot’s structure, no added stats.

Wheels – every robot needs four wheels to function as a base.

Weapons – parts with stats like damage, used for combat.

The goal was to have every part with its own HP. When a part takes enough damage, it falls off. If the core is destroyed, then the entire robot is destroyed as well.

Unfortunately, we didn’t get far enough for the system to be fully playable, but the foundation for modular robot building was in place.

Here are the scripts for the ScriptableObjects: 
<details>  
<summary>PartData scriptableobject</summary>   
  
![PartData scriptableobject](/ScrapBattle/Code/PartData_ScriptableObjectScript.png) 
</details>  

<details>  
<summary>Part script</summary>   
  
![Part script](/ScrapBattle/Code/Part_Script.png) 
</details>  

<details>  
<summary>Core Part script</summary>   
  
![CorePart script](/ScrapBattle/Code/CorePart_Script.png) 
</details>  

<details>  
<summary>Body Part script</summary>   
  
![BodyPart script](/ScrapBattle/Code/BodyPart_Script.png) 
</details>  

<details>  
<summary>Wheel Part script</summary>   
  
![WheelPart script](/ScrapBattle/Code/WheelPart_Script.png) 
</details>  

<details>  
<summary>Weapon Part script</summary>   
  
![WeaponPart script](/ScrapBattle/Code/WeaponPart_Script.png) 
</details>  

---

## *Visual stats text*
To show stats to the player, I created a text display that follows the camera and appears when you hover over a part with the VR controller.

<details>  
<summary>Hover show script</summary>   
  
![Hover show script](/ScrapBattle/Code/ShowStatText_Script.png) 
</details>  

<details>  
<summary>Text script</summary>   
  
![Text script](/ScrapBattle/Code/StatToText_Script.png) 
</details>  

This is how it looks ingame:
<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Core_Stats.png" width="500" height="450" /></td>
    <td><img src="/ScrapBattle/Images/Wheel_Stats.png" width="500" height="450" /></td>
  </tr>
</table>

---

## *Expanding The Building System*

We already had a basic system for assembling parts, but it wasn’t optimized for the components we were using. I spent most of my time refining the building system. Some parts can only be placed in specific locations — for example, wheels attach to the blue connectors while other parts go on the red ones, as shown in the picture below. I focused on making all parts fit together seamlessly using snap zones and created prefabs for each component with the correct stats.
<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Connections.png" width="500" height="450" /></td>
  </tr>
</table>

---

## *Level Design*
I designed a scrapyard environment using the limited assets provided by the artists (such as a scrap pile) and supplemented it with a few downloaded models, like cars.

I began by creating and shaping the terrain, applying a worn, dirty texture to set the atmosphere. To populate the scene, I placed scrap piles of varying sizes. While the assets were limited and a bit repetitive, I worked around this by adding large scrap mounds in the distance and using fog to create depth and disguise repetition.

To bring the environment to life, I added cars, rats, and a temporary scrap crane I built out of simple shapes while waiting for the artists to deliver a proper model. I also integrated a bird system that makes the scene feel much more dynamic — birds fly around and occasionally land on the scrap piles or the crane, adding movement and realism.

It looks like this:
<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Environment1.png" width="500" height="450" /></td>
    <td><img src="/ScrapBattle/Images/Environment2.png" width="500" height="450" /></td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Environment3.png" width="500" height="450" /></td>
    <td><img src="/ScrapBattle/Images/Environment4.png" width="500" height="450" /></td>
  </tr>
</table>

This is the picture i was trying to replicate: 

<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Inspiration Environment.jpg" width="500" height="450" /></td>
  </tr>
</table>

---

## *Crane*
The crane’s purpose was to deliver parts to the player. If a part was thrown away, the crane would return it. We never developed the game far enough to include robot fights, but the idea was that the crane would also deliver all new parts to the player after each battle.

Since we didn’t have a proper model yet, I built a temporary crane by reshaping simple cubes and animating it to deliver parts.

Here are the scripts for bringing back parts that have been thrown away:
<details>  
<summary>Crane drop script</summary>   
  
![CraneDrop script](/ScrapBattle/Code/CraneDrop_Script.png) 
</details>  

<details>  
<summary>Part respawn script</summary>   
  
![PartRespawn script](/ScrapBattle/Code/PartRespawn_Script.png) 
</details>  

<details>  
<summary>Part out of map script</summary>   
  
![PartOutOfMap script](/ScrapBattle/Code/PartOutOfMap_Script.png) 
</details>  

And here’s how it looks in action, delivering the parts:
<table>
  <tr>
    <td><img src="/ScrapBattle/Images/DropParts_Gif.gif" width="500" height="450" /></td>
  </tr>
</table>

---

## *Saving the build*
I set up a two-phase building and deployment system for the robots. Each part had two prefabs: one used during the building phase, and one “real” version used when deploying the robot. On every buildable part, I added a script called SavePartData, which stores the part’s local position, rotation, and a reference to its real prefab.

When the robot is deployed, the RobotManager script goes through all the parts I placed, calculates their offsets, and instantiates the real prefabs under a single parent object. This makes the robot act as one complete machine, while each part is still its own GameObject. I also added logic for requirements, like making sure the robot has at least four wheels before it can be deployed.

The result was a system where you can build robots freely in the editor-like building phase, and then instantly switch into gameplay mode with a functional, unified robot that you can drive around in the arena.

<details>  
<summary>Save part data script</summary>   
  
![SavePartData script](/ScrapBattle/Code/SavePartData_Script.png) 
</details> 
  
<details>  
<summary>RobotManager script</summary>   
  
![RobotManager script](/ScrapBattle/Code/RobotManager_Script.png) 
</details>  

---

## *Arena & driving*
With about a day left in the project, we still didn’t have any driving gameplay, so I put together a small pit arena and quickly prototyped a movement system to let the player control their robot.

I wrote a RobotController script that uses Unity’s Input System to read joystick input and apply it to the robot’s Rigidbody. The script handles acceleration, deceleration, and smooth velocity changes with Lerp, so the robot doesn’t start and stop abruptly. It also aligns movement to the camera’s forward and right directions, letting the player steer relative to their view. To keep the robot stable, I constrained its Rigidbody rotations and adjusted the center of mass.

On top of that, I made a WheellMovement script for visuals. It checks the robot’s velocity and, if it’s moving, plays particle effects and simple wheel animations. When the robot stops, the effects and animations stop too, giving the movement a more lively and reactive feel. One issue I ran into was that the wheels on one side were rotated the wrong way, causing the animations and particles to play in the opposite direction. Unfortunately, I didn’t have time to fix this before the project deadline.

<details>  
<summary>Robot controller script</summary>   
  
![RobotController script](/ScrapBattle/Code/RobotController_Script.png) 
</details>  

<details>  
<summary>Wheel Spinning Animation script</summary>   
  
![Wheel script](/ScrapBattle/Code/WheelAnimation_Script.png) 
</details>  

The system worked as a basic prototype, but not exactly as I had envisioned. My goal was to restrict the robot to only move forward with more natural, non-instant turning, but I ran out of time to refine those mechanics. Here is how it looks driving the robot:

<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Driving_Gif.gif" width="500" height="450" /></td>
  </tr>
</table>
