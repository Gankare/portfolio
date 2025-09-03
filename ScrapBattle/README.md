# ScrapBattle  
![ScrapBattle_Title](/ScrapBattle/Images/ScrapYard.png)  
## *A brief game description*

**Scrapbattle** is a VR 

---

## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---

## *Stat System*
I built a dynamic, easy-to-use system where every robot part has its own stats. Each part is defined as a ScriptableObject, which determines the model, description, and stats for that specific piece.

There are four different part types:

Core – the essential starting block that every robot must have. It’s the foundation you build on.

Body Parts – extensions that let you expand your robot’s structure.

Wheels – every robot needs four wheels to function as a base.

Weapons – parts with stats like damage, used for combat.

The goal was to have every part with its own HP. When a part takes enough damage, it falls off. If the core is destroyed, then the entire robot is destroyed as well.

Unfortunately, we didn’t get far enough for the system to be fully playable, but the foundation for modular robot building was in place.

Here are the scripts for the ScriptableObjects: 
<details>  
<summary>Hightlight Script</summary>   
  
![Button haptic script](/DeepPressure/Code/HoverHighlight_Script.png) 
</details>  

---

## *Expanding The Building System*

i mostly worked on making the building system, making the parts fit well together with snapzones 

## *Level Design*

---

## *New Parts System*

---

## *Arena & Driving*
