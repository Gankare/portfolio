# *Spellslingers*

![Spellslingers Menu](/SpellSlingers/Images/SpellSlingers_Menu.png)    
[Itch.io page](https://yrgo-game-creator.itch.io/spellslingers)   
[Repository Link](https://github.com/jheden/Spellslingers)  

## *A brief game description*  

**Spellslingers** is a pixel art, top-down, local multiplayer arena shooter, where you conjure and combine elements to cast powerful spells. With 126 different combination of spells, you play 2-4 players and unleach you inner wizard upon eachother.   

---  

## *My contributions to this project*  

Below is a summary of my code written to this game, keep in mind that this is a group effort and we co-developed a lot of features, but all the highlighted features below have been implemented by me.   

---  

# - UI 

When we started the project, we divided the tasks among us, doing all the UI was my task. 

## - Main Menu  
![MainMenu](/SpellSlingers/Images/Mainmenu_ToSelect.gif)    


## - Character Select menu  
![SelectMenuEditor](/SpellSlingers/Images/VersusMenu_Editor.png)    
![Character prefab](/SpellSlingers/Images/CharacterSelect_Prefab.png)   
The left gif shows changing hat, the right gif shows changing teams:  

<table>
  <tr>
    <td><img src="/SpellSlingers/Images/ChangeHat.gif" /></td>
    <td><img src="/SpellSlingers/Images/ChangeTeam.gif" /></td>
  </tr>
</table>

## - Saving information across scenes  
![MapSelect](/SpellSlingers/Images/ReadyTo_MapSelect.gif)    
![Select to ingame](/SpellSlingers/Images/ReadyTo_Ingame.gif)  

## - Pause & Spell Menu
I made a spell menu where the player can see all the 126 spells of the game, the menu plays a demo of the spell thats clicked on and show what buttons/elements to use to cast it.

This is what it looks like to go from ingame threw the pause menu to the spell menu:  
![Ingame to spellmenu](/SpellSlingers/Images/IngameTo_SpellMenu.gif)  

This is what it looks like to browse threw some spells in the spell menu:  
![Spellmenu](/SpellSlingers/Images/SpellMenu.gif)  

<details>  
<summary>VersusUI script(controlls all UI in the arena)</summary>   

![VersusUI Script](/SpellSlingers/Code/VersusUI_Script.png) 
</details>  

<details>  
<summary>Combolist script for the structure of the spellmenu</summary>   
  
![Combolist Script](/SpellSlingers/Code/Combolist_Script.png) 
</details>  

<details>  
<summary>Combo button script</summary>   
  
![ComboButton Script](/SpellSlingers/Code/ComboButton_Script.png) 
</details>  

## - ScoreScreen & Bookpiles   
![Books](/SpellSlingers/Images/Books.png)   
![Tounges](/SpellSlingers/Images/Tounges.png)   

<table>
  <tr>
    <td><img src="/SpellSlingers/Images/IngameTo_ScoreMenu.gif" /></td>
    <td><img src="/SpellSlingers/Images/IngameTo_ScoreMenu2.gif" /></td>
  </tr>
</table>

---  
