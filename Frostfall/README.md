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

The player controller blueprint is pretty basic, nothing changed with the movement. I Added a picup and drop for the fuelcans, flickering for the lighter that the player holds and also a pause game button.  Link for the code: [Player blueprint](https://blueprintue.com/blueprint/ydhxzuci/)   
### True first person character & camera   
I decided to go with a third person template instead of a first person template when starting my project because I wanted a true first person (where the player is able to see their own body).  

I used a megascan 3D character model for the player and socketed the camera to the head, adjusted the fov and camera wobble when the player walks.   
![Player](/Frostfall/Images/Player.png)  

### Lighter  

I downloaded a lighter model and living candles from the unreal store. Then I socketed the lighter to the player's hand and socketed the living flame from the candles to the lighter. I set two point lights to the lighter, one closer and stronger and one farther away that's more subtle. 

It looks like this:  
![Flame](/Frostfall/Images/Flame.gif)  
### Fuel  
I took this oilcan from megascans and made the texture emissive to glow in the dark, making it clear that the can is an interanctable object.    
 <img src="/Frostfall/Images/FuelCan.png" alt="Fuelcan" width="500" height="400">  
 
![FuelCan code](/Frostfall/Images/FuelCode.png) 
![Pick&Drop Fuel](/Frostfall/Images/PickUp&Drop.gif) 

---  

## - Npc's    
### Wendigo  
[Wendigo blueprint](https://blueprintue.com/blueprint/rngndrt9/)  

![Wendigo](/Frostfall/Images/Wendigo.png)  
### Walking patern  
![Wendigo Running](/Frostfall/Images/RunningWendigo.gif)  
![Wendigo catching](/Frostfall/Images/Chased.gif)  

### Wendigo Jumpscare  
![Jumpscare animation](/Frostfall/Images/ScareAnimation.gif)   
![Jumpscare ingame](/Frostfall/Images/WendigoInGame.gif)   

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
Adding the compass and minimap was the last thing i added because people that playtested the game thought that it was to dark and did not know where they where most of the time. The compass and minimap helps the player be able to figure out where they are and where they are headed.  

---  

## - Sound  
![Sound files](/Frostfall/Images/Sounds.png)  

---  

## - LevelDesign process     
 <img src="/Frostfall/Images/Drawing.jpg" alt="First drawing" width="500" height="500"> <img src="/Frostfall/Images/FirstMapLayout.png" alt="First map" width="500" height="500">
 <img src="/Frostfall/Images/SecondMapLayout.png" alt="Second map" width="500" height="500">
 <img src="/Frostfall/Images/FinishedMap.png" alt="Finished map" width="500" height="500">
