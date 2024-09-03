# *Frostfall*

![Frostfall Jumpscare](/Frostfall/Images/Jumpscare.png)   

[Indiedb page](https://www.indiedb.com/games/frostfall)   
[Repository Link](https://github.com/Gankare/FrostfallHorrorGame)  

## *A brief game description*  

**Frostfall** Is a single player horror game located in a snowy forest at night. Your car ran out of fuel and with only a lighter, you have to search the woods for fuel.  
A wendigo roams the woods and is not happy to see you, you can run but you can not hide.  
Gather fuel and fill the car up, when you have a full tank you can escape the woods and survive the night.  

---

## *My contributions to this project*

All the features have been implemented by me. 

---  

## - Player  

The player controller blueprint is pretty basic, nothing changed with the movement. I Added a pickup and drop for the fuelcans, flickering for the lighter that the player holds and also a pause game button.  Link for the code: [Player blueprint](https://blueprintue.com/blueprint/ydhxzuci/)   
### True first person character & camera   
I decided to go with a third person template instead of a first person template when starting my project because I wanted a true first person (where the player is able to see their own body).  

I used a megascan 3D character model for the player and socketed the camera to the head, adjusted the fov and camera wobble when the player walks.   
![Player](/Frostfall/Images/Player.png)  

### Lighter  

I downloaded a lighter model and living candles from the unreal store. Then I socketed the lighter to the player's hand and socketed the living flame from the candles to the lighter. I set three different pointlights and one spotlight around the player and lighter, I also added flickering to the strongest pointlight called "FlameLight" in "Event Beginplay", in the player blueprint.

It looks like this:  
![Flame](/Frostfall/Images/Flame.gif)  
### Fuel  
I took this oilcan from megascans and made the texture emissive to glow in the dark, making it clear that the can is an interanctable object.    
 <img src="/Frostfall/Images/FuelCan.png" alt="Fuelcan" width="500" height="400">  

In the fuelcan blueprint, I made the players movement slower while carrying fuel, added a 3D widget that always faces the player and a collider on the fuelcan that turns the widget on when the player enters and vice versa:
![FuelCan code](/Frostfall/Images/FuelCode.png)  
This is how the pick & drop system looks ingame:  
![Pick&Drop Fuel](/Frostfall/Images/PickUp&Drop.gif) 

---  

## - Graphics  
This was my first game in Unreal Engine, so I decided to go for the ps1 looking graphics to keep the models and textures low resolution, since Unreal is known to get laggy due to demanding graphics. Also, ps1 graphics fit horror games.  

I lowered all the megascan texture sizes to as low as possible while still keeping the power of two rule.  

---  

## - Npc's    
### Wendigo  

I found an oldschool wendigo model that fit my game perfectly. So I got premission from Evan Sorrell, the guy who made the model to use it for my project. He makes horror games, this is his website: 
[Pixelwolf.net site](https://pixelwolf.net/)  

![Frostfall Jumpscare](/Frostfall/Images/WendigoStare.png)
 <img src="/Frostfall/Images/Wendigo.png" alt="Wendigo" width="450" height="410">  
 
### Walking pattern  

The wendigo slowly chases the player almost constantly with the "Ai move to" node set to the player. When the wendigo sees the player with the "OnSeePawn(pawnsensing)" event, the wendigo stands still and screams, then gains a high speed that goes down each second. If the wendigo does not see the player for 10 seconds, the wendigo stop chasing the player for a while, just walking around randomly before starting to slowly chase the player again.  

Link for the wendigo code: [Wendigo blueprint](https://blueprintue.com/blueprint/rngndrt9/)  
  
Gif of wendigo gradually slowing down when chasing the player:  
![Wendigo Running](/Frostfall/Images/RunningWendigo.gif)  

### Wendigo Jumpscare  
The wendigo model did not come with a jump scare animation, so I made this:  
![Jumpscare animation](/Frostfall/Images/ScareAnimation.gif)  

<table>
  <tr>
    <td><img src="/Frostfall/Images/Chased.gif" /></td>
    <td><img src="/Frostfall/Images/WendigoInGame.gif" /></td>
  </tr>
</table>

### Deer Npc 
![Deer](/Frostfall/Images/DeerNpc.png) 
![Npc Code](/Frostfall/Images/SmallDeerAiCode.png) 

---  

## - Car  

### Turn in
![Car](/Frostfall/Images/Car.png)  
![Car Code](/Frostfall/Images/CarCode.png)   
![Car Turnin](/Frostfall/Images/Turnin.gif)   
### Cinematic    
![Car Cinematic](/Frostfall/Images/Escape.gif)   

---  

## - Widgets and menus  

### Main menu  
![Main menu](/Frostfall/Images/NewMenu.png)   
### Pause menu  
![PauseMenu](/Frostfall/Images/3DPauseMenu.png)   
### Mini map and compass 
Adding the compass and minimap was the last thing i added because people that playtested the game thought that it was to dark and did not know where they were most of the time. The compass and minimap helps the player be able to figure out where they are and where they are headed.  

---  

## - Sound  
![Sound files](/Frostfall/Images/Sounds.png)  

---  

## - LevelDesign process     
 <img src="/Frostfall/Images/Drawing.jpg" alt="First drawing" width="500" height="500"> <img src="/Frostfall/Images/FirstMapLayout.png" alt="First map" width="500" height="500">
 <img src="/Frostfall/Images/SecondMapLayout.png" alt="Second map" width="500" height="500">
 <img src="/Frostfall/Images/FinishedMap.png" alt="Finished map" width="500" height="500">
