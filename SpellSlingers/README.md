# *Spellslingers*

![Spellslingers Menu](/SpellSlingers/Images/SpellSlingers_Menu.png)    
[Itch.io page](https://yrgo-game-creator.itch.io/spellslingers)   
[Repository Link](https://github.com/jheden/Spellslingers)  

## *A brief game description*  

**Spellslingers** is a pixel art, top-down, local multiplayer arena shooter, where you conjure and combine elements to cast powerful spells. With 126 different combination of spells, you play 2-4 players and unleash you inner wizard upon eachother.   

---  

## *My contributions to this project*  

Below is a summary of my code written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.   

---  

# - UI 

When we started the project, we divided the tasks among us, I wanted to learn Unity's new input system so doing the all UI became my task. 

The game was from the beginning suppose to be a dungeon rougelike co-op with friendly fire, so some scripts below has functionality for solo, co-op, and versus mode even if versus mode is the only mode in the game. We changed the game to only a versus game mode because we did not have time for the rest. 

---  

## - Main menu  
![MainMenu](/SpellSlingers/Images/Mainmenu_ToSelect.gif)   
<details>  
<summary>Main menu script</summary>   
   
![Main Menu script](/SpellSlingers/Code/MainMenu_Script.png) 
</details>  

---  

## - Character Select menu  
![SelectMenuEditor](/SpellSlingers/Images/VersusMenu_Editor.png)     

<details>  
<summary>MenuCharacterSelect Script, lets players join the selection menu making sure they don't have the same team or hat color as the other players</summary>   
   
![Menu Character select script](/SpellSlingers/Code/MenuCharacterselect_Script.png) 
</details>  

![Character prefab](/SpellSlingers/Images/CharacterSelect_Prefab.png)   
<details>  
<summary>Character Select Script, Includes all the functionality for the select menu</summary>   
   
![Character select script](/SpellSlingers/Code/Characterselect_Script.png) 
</details>  

The left gif shows changing hat, the right gif shows changing teams:  
<table>
  <tr>
    <td><img src="/SpellSlingers/Images/ChangeHat.gif" /></td>
    <td><img src="/SpellSlingers/Images/ChangeTeam.gif" /></td>
  </tr>
</table>

---  

## - Saving information across scenes  
![MapSelect](/SpellSlingers/Images/ReadyTo_MapSelect.gif)    
<details>  
<summary>Code from the bottom of the Character Select script, the players infromation is saved to the gamesettings script. The players team, hat color, gamemode and controller id is saved when all the players readies up</summary>   
   
![Player Ready code](/SpellSlingers/Code/Characterselect_Ready.png) 
</details>  

<details>  
<summary>GameSettings script, this script has dictionaries with all the information that needs to be saved cross scenes</summary>   
   
![Game settings](/SpellSlingers/Code/SaveInformaion_Script.png) 
</details>  

<details>  
<summary>PlayerSpawnSettings script, this script spawns in each players with all the infromation saved in the gamesettings script</summary>  
  
The biggest challenge was to keep information of each player to the same controller cross scenes, I managed to do this with Unity Engines's Input System, referencing to the inputdecive and 
this line of code in the script below: var player = PlayerInput.Instantiate(GameSettings.instance.players[inputDevice], controlScheme: "Gamepad", pairWithDevice: inputDevice.device);  

![Playerspawn script](/SpellSlingers/Code/PlayerSpawn_Script.png) 
</details>  

![Select to ingame](/SpellSlingers/Images/ReadyTo_Ingame.gif)  

---  

## - Pause & Spell Menu
I made a spell menu where the player can see all the 126 spells of the game, the menu plays a demo of the spell that's clicked on and show what buttons/elements to use to cast it.  

This is what it looks like to go from in game through the pause menu to the spell menu:
![Ingame to spellmenu](/SpellSlingers/Images/IngameTo_SpellMenu.gif) 

<details>  
<summary>Playercontroller code, Controlls for pausing the game and navigating the pausemenu)</summary>   
  
The player who paused the game becomes the pausemaster and is the only one that can navigate the pause menu:   
![Player Controller pause](/SpellSlingers/Code/Playercontroller_Pause.png) 
</details>  

<details>  
<summary>VersusUI script(controlls all visual UI in the arena)</summary>   

![VersusUI Script](/SpellSlingers/Code/VersusUI_Script.png) 
</details>  

This is what it looks like to browse through some spells in the spell menu:  
![Spellmenu](/SpellSlingers/Images/SpellMenu.gif)  

<details>  
<summary>ComboList script for the structure of all buttons in the spellmenu</summary>   
  
![Combolist Script](/SpellSlingers/Code/Combolist_Script.png) 
</details>  

<details>  
<summary>Combo button script is on each button, for the combo text and senario</summary>   
  
![ComboButton Script](/SpellSlingers/Code/ComboButton_Script.png) 
</details>  

---  

## - ScoreScreen & Bookpiles  
For the score screen, we decided to have book piles as pedestals meaning the more score a player has the higher the bookpile they will stand on.  

<details>  
<summary>Scorescreen script, this script decides the winner, shows score and calls on the bookpile script</summary>   
  
![Scorescreen script](/SpellSlingers/Code/Scorescreen_Script.png) 
</details>  

This are the different books and tounges that the piles are randomly built with:  
![Books](/SpellSlingers/Images/Books.png)   
![Tounges](/SpellSlingers/Images/Tounges.png)   

<details>  
<summary>Bookcontroller script, this script contains all the properties for the bookpiles</summary>   
  
![Bookcontroller script](/SpellSlingers/Code/BookController_Script.png) 
</details>  

<details>  
<summary>Bookpile script, this script takes books and tounges from the bookcontroller script and makes random piles with them </summary>   
   
---  

There are three different sizes of books, and they go in both directions, this made calculating a correct offset from the last book and the placement of the player hard because two books of the same size but with different directions had different offsets.  

I found no way of calculating this, so I manually set the offset of each book in each circumstance they may end up with, this is why this script is so long, but it works:  
![Bookpile script](/SpellSlingers/Code/Bookpile_Script.png) 
</details>   

If there are more players the piles heights differ accordingly, this is how the book piles look when there are two players:
<table>
  <tr>
    <td><img src="/SpellSlingers/Images/IngameTo_ScoreMenu.gif" /></td>
    <td><img src="/SpellSlingers/Images/IngameTo_ScoreMenu2.gif" /></td>
  </tr>
</table>

---  

## - Additional UI scripts  

<details>  
<summary>HoverButtonSound script, Adds sound the hover over buttons</summary>   
With ISelectHandler and IDeselectHandler, The Onselect and OnDeselect founctions gets called with (BaseEventData eventData) if the player hovers the buttons.  
   
![Hoverbutton script](/SpellSlingers/Code/HoverbuttonSound_Script.png) 
</details>  

<details>  
<summary>MenuMapSelect script, this script lets the players choose map after readying up in character select</summary>   
   
![Map select](/SpellSlingers/Code/MapSelect_Script.png) 
</details>  

---  

