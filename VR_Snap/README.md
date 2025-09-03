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

---  

###  *Locomotion*
I was using the Meta Movement plugin so that the player’s 3D model would mimic their real-world movements. This worked fine, except when moving with the joystick. In that case, the player’s body would just stand still while only the camera moved.

I couldn’t simply place the player model directly under the camera, because then when the camera rotated, the body would rotate twice as much and you’d end up seeing your own body from inside.

To fix this, I wrote a simple script that updates the player model’s position to match the camera’s position every frame (in the Update function).

<details>  
<summary>Model rig to camera script</summary>   
  
![RigToPlayer Script](/VR_Snap/Code/ModelFollow_Script.png) 
</details>  

Since the legs don’t animate when moving with the joystick, I decided to change the body’s texture to a hologram effect. That way it makes more sense visually, since it looks like you’re floating around instead of walking.

To help reduce motion sickness, I added a tunneling effect using vignetting in post-processing. It fades in while you’re moving, and for a test, I think it turned out pretty well. Just keep in mind that the vignette looks stronger in the GIF than it actually does inside the headset.

This is what it looks like while walking around:
<table>
  <tr>
    <td><img src="/VR_Snap/Images/LocoMotion_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

---  

##  *Polaroid camera*


