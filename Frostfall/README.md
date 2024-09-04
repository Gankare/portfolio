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

When the player gets jump scared/caught by the wendigo, I disable player input, makes the player mesh invisible, set the camera towards the wendigo, add camera shake, screaming sound and grain on the screen. This is all done inside of Event tick/Update, in the player blueprint. Relink: [Player blueprint](https://blueprintue.com/blueprint/ydhxzuci/)   

The jumpscare looks like this ingame:  
<table>
  <tr>
    <td><img src="/Frostfall/Images/Chased.gif" /></td>
    <td><img src="/Frostfall/Images/WendigoInGame.gif" /></td>
  </tr>
</table>  
  
### Deer Npc  
After making the game loop, I wanted to add a little bit of a randomness into the game. 

So I added a deer that runs around the map randomly at a very high speed, surprising the player with hoof noises and random screams.   
![Deer](/Frostfall/Images/DeerNpc.png)  

The deer npc's code:  
![Npc Code](/Frostfall/Images/SmallDeerAiCode.png)  

---  

## - Car  
I downloaded this car model and changed some of the materials on it, the windows were emissive before and the internal did not match the car. After making the materials look good, I added spotlights to the car's headlights, so the player easily could find where to go with the fuel.  
 <img src="/Frostfall/Images/Car.png" alt="Car" width="550" height="400">  
 
### Turn in fuelcan  
The car blueprints do not differ so much from the fuelcans blueprint. If the player is close, a text of how many fuelcans have been turned in shows, and the text is always turned towards the player.    

Car blurprint code:  
![Car Code](/Frostfall/Images/CarCode.png)   

This is what it looks like to turn in a fuelcan ingame:  
![Car Turnin](/Frostfall/Images/Turnin.gif)   

### Cinematic    
When filling the car up with five fuelcans you win the game, I made a cinematic with the sequencer in the scene, I move both the camera and the car in the sequence. So when you win, both the player and wendigo gets removed, the cinematic starts and car start + speeding away sounds play.

The cinematic looks like this ingame:  
![Car Cinematic](/Frostfall/Images/Escape.gif)   

Note this is how the window material looked before i changed it.  

---  

## - Widgets and menus  
When first making the widgets my goal was to have them all in world space as 3D texts, but for some reason it only worked in the editor and not when i built the game. With limited time I decided to make the menu and pause menu 2D like most UI, even if it does not fit in with the rest of the game.  

This is how the 3D pausemenu looked before, in the editor:  
 <img src="/Frostfall/Images/3DPauseMenu.png" alt="3D_PauseMenu" width="700" height="450">   
 This is the 2D pausemenu looks now:  
 <img src="/Frostfall/Images/New_PauseMenu.png" alt="New_PauseMenu" width="700" height="450">  

This is how the main menu looks now:  
 <img src="/Frostfall/Images/NewMenu.png" alt="Main menu" width="700" height="450">  

### Mini map and compass 
Adding the compass and minimap was the last thing I added because people that playtested the game thought that it was too dark and did not know where they were most of the time. The compass and minimap helps the player be able to figure out where they are and where they are headed. The compass code is in the player blueprint, the map is an image added in the level blueprint.

---  

## - Sound  
Sounds is alomost the most important element in making a horror game. I used sound attenuation to make some of the sounds 3D, meaning the sounds get higher the closer you are to them. I made the footsteeps and screams 3D, i also added 2D ambient background noises and owl howls for a errie feel.  

The sound files used:  
![Sound files](/Frostfall/Images/Sounds.png)  

---  

## - LevelDesign process     
 <img src="/Frostfall/Images/Drawing.jpg" alt="First drawing" width="500" height="500"> <img src="/Frostfall/Images/FirstMapLayout.png" alt="First map" width="500" height="500">
 <img src="/Frostfall/Images/SecondMapLayout.png" alt="Second map" width="500" height="500">
 <img src="/Frostfall/Images/FinishedMap.png" alt="Finished map" width="500" height="500">
