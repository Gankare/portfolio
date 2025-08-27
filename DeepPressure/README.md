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

### *Haptics*
To make the grabbable objects feel more interactive, I added vibration feedback to the VR controller. When grabbing an object or pulling a lever, the controller vibrates, and the intensity of the vibration increases with the speed of the pull. This effect makes it feel much more like you’re actually dragging a lever in the real world.

Here are the Haptic scripts:

### *Hightlight*
