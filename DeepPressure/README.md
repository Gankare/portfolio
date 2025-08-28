# Deep pressure  
![Deep Pressure_Title](/DeepPressure/Images/Fishes_Gif.gif)  
## *A brief game description*

**Deep Pressure** is a VR submarine simulator that traps you in a failing vessel deep beneath the sea. Navigate dark caves filled with creatures, mines, and jagged rocks while balancing fragile systems as crushing pressure threatens to implode the sub.

---
## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---
## *Building the Submarine*
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
## *Levers and Buttons*

### *Hightlight*
I added highlights to the interactable objects in the submarine to make it clearer for the player which items can be used. Since the environment contains a lot of wires, buttons, and other non-interactable details, the highlights help reduce confusion and guide the player’s attention to what actually matters. I implemented this by casting a ray from each controller. If the ray hits an object with the Highlight script attached, that object lights up. The highlight system itself comes from an asset, which I integrated into the project.
<details>  
<summary>Hightlight Script</summary>   
  
![Button haptic script](/DeepPressure/Code/HoverHighlight_Script.png) 
</details>  
The highlight looks like this:
<table>
  <tr>
    <td><img src="/DeepPressure/Images/HighLight_Gif.gif" width="450" height="250" /></td>
  </tr>
</table>

---  

### *Haptics & Object Interaction*
To make the grabbable objects feel more interactive, I added vibration feedback to the VR controller. When grabbing an object or pulling a lever, the controller vibrates, and the intensity of the vibration increases with the speed of the pull on the levers. This effect makes it feel much more like you’re actually dragging a lever in the real world.

### *Button*
The button visually presses down when pushed, giving it a clear physical response. Using UnityEvents, we can easily assign actions to the button directly in the editor. I added haptic feedback when the button is pressed to the controller pressing.
<details>  
<summary>Button script</summary>   

![Button haptic script](/DeepPressure/Code/Button_Script.png) 
</details>  

---  

### *Engine & Pressure Lever*
To simplify hand interactions with the levers, I added the GetHand script to both controllers. This way, it’s easier to determine which hand is responsible for each interaction.   
<details>  
<summary>GetHand script</summary>   

![GetHand script](/DeepPressure/Code/GetHand_Script.png) 
</details>  

I first created the lever script for the engine lever. Later, when I needed a pressure lever, I duplicated the original script and modified it to fit the new functionality. While both scripts are quite similar since they share the same lever mechanics, they work differently and therefore remain separate. The original script, currently named Lever, would be more accurately called EngineLever, as it specifically controls the engine lever, while the pressure lever script is responsible for lowering pressure, which in turn affects the gauge.

<details>  
<summary>Lever Script</summary>   
  
![Lever Script](/DeepPressure/Code/LeverHaptics_Script.png) 
</details>  

<details>  
<summary>Pressure Scripts</summary>   
  
![Lever Script](/DeepPressure/Code/LeverHaptics_Script.png) 
</details>  

