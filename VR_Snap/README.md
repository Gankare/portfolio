# *VR Snap*
<table>
  <tr>
    <td><img src="/VR_Snap/Images/Camera_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

## *Game description*  

**VR Snap** is a VR photography simulator.

---

## *My contributions to this project*

All the features have been implemented by me. 

---  

##  *Why i made this game*

During my internship at VR World, we had a Christmas break where we were free to create whatever we wanted. I took the opportunity to dive deeper into VR by experimenting with a character model that mirrors the player’s body.

I’ve always been interested in making a “creature snap” style game, where players explore the world, photograph different animals, and collect their discoveries in a scout book or journal. To test the idea, I created a small demo centered around building a functional VR camera system. The experiment was successful, and I was surprised by how straightforward it was to implement.

---  

##  *Player*

At first, I wanted to create a virtual body that mimicked real-life movements with locomotion. I experimented with different plugins and 3D models, trying to make the legs move naturally with the body instead of staying still while only the upper body moved. Using Body Tracking Joint Set, I managed to get the legs to move forward when the upper body reached a certain distance away from the leg joints. However, the movement didn’t match my real legs and looked awkward.

###  *Scaling*
During this process, I also realized that the 3D model was larger than my actual body. To fix this, I made it a priority to ensure the avatar would always scale to the player’s real-world size. I tested a component called Retargeting Layer from the Meta Movement plugin, which allowed me to dynamically scale the rigged 3D model to the player’s height in real time.

If I remember correctly, the script included a listener that checked for changes in height and recalculated the model’s scale accordingly, both at the start and whenever significant differences were detected.

The Real time scaling looks like this, from sitting to standing:
<table>
  <tr>
    <td><img src="/VR_Snap/Images/Scale_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

###  *Locomotion*


---  

##  *Polaroid camera*


