# VR Tamagotchi simulator
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
To build a mixed reality experience for Oculus, I used Meta’s MR Utility Kit plugin and learned how to integrate it into Unity.

The workflow works like this:

First, the player scans their real-world room, which is visualized like this:
<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/RoomScan_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

Once the scan is complete, the plugin provides access to the effect mesh script used for the floor, ceiling, and other surfaces.

This script generates mesh colliders in Unity that match the player’s real environment.

The meshes can be given temporary materials (like colors) for testing, and then made invisible once everything is working correctly.

This effectively creates an MR room inside Unity, allowing digital objects to interact with the player’s physical space.
<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/MRUK.png" width="500" height="450" /></td>
    <td><img src="/Tamagotchi_Sim/Images/EffectMesh.png" width="500" height="450" /></td>
  </tr>
</table> 

Once the colliders are generated, I added a NavMesh Surface so that the AI pet could navigate and walk around the player’s real room.

Finally, I used another script included in Meta’s MR Utility Kit called “Find Spawn Positions.” This script checks the scanned meshes and spawns prefabs at valid locations. For example, in the picture below, the system is spawning the pet’s offline poop on surfaces like the floor, table, couch, or bed.

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/Navmeshsurface.png" width="500" height="450" /></td>
    <td><img src="/Tamagotchi_Sim/Images/FindSpawnPositions.png" width="500" height="450" /></td>
  </tr>
</table> 


---

## *Online & offline*
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

## *Menu UI*
I added a main menu with instructions, This way, new players could quickly understand the core gameplay loop (feeding, cleaning, playing, and evolving the pet) without needing extra guidance.
it looks like this: 

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/Menu_Instructions.png" width="500" height="450" /></td>
  </tr>
</table> 

---

## *Ingame UI*
I designed and implemented the ingame UI system to support all the core gameplay states. The UI itself is kept simple, since my main goal was to make the gameplay work smoothly in VR — and the system fully supports that. It’s split into three scripts:  

#### *UIManager*

Central hub for UI-related gameplay interactions.

Spawns interactive objects near the player (food, a broom for cleaning, a ball for playing).

Manages special game states such as pet death and acquiring a new pet, showing the correct canvases and disabling the VR menu when needed.

Formats and displays how long the pet lived before death.

<details>  
<summary>UIManager script</summary>   
  
![UIManager script](/Tamagotchi_Sim/Code/UIManager_Script.png) 
</details>    

---

#### *VRMenuToggle*

Controls how the in-game menu is opened in VR.

Supports two input methods for accessibility: pressing the Start button on the left controller, or performing a pinch gesture with the left hand.

Includes a cooldown to prevent accidental double activations.

Keeps track of whether the menu is currently active and whether it can be opened at all (e.g., disabled during death/new pet states).

<details>  
<summary>VRMenuToggle script</summary>   
  
![VRMenuToggle script](/Tamagotchi_Sim/Code/MenuToggle_Script.png) 
</details>    

---

#### *DisplayAliveTime*

Lightweight helper script for displaying the pet’s total “time alive” using TextMeshPro.

Connects directly with the pet’s growth system so the timer updates in real-time as the pet lives and evolves.

<details>  
<summary>DisplayAliveTime script</summary>   
  
![DisplayAliveTime script](/Tamagotchi_Sim/Code/DisplayAliveTime_Script.png) 
</details>  


This is how the ingame UI menu looks: 

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/Ingame_Menu.png" width="500" height="450" /></td>
  </tr>
</table> 

---

The game offers you a fresh start with a new pet, either after your pet has fully grown and a day has passed, or when it has starved to death.

This is how the new pet menus look: 

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/NewPet_Menu.png" width="500" height="450" /></td>
    <td><img src="/Tamagotchi_Sim/Images/Starved_Menu.png" width="500" height="450" /></td>
  </tr>
</table> 

---

## *Feeding and eating*
I implemented a food and hunger system to manage the pet’s wellbeing both online and offline. The system is split across three scripts:

#### *PetHungerManager*

Tracks the pet’s hunger, food consumption, and survival.

Calculates how much food the pet should have eaten while the player was away and updates hunger status accordingly.

Handles thresholds for hunger and death, triggering the death UI if the pet starves.

<details>  
<summary>HungerManager script</summary>   
  
![HungerManager script](/Tamagotchi_Sim/Code/HungerManager_Script.png) 
</details>  

---

#### *SpawnFood*

Handles spawning and tracking food in the game world.

Ensures the food bowl never exceeds a maximum number of pieces.

Supports spawning food both at the start of the game and when the player adds more food during gameplay.

Manages saving and loading the current food count using PlayerPrefs so the pet’s food state persists between sessions.

<details>  
<summary>SpawnFood script</summary>   
  
![SpawnFood script](/Tamagotchi_Sim/Code/SpawnFood_Script.png) 
</details>  

---

#### *EatFood*

Detects when the pet collides with food and triggers the eating process.

Plays a sound effect and updates the last time the pet ate.

Implements a short cooldown to prevent eating the same food repeatedly too quickly.

<details>  
<summary>EatFood script</summary>   
  
![EatFood script](/Tamagotchi_Sim/Code/EatFood_Script.png) 
</details>  

I designed it this way so that the pet behaves realistically, eating over time and reacting to the player’s actions, while keeping offline behavior in mind. This made the pet feel alive and required the player to actively feed it to grow and survive.

At the start of this GIF, you can see how food spawns in the bowl: 

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/MR_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

---

## *Playing and petting*
In the GIF above, you can see the two main ways to interact with the TamaPet: petting it and playing catch.

The petting and playing scripts are similar to the food system in that they track interactions and manage the pet’s state over time, including offline behavior. Unlike food, these scripts don’t consume a resource. Instead, they update whether the pet has been played with and trigger animations, particle effects, and physics-based interactions. Petting makes the pet react happily, while playing catch uses the ball’s physics so the pet can fetch it, giving immediate visual and interactive feedback that makes the pet feel alive.

Here are the scripts used for playing with the pet:

<details>  
<summary>PlayManager script</summary>   
  
![PlayManager script](/Tamagotchi_Sim/Code/PlayManager_Script.png) 
</details>  

<details>  
<summary>PetPet script</summary>   
  
![PetPet script](/Tamagotchi_Sim/Code/PetPet_Script.png) 
</details>  

<details>  
<summary>BallPhysics script</summary>   
  
![BallPhysics script](/Tamagotchi_Sim/Code/ThrowBall_Script.png) 
</details>  

---

## *Pooping and cleaning up*
The poop system manages the pet’s waste, adding another layer of care beyond hunger and play. The GeneratePoop script keeps track of how many poops exist, handles offline spawning based on the last time the pet pooped, and limits the total number of poops in the room. It also provides a function to clean up poops, updating the saved data.

<details>  
<summary>GeneratePoop script</summary>   
  
![GeneratePoop script](/Tamagotchi_Sim/Code/GeneratePoop_Script.png) 
</details> 

---

The AddNewPoop script handles the timed spawning of new poops while the game is running, placing them behind the pet at a set interval. Together, these scripts make the pet feel more alive by creating ongoing responsibilities for the player, like feeding and cleaning, without being tied to direct player actions like eating or playing.
 
<details>  
<summary>AddNewPoop script</summary>   
  
![AddNewPoop script](/Tamagotchi_Sim/Code/AddNewPoop_Script.png) 
</details>  

---

In this GIF you can see how the player can spawn a broom and clean up the pet’s waste:

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/VRCatch_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

Here is an image containing all the prefabs I created for the Tamagotchi simulator:

<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/Prefabs.png" width="500" height="450" /></td>
  </tr>
</table> 

---

## *Pet AI*
I implemented the PetAI script to give the pet autonomous behavior, making it feel alive and responsive in the virtual environment. The AI is built around a simple state machine with states like Idle, Wandering, Eating, Sleeping, Fetching, and Returning.

Key points of how it works:

State Machine: The pet switches between different states based on timers, hunger, or player interaction. For example, it wanders when idle, moves to food when hungry, and goes to sleep periodically.

Navigation: I used Unity’s NavMeshAgent to move the pet around the environment, with random wandering positions and stuck detection to prevent it from getting trapped.

Fetch Mechanics: When the player throws a ball, the pet switches to Fetching, moves toward the ball, picks it up using a small offset, and then returns it to the player. During this, it disables physics on the ball to avoid glitches and re-enables it when returned.

Animations & Effects: Animations like walking and happy triggers are tied to states, and a particle system plays when the pet successfully interacts or completes an action like returning the ball.

Integration with Other Systems: It interacts with my other gameplay systems, such as the play system (PetPlayManager) and food system, so that its actions are meaningful and influence the game state.

Overall, this script makes the pet feel like a dynamic character, reacting both to the environment and player input, while keeping the AI behavior simple and predictable for VR interactions.

<details>  
<summary>PetAI script</summary>   
  
![PetAI script](/Tamagotchi_Sim/Code/PetAI_Script.png) 
</details>  

---

## *Fur shader*
The pet models I got from the artist were untextured and had no eyes, which made them look a bit plain in VR. To improve their appearance, I reused a fur shader from a previous project and applied it to the models. I also created simple eyes using spheres with a reflective smooth metal material. Together, this gave the pets a soft, furry look and made them feel much more alive and visually appealing in the mixed reality environment.

Before:
<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/Original_Models.png" width="500" height="450" /></td>
  </tr>
</table> 

After: 
<table>
  <tr>
    <td><img src="/Tamagotchi_Sim/Images/Fur.png" width="500" height="450" /></td>
  </tr>
</table> 
