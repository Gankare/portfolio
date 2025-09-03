# ScrapBattle  
![ScrapBattle_Title](/ScrapBattle/Images/ScrapYard.png)  
## *A brief game description*

**Scrapbattle** was meant to be a VR robot fighting game where you build your own robot in a scrapyard and then battle other robots to earn new and better parts. The idea was inspired by the TV series Robot Wars.

We didn’t get that far in development though, so for now it’s more of a “build-a-robot simulator.” Still, the core concept was there, and the building system laid the groundwork for what could have become full robot battles.

---

## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

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

## *Expanding The Building System*

i mostly worked on making the building system, making the parts fit well together with snapzones 

## *Level Design*

---

## *New Parts System*

---

## *Arena & Driving*
