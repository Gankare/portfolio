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

##  *Why I made this game*

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

You can pick up the camera with one hand, but it takes both hands to activate it and take pictures. I also added a snap zone on the player’s side so you can holster the camera and walk around without holding it.

The model itself isn’t meant to be a Polaroid — it’s a modern camera — but I made Polaroid-style pictures come out of it. I think it looks funny, but also pretty cool.

Here’s how it works: if the player is holding the camera with two hands and presses the trigger, a picture spawns and animates outward from the center of the camera. If you take another picture, the previous one is detached from the camera and gravity is applied so it falls away.

The Polaroid photo itself isn’t just a random texture — the camera model actually has its own in-game camera. When you take a shot, it captures that camera’s view, turns it into a texture, and applies it to a 3D object representing the photograph. This makes each picture a real snapshot of what the in-game camera sees.

I also added a sound effect and a quick flash of light when a picture is taken, although the flash is a bit hard to notice in the game’s bright environment.

All the scripts are below, along with a GIF showing the camera functionality:
<details>  
<summary>Polaroid script</summary>   
  
![Polaroid Script](/VR_Snap/Code/Polaroid_Script.png) 
</details>  

<details>  
<summary>Photo script</summary>   
  
![Photo Script](/VR_Snap/Code/Photo_Script.png) 
</details>  

<details>  
<summary>Physics script</summary>   
  
![Physics Script](/VR_Snap/Code/Physics_Script.png) 
</details>  

<details>  
<summary>Sound script</summary>   
  
![Sound Script](/VR_Snap/Code/Sound_Script.png) 
</details>  

<table>
  <tr>
    <td><img src="/VR_Snap/Images/PolaroidPicture_Gif.gif" width="500" height="450" /></td>
  </tr>
</table> 

