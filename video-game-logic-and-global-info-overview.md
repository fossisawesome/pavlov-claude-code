# Videos: "Pavlov VR Mod Kit: Game Logic overview" and "Global Info overview" (Lance S / Vankrupt, UE4-era kit)

> Sources: Game Logic https://www.youtube.com/watch?v=g6qwk1vJ488 (15:20); Global Info https://www.youtube.com/watch?v=XvDfRuYXI10 (4:20). Both have only the repo link as description and no pinned comment. Part of the series: Game Logic -> Global Info -> Custom Items ([video-custom-items-overview-KlxXufos_-M.md](video-custom-items-overview-KlxXufos_-M.md)) -> Player Proxy/skins (next video, not on the wiki list we processed). Evidence: YouTube **auto-captions only** (no frames), read 2026-11-10. Transcripts: [../transcripts/g6qwk1vJ488.md](../transcripts/g6qwk1vJ488.md), [../transcripts/XvDfRuYXI10.md](../transcripts/XvDfRuYXI10.md). Names are as heard; **[ASR?]** = likely mis-transcribed.
> **Version caveat:** UE4.21-era kit, but the classes (`Pavlov_GameLogic`, `Pavlov_GlobalInfo`, example `GL_*` blueprints) are still in the Shack kit. Event/function names below should be checked against `Examples/Proxies/CMP_GlobalInfoExample`, `Blueprints/Pavlov_GameLogic_Example` and `Examples/GL_Base` in the Pavlov-Shack kit.

---

# Part 1: Game Logic overview (g6qwk1vJ488)

## Where the classes are
View Options -> **Show Plugin Content** in the Content Browser; folders **Blueprints** and **Examples** under CustomMapTools. `Examples` has the vanilla-style game modes (the same `GL_*` examples listed in [../04-gamelogic-proxies-modinitializer.md](../04-gamelogic-proxies-modinitializer.md)). The narrator builds a tiny tutorial mode.

## The generic game loop (flowchart, 0:40-2:46)
1. **Game start** -> **Starting** state: wait 1 second; check for the required player count (set it to 1 for testing, or 2 for a duel; or skip the check). Not enough -> wait another second and recheck.
2. -> **Standby**: **spawn and configure all players** (loadouts/weapons for the round, enable buying, freeze time, set health, set movement disabled, etc.); wait for players to buy.
3. -> **Started**: wait for the **end-of-round condition** (timer, a team dead, first death...). It is **event-based**, not polled.
4. -> **Ended**: decide **go back to the lobby, or on a custom server rotate to the next map**; or loop back to Starting for another match.

## Implementing it
- **Override `On Round State Changed`** (My Blueprint -> Functions -> Override). It gives the **new state**: **`Starting`**, **`Standby`**, **`Started`**, **`Ended`**.
  - **Starting:** `Delay 1s`, check `Get Game State -> Player Array` length > 0 (note: **bots are not filtered out**). If true -> **`Set Round State` = Standby**; else loop.
  - **Standby:** initialize/spawn players ("spawn and possess pawns"), optionally `Set Buying Enabled` (per player), freeze time, health, `Set Movement Disabled`; then set Started.
  - **Started:** start a **respawn loop**: set a **timer** (store its **timer handle**), loop all players, if dead > ~5 s then **`Get Spawn Transform`** and **spawn** them. Also set the match properties (next section).
  - **Ended:** clear the respawn timer handle, short delay ("give everyone a second to relax"), then either set **Starting** again or, to end: **`Get Game Mode` -> cast to game mode -> End** (kicks back to the lobby, or **rotates on a custom server**). On a community server it's good practice to rotate if the match isn't popular (check player count).
- **`Set Game Properties`** node (search for it; make a `Game Properties` struct from the pin). Struct fields heard (names may be slightly off **[ASR?]**):
  - **No Teams** / **Teams Always Scoring**: leave ticked if you don't want end/start scoring; untick to score.
  - **Force No Scoring**: tick if you compute all scoring manually. Related scoring fields: **max cash**, **cash kill reward**, **cash kill penalty**, **increment team score** (team-based modes, per kill).
  - **Auto Respawn**: the narrator recommends **building your own respawn loop** instead (as above).
  - **Keep Bodies**: keep bodies in the level (don't destroy). **Keep On If Alive**: respawns the pawn or moves them back to their start point if you call spawn-and-possess at the end of a round.
  - **Inactivity Threshold**: cleans out items inactive past this limit.
  - **Dynamic Spawns**: **recommended on**: checks the spawn point for nearby players before spawning.
  - **Spawn Ghosts On Login**: **recommended on by default**.
  - **Round time** (the example uses **900 seconds**): when it elapses the state goes Started -> Ended.

## Events to override
- **`On Player Spawned`**: gives the **player status** (lots of data about the player). Use it to **give cash, set buying enabled, give items, spawn attachments, set vitality**. Example: spawn with a **Desert Eagle (`de`)**, **knife**, **ACOG**, "full armor and a helmet". **Tip: collapse all spawn logic into a function** (select, right-click -> Collapse to Function) so it **runs within a single frame** and isn't skipped when many players spawn at once (round transitions), and **avoid delays inside it**.
- **`On Player Killed`** (the narrator says "zombie killed" once by mistake): inputs = **killed player's status**, the **killer's player state** (get their status from it), **was headshot**, **killed-by item ID**. Use for last-man-standing/kill-count end conditions.
- Others (not used in the example): **`On Round Beginning`** (heard "on random"?) **[ASR?]**, **`On Player Left Server`**, **`On Player Joined Server`** (also usable for save/load per player), **`On Custom Mark On Commands`** (likely `On Custom Commands`/mod RCON commands) **[ASR?]**, covered "in a later video" (advanced).

## Class defaults on the Game Logic
- **Definition**: **must be set** to use the game logic. Create it via **Window -> Pavlov Workshop -> Create New** (generates the UGC folder + definition file; **all content must be inside the UGC folder**; the definition holds mod/map settings, e.g. Compatibility/Custom per [../03-map-making-workflow.md](../03-map-making-workflow.md)).
- **Global Info Class**, **Player Info Class**, **Player Proxy Class**: if you create a custom game mode you can set these; they are "basically wrappers for the player pawn, the player state and the game state". Set them if you want them spawned by default.

## Globally exposed functions (14:09-15:10, Blueprint-callable from anywhere)
- **Get Player Status** (from a player state or a pawn): all info about the player.
- **Get Game Mode Properties**; **Get Spawn Transform** (for that player's team); **Spawn** (spawns the controller as a **ghost** or a **player**).
- **Increment Player Score**, **Increment Team Score**, **Set Player Cash**, **Set Team Cash**, **Give Cash**.
- **Set Round State**, **Switch Off Round State** (as heard) **[ASR?]**, **Set Buying Enabled**, **Set Movement Disabled**, **Set Player Vitality**.
- **Spawn Item** (by ID), **Spawn Attachments**.
- **Set Player Team** (from the player state): best done **after death or between rounds** (not at spawn); if rebalancing teams do it **right before spawning in the loop**.
- **Helper library:** **Get Moderators** / **Get Whitelist** (community servers), **Is Community Server** vs lobby, **Get Game Logic** (this class), **Get Global Info**, **Get UTC Time** and **Get Day Of Week (UTC)** (new; lets logic vary by weekday), **Load String Array / Load String From File** and **Save String To File** (**custom/community servers only**), **Add Message Handler**, **Add Player Info**, **Add Player Proxy**.
- Support: the narrator's Discord handle is "smart day" **[ASR?]**; the Pavlov Discord workshop channels.

---

# Part 2: Global Info overview (XvDfRuYXI10)

- **What it is:** attached to the **GameState**, so its lifespan is the **whole match**; it is **net relevant and replicated to all clients** (accessible client and server). Put **replicated variables related to game state** here.
- **Example:** `Examples/Proxies/CMP_GlobalInfoExample` (in the video "global info example"). Mostly empty; the useful bits are **Class Defaults**:
  - **Player Skin Table** (covered with the player proxy; see [../04-gamelogic-proxies-modinitializer.md](../04-gamelogic-proxies-modinitializer.md) player skin section).
  - **Custom Item Table** (covered next video; this is where you "specify to use" custom items; see [video-custom-items-overview-KlxXufos_-M.md](video-custom-items-overview-KlxXufos_-M.md) section 6).
  - **Limited Ammo Type**: **Unlimited**, **Limited Generic** (any ammo works with any weapon), **Limited Specific** (each weapon needs its own ammo type). Also **Disable Attach Mode** (people can't remove/replace attachments).
- **Runtime functions** on the Global Info: **Get Limited Ammo Type**, set it via console command (**server-side only**, not client-side), **Disable Voting** (confirms the mod.io votekick guides), **Disable Attach Mode**, **Get Skin Table**, **Get Custom Item Table** (lookups).
- **Create one:** Content Browser -> right-click -> **Blueprint Class** -> search **`Global Info`** -> select **Pavlov Global Info** as the base class -> name it. **Specify it** in your **Game Logic -> Class Defaults -> Global Info Class**.
- **Access it anywhere:** **`Get Global Info`** (works from any class, client or server). **It may be invalid in the very first second the server starts**, valid afterwards for the whole match. **Cast** it to your own type (the example casts to "global info example 1"), then read/set your variables.
- **Replication rules:** make a variable **Replicated** to read it on both client and server; **None** if no replication needed; **any replicated variable should be set on the server**.
- Next video (not covered here): the **custom item table**, then the **player proxy / player skin table**.

---

# Consolidated answer: how custom items are registered (old kit) / what to check in UE5
Game Logic -> **Global Info Class** = your Global Info -> **Custom Item Table** property = a **Data Table** whose row struct is **Custom Item Data** (one row per item: row name = item ID, plus the item class) -> items are spawned by ID with **Spawn Item**. In the UE5 kit, `Examples/Items/CustomItemTableExample` is still shipped; the newer gun/mod flow registers items from a **Mod Initializer** (`Add To List`; see [video-creating-custom-guns-nxw2cP2fICQ.md](video-creating-custom-guns-nxw2cP2fICQ.md)). Use the table route for map/gamemode-local items and the initializer route for content mods [?; confirm in editor].
