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
This little project was mainly for practicing VR game development. We did a couple of projects like this while working at VR World. Not many people at this internship were motivated to work, so I ended up doing most of this and the other projects myself.

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

i mostly worked on making the building system, making the parts fit well together with snapzones 

---

## *Level Design*
I designed a scrapyard environment using the limited assets provided by the artists (such as a scrap pile) and supplemented it with a few downloaded models, like cars.

I began by creating and shaping the terrain, applying a worn, dirty texture to set the atmosphere. To populate the scene, I placed scrap piles of varying sizes. While the assets were limited and a bit repetitive, I worked around this by adding large scrap mounds in the distance and using fog to create depth and disguise repetition.

To bring the environment to life, I added cars, rats, and a temporary scrap crane I built out of simple shapes while waiting for the artists to deliver a proper model. I also integrated a bird system that makes the scene feel much more dynamic — birds fly around and occasionally land on the scrap piles or the crane, adding movement and realism.

It looks like this:
<table>
  <tr>
    <td><img src="/ScrapBattle/Images/Environment1.png.png" width="500" height="450" /></td>
    <td><img src="/ScrapBattle/Images/Environment2.png" width="500" height="450" /></td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="ScrapBattle/Images/Environment3.png" width="500" height="450" /></td>
    <td><img src="/ScrapBattle/Images/Environment4.png" width="500" height="450" /></td>
  </tr>
</table>

This is the picture i was trying to replicate: 

---

## *Crane*


<table>
  <tr>
    <td><img src="/ScrapBattle/Images/DropParts_Gif.gif" width="500" height="450" /></td>
  </tr>
</table>

### *New Parts System*

---

## *Arena & Driving*
