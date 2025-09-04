# Tama Sim
<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/MRTama.png" width="500" height="450" /></td>
  </tr>
</table> 

## *A brief game description*

**Tama Sim** is a VR simulator I developed together with a graphic design student as an experiment in mixed reality (MR). The game is inspired by Tamagotchi, reimagined in VR. Players care for a virtual pet by feeding it, playing with it, and cleaning up after it.

The better care you provide, the faster the pet grows. Once it fully evolves, you can choose to start over with a new pet. Neglecting the pet slows its growth, and if ignored for too long, it can even die. To add variety, each pet spawns with a random color, giving every playthrough a slightly different feel.

---
## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---

## *Scanning the room for mixed reality(MR)*

---

## *Offline*
I created a time and evolution system for a virtual pet. The ElapsedTime script is the largest script I wrote and is responsible for handling all the pet’s offline behavior. It tracks how long the pet has been alive, even when the game is closed, and updates its growth and evolution stages based on real-world time.

<details>  
<summary>ElapsedTime script</summary>   
  
![ElapsedTime script](/Tamagotchi_Sim/Code/ElapsedTime_Script.png) 
</details>  

Here’s what the system does:

Persistent time tracking – Uses DateTimeOffset and PlayerPrefs to save the last exit time and calculate how much real time has passed since the player last played.

Pet growth & evolution – Increases the pet’s age over time, with modifiers based on factors like hunger, poop count, and whether the pet has been played with. The pet progresses through different stages (egg → child → teen → adult).

Visual updates – Activates and positions the correct pet stage model and applies a saved/randomized color to the pet’s material.

Alive time display – Continuously updates the UI with a formatted string showing how many days, hours, and minutes the pet has been alive.

Adult check – When the pet reaches adulthood, it tracks how long it stays alive as an adult and triggers an event (like spawning a new pet) if it survives for 24 hours.

Data saving – Periodically saves pet stats (age, alive time, colors, etc.) so the pet’s state is always preserved between sessions.

Reset system – Provides a full reset of the pet’s stats, timers, and colors when starting fresh.

This script essentially makes the pet feel alive outside of play sessions, evolving and growing in real time, just like a digital Tamagotchi.

---

## *Online*

---

## *Feeding and eating*

---

## *Pooping and cleaning up*

---

## *Playing and petting*

---

## *Fur shader*
