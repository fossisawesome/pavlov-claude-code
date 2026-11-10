# Making a Standoff 1 vs 1 Map

> Source: https://mod.io/g/pavlov/r/making-a-standoff-1-vs-1-map-guide
> Author: Mottflyer | Added: 2024-05-21 | Updated: 2024-05-21 | Views: 429 | Comments: 1 | Tags: 1 vs 1, 1v1, Gamemode, Standoff
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 7 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A quick guide on making a map for the Standoff 1 vs 1 Gamemode.

---
Make a map for the Standoff 1 vs 1 is very simple.

 

Start by creating a new map mod for your 1 vs 1 arenas or use a map you already have ready.

 

Download the Standoff Gamemode API source to your project.

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/sourcemod.png)

 

Go to the Standoff Gamemode API folder and create a child class of the *BP_Standoff_Arena_Base* and the *BP_Standoff_Lobby_Base*. Move the new child classes to the map mod you created.

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/createchildclasses.png)

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/examplemoddirectory.png)

 

Add your arena meshes to the arena BP and lobby meshes to the lobby BP. In the new BPs move the *player spawns*, *scoreboards*, *queue region* and *no fire zones* into position and set relevant arena and lobby details such as collision and lighting.

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/arenaexample.png)

 

Add the arena and lobby BPs to your map. Add the *BP_StandoffGamelogic* from the *Standoff Gamemode API* instead of the normal pavlov gamelogic blueprint and then setup the map as you would normally.
I Recommend adding 5 arenas so there is 1 for every player in 10-player lobbies.

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/mapexample.png)

 

Setup the map Definition with the *Custom Gamemode* box being checked.

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/definitionexample.png)

 

Go to your map's Mod.io page, open the *Admin Menu* and go to *Dependencies*. Add *Standoff Gamemode API* as a dependency otherwise the gamemode wont work.

![image](https://image.modcdn.io/members/26ce/20783807/profilestandoff/adddependancy.png)

 

Upload your map and enjoy!


---

## Comments (mod.io API, 1)

- **zeRocketVR** (2024-05-21): gg ez
