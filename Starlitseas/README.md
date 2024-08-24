# Starlitseas  
![Starlitseas_Title](/Starlitseas/Images/Starlitseas_Portal.png)  
[Itch.io page](https://yrgo-game-creator.itch.io/starlit-seas )  
[Repository Link](https://github.com/Z1LENT/Starlitseas)
## *A brief game description*

**Starlitseas** is a parkour speedrunning game located between the seas and the heavens. The spirits of the sea help guide you towards heaven, granting you abilities to glide and dash your way up into the sky. Jump on whales and floating islands through eight beautiful levels to reach your final destination.

---
## *My contributions to this project*
Below is a summary of some of my visual scripts written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.

---
## *Character movement*
The character movement is half of the game, espacially in a parkour speedrun game. So I worked on the movement on and off the entire project, the movement script is pretty big so I won't go over it all.   
[Whole PlayerController node script](https://blueprintue.com/blueprint/zrsn74_s/ )

Making movement for jumping upwards on moving animated whales was hard, making it feel like the player is moving fast but still not making the game to fast and hard for the player to controll. 

### - Making the movement feel fast:
The script below is the update/tick event. To make the movement feel faster than it is, I added increased fov and speed lines running down the screen when moving. 
![](/Starlitseas/Images/Update_PlayerScript.png)
### Whale tail jump:
When the whales are moving upwards their animated tails sometimes used to block the player from jumping onto the whales back. To fix this problem I added a tail jump I called ledgejump. When the player is holding space near a tail the player gets boosted into the air, like the tail is hitting the player upwards making the player be able to scale the whales instead of getting blocked by the tail and falling off. 

I put a collider check on the whales tails calling the players ledgejump script.
![](/Starlitseas/Images/Tailboost_WhaleScript.png)
When the players ledgejump script gets called, check if the player is holding space and if so do a tail jump.
![](/Starlitseas/Images/Ledgejump_Script.png)
I also made it look like a tail slap animation by speeding up the whales basic animation for one second when jumping on its tail. It looks like this: 

![](/Starlitseas/Images/TailJump.gif)

## - Abilites
Our team decided on having abilities that gives the movement more flare, we had serveral ideas during the creation of Starlitseas but landed on a glider like in fortnite and a dash like the character Genji's ability from Overwatch. 

### - Glide ability:
Making the gliding ability was challenging, I started by downloading animations from Mixamo for the Unreal mannequin doll. The animations was for jumping/standing to hanging and hanging Idle. 
Then I blended them together depending on the players velocity when deploying the gilder. 

![](/Starlitseas/Images/Hanging_Animations.png)

I made a spirit pet that always circles the player until the glider is deployed then the pet becomes the glider. I made an animation for the glider to go up in size in a sec, I also added a material that stick to the spirit ray(the glider) that gives it a magical look.

Deploying and landing with the glider looks like this: 

![](/Starlitseas/Images/DeployGlider.gif)

The gilder works by setting the velocity upwards to zero, removing gravity and adding a small force downwards. It worked but caused many problems when other forces effected the players velocity, this caused the player to be launched out of the map because of the zero gravity. I fixed it by removing the glider and adding back gravity everytime a tail jump, boost ring or blowhole added force to the player. 

This may sound like a bad fix but it made for a more interactive gameplay deploying and reploying the glider, I also made the glider give the player a small speedboost forward when deploying. It also makes for more speedrunning possibilities when the player learns how to combine different movement boosts in combination. 

The Glider script(it's to big to show clearly):
![](/Starlitseas/Images/GliderScript.png)

### - Dash ability:
I made the dash launch the player at a set speed in the direction that the camera is facing. To make it more noticable that an ability was just used I rapidly increase the fov and made the speed lines on the screen turn green for about a sec. The dash also resets the gilder ability.
![](/Starlitseas/Images/DashScript.png)
The gif below shows both the abilities combined: 

![](/Starlitseas/Images/DashGif.gif)

## - Reset on ground touch
Script below shows when the player is touching the ground the abilites and jump resets. Also creates camerashake depending on how fast the player hits the ground. 
![](/Starlitseas/Images/ResetJumpAndSprint_Script.png)

## - Small features
### Fadeing in and out the whales: 
To many whales at the same time made the game lag so I added render distance to the whales.
I thought it looked weird when they spawned in out of nowhere so I created a script that fades the material of the whales in and out:
![](/Starlitseas/Images/FadeScript.png)
![](/Starlitseas/Images/WhaleFade.gif)


### - Blowhole water effect: 
When stepping on a blow whales hole, the player gets shot up giving a speed boost. I added sound and made a water material to the boost for more of a feel.

I set the material on the players screen for two seconds when stepping on the hole:
![](/Starlitseas/Images/BlowholeWaterEffect_Script.png)
It looks like this: 

![](/Starlitseas/Images/BlowHole_Gif.gif)

### - Spirit Guide: 
I added a talking ray that gives the player tips on what to do/encourages the player to keep going every level. The text is a 3D widget set over the ray, the ray is always facing the player with the text. The text only shows when the player is close to the ray. 

Scipt of how this is done:
![](/Starlitseas/Images/TalkingRayScript.png)
The rays text is set in the level blueprint. You can see the sprirt guide in the leveldesign images below. 
![](/Starlitseas/Images/RayText_LevelBlueprint.png)

---  

## *LevelDesign*
Starlitseas has 8 levels, every level going upwards towards heaven. I made the levels increasingly harder and longer. Adding different obsticles and changing the envoiroment to make every level special while keeping the same theme.   

The player follows the whales and floating islands throughout every level, the whales follows splines and thats how the levels are built.  

<details>
<summary> - Level 1 </summary>  
The first level starts at the beach and the bridge is higher than the player can walk, so the only way to get forward in the game is to learn to jump. there is also a spirit guide that shows the player the basic controls.  

![](/Starlitseas/Images/Level1_Ingame.png)
Level 1 is straight forward with only whale sharks, making it hard to fail. The player learns to jump on whales that slowly moves forward.  
![](/Starlitseas/Images/Level1.png)
</details>

<details>
<summary> - Level 2 </summary>  
  
The second level is slightly longer, moving upwards making it harder to jump on the whales, introducing blow whales that shoots the player in the air when walking on them.  
![](/Starlitseas/Images/Level2_Ingame.png)
Still an easy level but introducing new elements.  
![](/Starlitseas/Images/Level2.png)
</details>

<details>
<summary> - Level 3 </summary>  

The third level is an introduction level for the glide mechanic and boosting rings, the only way to get from one platform to another is to use the glider and the boosts. Making the player learn how to use the mechanic in different ways.   
![](/Starlitseas/Images/Level3_ingame.png)
There are no whales in this level to make the player focus on the new mechanic without being stressed by constantly having to move forward.  
![](/Starlitseas/Images/Level3.png)
</details>

<details>
<summary> - Level 4 </summary>  
The fourth level combines the new mechanics with the whale jumping and it has two different ways of getting to the goal, one way faster than the other but more risky for the players that want to speedrun.  

The level also has a new darker look, making it feel like your higher up than in previous levels.  
![](/Starlitseas/Images/Level4_Ingame.png)
The level also introduces the first obsticle that can kill you, the jellyfish rings are at the end of the level and makes for a more interesting gameplay, having to glide through them.  
![](/Starlitseas/Images/Level4.png)
</details>

<details>
<summary> - Level 5 </summary>  
The fifth level is pretty straight forward, The splines are tight together with alot of obsticles to make it slower and harder for the player to go around them.
![](/Starlitseas/Images/Level5_Ingame.png)  

![](/Starlitseas/Images/Level5.png)
</details>

<details>
<summary> - Level 6 </summary>  
The sixth level is an introduction level for the dash mechanic, the dash works like one of Genji's abilities in the game Overwatch meaning you go in the direction that you are looking. I noticed that many playtesters thought that the dash was only forward. To make every player understand how the dash works I made level six have floating islands above the player that only are accessible if the player dashes upwards.  

The look of the level is lighter with an aurora and fantasy feel, to create the feeling of heading towards space/heaven.   

I also added the giant whale in the background to add to the fantasy feel. The giant whale slowly goes around the map with the help of a rotating springarm set in the middle of the map.  
![](/Starlitseas/Images/Level6_Ingame.png)
The level is like the third level but harder. It takes a combination of all the mechanics to beat it, this level is where most players gets stuck a while and it's to makes the player ready for the last two levels.  
![](/Starlitseas/Images/Level6.png)
</details>

<details>
<summary> - Level 7 </summary>  
The seventh level is the longest one, it has two possible paths for the player to go right from the start, one faster than the other. There is a bunch of gliding in this level and it gives of a magical/fantasy feeling.  

Midlevel there is a giant leap of faith, fog should be hiding the islands ahead (not like in the image below), making the player glide into the fog then revealing a bunch of islands with whales soaring around them. Giving the player an epic feeling.  
![](/Starlitseas/Images/Level7_Ingame.png)
![](/Starlitseas/Images/Level7_Glide.gif)
![](/Starlitseas/Images/Level7.png)
</details>

<details>
<summary> - Level 8 </summary>  
The eight level is the last level before arriving in heaven. Whales flying in every direction and then going down again giving the feeling they have reached their destination, leading the player towards the sky. This is the most magical looking level.  

To get to the end the player has to jump and dash from island to island, every island higher than the last, reaching the top taking them to heaven and clearing the game.  
![](/Starlitseas/Images/Level8_Ingame.png)
![](/Starlitseas/Images/Level8.png)
</details>
