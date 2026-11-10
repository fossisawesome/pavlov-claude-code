# Modkit 3.0 FAQ and Best Practices

> Source: https://mod.io/g/pavlov/r/modkit-30-faq-and-best-practices
> Author: Juntistik99 | Added: 2023-11-07 | Updated: 2024-04-09 | Views: 4909 | Comments: 3 | Tags: DNU_PINNED
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 4 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: How to get a better understanding as a community server owner, or content creator on how to best take advantage of the new modding system.

---
### Definitions of each new type of User Generated Content

 

**Content Mods**

Standalone content that can contain any gameplay assets, level geometry etc. Maps and gamemodes can rely on mods using their content. Mods cannot rely on maps, mods, or gamemodes. Mods should not alter the gamemodes gameplay loop, please use a GameMode if this is your goal.

 

**Maps**

Either act as Legacy being an all in one gamemode, map etc or just used as a map and gamelogic is ignored if using a custom GameMode. Can rely on Mods for content. **Note: If you enable Custom in your gamelogic then it will lock your map to only using the GameLogic provided with the map.**

 

**Gamemodes**

Overrides the GameLogic for the level, can rely on Mods for content.

 

### Understanding Dependencies

Dependencies are defined in this case as content that relies on another for it to work properly. For example if you have a "game mode" that relies on the content of a "Mod", then that game mode links to the mod as a dependency and both are downloaded by the player automatically prior to joining the match. Think of this as one way relationship. 

The benefit of this, is you no longer need to share project files in many circumstances between creators to add content to your mod. This also helps with versioning mods as well so when the original mod author updates their content, then any subsequent content using it as a dependency also receives the update! 

If you have a map or game mode that needs to call a Mod. You will need to link the dependency in Mod.io. Both projects need to be set to Live in Mod.io.

### Setting up Mod.io Dependencies

If you have a map or game mode that needs to call a Mod. You will need to link the dependency in Mod.io.

In this particular example we have a mod that contains all the assets for a level. The map itself is simply just the level connecting to the definition file in its own separate UGC. Creating content in this fashion dramatically reduces upload times as the only level needs to be uploaded whenever changes are made if no new content is added to the mod containing the assets. 

![image](images/modkit-30-faq-and-best-practices/b0a3f03050.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/dependenciesscreenshot.png -->

In order to set a dependency.

- Go to your Mod.io page for your Map/GameMode.

- Click on the pencil icon for admin

- Locate dependencies on the left side panel

- Search for the mod by name. This only works if the Mod is set to live.

- Save

If successfully performed, you should see your UGC list the mod as a dependency in the main UGC page. (see above image)

![image](images/modkit-30-faq-and-best-practices/4b27a5fcab.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/dependencies2.png -->

Use the mod title that is used in Mod.io to locate and save as a dependency. 

![image](images/modkit-30-faq-and-best-practices/9ca79d69e0.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/depend3.png -->

Both projects need to be set to Live in Mod.io. **The dependency needs to be uploaded for your particular content platform in order for it to work**. For example, if you setup a Shack map and use a mod dependency that is only published for PC, then it will fail to load. Each platform is for the client (your VR headset) and the server (lobbies and community servers).

PC + Linux is for the PC platform. 

Oculus + Mac is for the Shack platform on standalone. 

 

***How to use the MODS feature to share assets between UGCs***

1. Open project and make mod UGC

2. drop your asset pack into the UGC folder

3. Make map UGC

4. In your map level drag/drop and place assets from the mod UGC folder into your map

5. Upload mod UGC

6. Upload map UGC

7. make sure mod UGC is public

8. set the mod UGC as a dependency for your map UGC on the Mod.io webpage for your map

9. set your map as public

 

***How to Create a GameMode***

- Create the UGC (Make sure to select Gamemode in the process)

- Create a Pavlov_Gamelogic  (we will not be covering how to create a gamemode loop just the basics of uploading) Leave the definition blank inside the game logic, you can assign your own player proxy and global info.

- Open your definition inside your ugc, assign the Pavlov_GameLogic you created.

- Upload to Mod.io

Note: You cannot load a custom gamemode if the map is a custom gamemode map (it has custom gamemode enabled in the map definition)

***How to Create a Mod***

- Create the UGC (make sure to select Mod)

- Create a Pavlov_ModInitializer actor inside your UGC. This gets created on the client and server but is not replicated. Use this class to spawn additional content, get access to the globalinfo, gamelogic etc. There's a function OnModInitialized that you can override, this can be used to add custom guns, items etc similar to the setup previously done in the global info.
Note: If you're just creating a content mod (ie. static meshes etc for a level) you can skip to step 4.

- Open your mod definition, set the ModInitializer to the one we just created.

- Add any additional content you'd like inside your UGC, if you're using this as a content pack then you can map/gamemode dependencies on this mod and use this content with other UGC plugins.

- Upload to Mod.io

 

### Community Servers and Mods

***Game.ini***
You can now specify custom gamemodes by UGC ie.
MapRotation=(MapId="UGC3249319",GameMode="UGC3262731")

 

***Playing a Mod on a Vanilla Map with a community server***
We’ve added AdditionalMods, these can be enabled on the server and are loaded in every map. Such as using the lines:
AdditionalMods=UGC3265420
AdditionalMods=UGC3267926

 

***Calling a mod with RCON***

Currently you can only load Maps/Mods via rcon by using the SwitchMap command, at a later point we plan to add the ability to add/remove additional mods. For the time being you can change the game.ini to add additional mods and restart the server.

 

***How to spawn an Item from a Mod***

Mod makers should provide a list of itemIds on the mod page, these can be used in the various modkit functions, RCON, weapon spawners, vehicle spawners, etc. Modders can also now add items and weapons to the player buy menu. 

##### RCON commands

- `UGCaddmod UGC[#]` with [#] being the resource ID or UGC number

- `UGCremovemod UGC[#]` to remove the mod

- `UGCClearModList` to clear all currently loaded mods

**Server must rotate current map in order for the mod that has been removed or added to take effect** 

It will be up to the mod creator, but you can also run RCON commands to interact with custom items, or they will make the custom items available in their buy menu.

Most modders list the item IDs in their description as good practice.

Commands for custom game modes would behave similar to commands for vanilla game modes For example `switchmap sand snd` and instead of using snd in this example you would use UGC[#] So if you wanted to run switchmap to a custom game mode on a custom map you can use `Switchmap UGC[#] UGC[#]` Here's a live example `switchmap UGC3247570 UGC3267976` This would run Random Gun on Kill custom game mode by MessiahPengiun with Ardennes by Charble.

Important note: Gamemodes can't be added as a server wide mod such as using UGCaddmod or listing in the game.ini under additional mods, the command will fail.

 

**Make sure the mod you're loading supports the correct platform!**

 This can be confirmed by looking at the version platforms. Mac is for Shack server and Oculus is for the Shack client

![image](images/modkit-30-faq-and-best-practices/43a9353475.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/versioning.png -->


---

## Comments (mod.io API, 3)

- **ErgoDEV** (2024-07-17): dope
- **mr_cabnet123** (2023-11-25): dis gonna take long
- **Cheeto_V** (2023-11-25): Yippee!
