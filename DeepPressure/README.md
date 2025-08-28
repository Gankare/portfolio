# Deep pressure  
![Fishes](/DeepPressure/Images/Fishes_Gif.gif)  
## *A brief game description*

**Deep Pressure** is a VR submarine simulator that traps you in a failing vessel deep beneath the sea. Navigate dark caves filled with creatures, mines, and jagged rocks while balancing fragile systems as crushing pressure threatens to implode the sub.

---
## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---
## *Building the submarine*
I started building the submarine using a rusty barrel and other worn-out models like pipes, spotlights, and doors. The exterior didn’t look great, but since the player would only see the interior, that wasn’t a big concern.

However, I ran into a problem: the barrel’s texture only looked good with a specific shader, which wasn’t compatible with VR. To solve this, I had to rethink my approach. I installed the ProBuilder plugin and rebuilt the submarine’s body from scratch, giving me full control over the shape and structure. Once the base was done, I added all the rusty details—doors, pipes, wires, and electrical components—to give the interior that worn, industrial look.

The first prototype looked like this: 
<table>
  <tr>
    <td><img src="/DeepPressure/Images/FirstPrototype.png" /></td>
    <td><img src="/DeepPressure/Images/FirstPrototype2.png" /></td>
  </tr>
</table>

Then after using ProBuilder the final product looks like this: 

<table>
  <tr>
    <td><img src="/DeepPressure/Images/SubFromOutside.png" /></td>
    <td><img src="/DeepPressure/Images/Room1.png" /></td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="/DeepPressure/Images/Room2.png" /></td>
    <td><img src="/DeepPressure/Images/Wires.png" /></td>
  </tr>
</table>

---

## *Door interaction*

The submarine has two rooms, and I wanted the player to easily move between them. When hovering over the door and pressing the trigger on the controller, the player teleports to the other side.
<details>  
<summary>Door Interact Script</summary>   
  
![Door Teleport script](/DeepPressure/Code/DoorTeleport_Script.png) 
</details>  
The teleport looks like this:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/DoorTeleport_Gif.gif" width="500" height="450" /></td>
  </tr>
</table>

---

## *Levers and buttons*

### *Hightlight*
I added highlights to the interactable objects in the submarine to make it clearer for the player which items can be used. Since the environment contains a lot of wires, buttons, and other non-interactable details, the highlights help reduce confusion and guide the player’s attention to what actually matters. I implemented this by casting a ray from each controller. If the ray hits an object with the Highlight script attached, that object lights up. The highlight system itself comes from an asset, which I integrated into the project.
<details>  
<summary>Hightlight Script</summary>   
  
![Button haptic script](/DeepPressure/Code/HoverHighlight_Script.png) 
</details>  
The highlight looks like this:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/HighLight_Gif.gif" width="500" height="450" /></td>
  </tr>
</table>

---  

### *Haptics & object interaction*
To make the grabbable objects feel more interactive, I added vibration feedback to the VR controller. When grabbing an object or pulling a lever, the controller vibrates, and the intensity of the vibration increases with the speed of the pull on the levers. This effect makes it feel much more like you’re actually dragging a lever in the real world.

### *Button*
The button visually presses down when pushed, giving it a clear physical response. Using UnityEvents, we could easily assign actions to the button directly in the editor. I added haptic feedback when the button is pressed to the controller pressing.
<details>  
<summary>Button script</summary>   

![Button haptic script](/DeepPressure/Code/Button_Script.png) 
</details>  

---  

### *Engine & pressure lever*
To simplify hand interactions with the levers, I added the GetHand script to both controllers. This way, it’s easier to determine which hand is responsible for each interaction.   
<details>  
<summary>GetHand script</summary>   

![GetHand script](/DeepPressure/Code/GetHand_Script.png) 
</details>  

I created a script to force-release the controller’s grab on levers when they are pulled too far away. This prevents players from controlling a lever from unrealistic distances, like from another room.
<details>  
<summary>PullDistance Script</summary>   

![PullDistance script](/DeepPressure/Code/PullDistance_Script.png) 
</details>  

---  
#### *Engine lever*
Firstly I created the lever script for the engine lever. Later, when I needed a pressure lever, I duplicated the original script and modified it to fit the new functionality. While both scripts are quite similar since they share the same lever mechanics, they work differently and therefore remain separate. The original script, currently named Lever, would be more accurately called EngineLever, as it specifically controls the engine lever, while the pressure lever script is responsible for lowering pressure, which in turn affects the gauge.

This script handles the engine lever’s behavior, including haptic feedback when the lever is pulled
<details>  
<summary>Lever Script</summary>   
  
![Lever Script](/DeepPressure/Code/LeverHaptics_Script.png) 
</details>  

Shutting off the engine stops the submarine because it is damaged, and it also turns off the lights. This gives the player the ability to power down the submarine, take a breather, and perform tasks in other room. Additionally, a monster attacks the submarine randomly. The only way to defend against it is to turn off the sub when the monster is nearby; otherwise, the monster will destroy it.

Here is what both turning off the engine and the monster destroying the submarine look like:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/LightsOff_Gif.gif" width="385" height="250" /></td>
    <td><img src="/DeepPressure/Images/Tentacle_Gif.gif" width="385" height="250" /></td>
  </tr>
</table>

---  

#### *Pressure lever*
This script handles the pressure lever’s behavior, including haptic feedback when the lever is pulled
<details>  
<summary>Pressure Lever Script</summary>   
  
![Pressure Lever Script](/DeepPressure/Code/PressureLeverHaptic_Script.png) 
</details>  

---  

This script manages the pressure value, gradually increasing it when the lever is not being pulled. If the pressure rises too high, it triggers warning signals, can cause pipes to burst one by one, and eventually destroy the powerbox, ultimately leading to the submarine imploding if left uncontrolled. This creates a dynamic system.
<details>  
<summary>Pressure Script</summary>   
  
![Pressure Script](/DeepPressure/Code/Pressure_Script.png) 
</details>  
Here’s a visual of the pipes and electric box failing and being destroyed:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/Gas_Gif.gif" width="500" height="350" /></td>
  </tr>
</table>

---  

The Lower Pressure script quickly reduces the system’s pressure when the lever is pulled, simulating a rapid release.
<details>  
<summary>Lower Pressure Script</summary>   
  
![Lower Pressure Script](/DeepPressure/Code/LowerPressure_Script.png) 
</details>  

This is what lowering the pressure from a critical stage looks like:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/HighPressure_Gif.gif" width="500" height="450" /></td>
  </tr>
</table>

---  

## *Pixel shader*

Shaders in VR can be a bit tricky. Camera shaders that work on PC often don’t function properly in a VR build. Initially, I wanted to use a shader like this one I tried:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/TryingShader.png" width="500" height="450" /></td>
  </tr>
</table>

To solve this, I found a pixel shader that can be applied to objects and placed a screen that follows the camera with this pixelated filter applied. This creates the effect of a pixelated shader on the entire view, making it look like the scene itself has a pixelated shader. 

It works like this, but I keep it at a high resolution so the pixelation doesn’t look too blocky. The pixelated effect is visible in the other GIFs, giving the scene a subtle retro feel. I haven’t seen many VR games use this style, so this was also a test to see if pixelation would cause motion sickness. My conclusion: it doesn’t make you dizzy.
<table>
  <tr>
    <td><img src="/DeepPressure/Images/PixelShader_Gif.gif" /></td>   
  </tr>
</table>

---  

## *Grab haptics*
I added several grabbable objects, such as a lantern and bottles. The bottles are purely decorative, while the lantern can be used to improve visibility when the submarine’s engine is off. To enhance the tactile feel of grabbing, I added haptic feedback to the grab function.

This script was implemented toward the end of the project. I based it on the lever haptics script and modified it to trigger only once per grab. While some variable names were not updated due to time constraints, the functionality works as intended. If the project had been longer, I would have gone back to clean up all the names for clarity.

<details>  
<summary>Grab Haptics Script</summary>   
  
![Grab Haptics Script](/DeepPressure/Code/GrabHaptics_Script.png) 
</details>  

<table>
  <tr>
    <td><img src="/DeepPressure/Images/Lantern.png" /></td>  
    <td><img src="/DeepPressure/Images/Bottles.png" /></td>  
  </tr>
</table>

---  

## *Enviroment*

When the game was nearly complete, the map still felt barren. As a final touch, I added a variety of random corals and rocks scattered across the entire map to make it feel more alive.

It looks like this:

<table>
  <tr>
    <td><img src="/DeepPressure/Images/Corals.png" /></td>   
    <td><img src="/DeepPressure/Images/SubLights.png" /></td>   
  </tr>
</table>
<table>
  <tr>
    <td><img src="/DeepPressure/Images/Coral1.png" /></td>   
    <td><img src="/DeepPressure/Images/Coral2.png" /></td>   
  </tr>
</table>
