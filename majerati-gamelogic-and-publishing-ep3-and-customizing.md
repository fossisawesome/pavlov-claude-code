# MaJerati tutorials: custom Game Logic and publishing (Ep.3 and "Customizing Custom GameLogics")

> Sources: Ep.3 https://www.youtube.com/watch?v=s31d9npfiOs (21:07, "Basic Custom GameLogic & Mod-io", **Shack modkit 3 / UE 5.1.1**, 2023); "Customizing Custom GameLogics" https://www.youtube.com/watch?v=VM0ZFpByeMA (26:45, UE5, ~2025). No descriptions beyond chapters/links, **no pinned comments**. Evidence: YouTube **auto-captions only** (no frames), read 2026-11-10. Transcripts: [../transcripts/s31d9npfiOs.md](../transcripts/s31d9npfiOs.md), [../transcripts/VM0ZFpByeMA.md](../transcripts/VM0ZFpByeMA.md). Spoken names may be misheard (**[ASR?]**). These are the **UE5 / Shack-era** counterparts to the older [video-game-logic-and-global-info-overview.md](video-game-logic-and-global-info-overview.md).
> The author states he is **moving away from Pavlov/UE5 tutorials** and published all his assets (custom skins, guns, knives, hands, item spawners, jumps, skin boxes, chicken spawners, UMaps such as "Killer Clown", and the tutorial game logic under a "new debug map" folder) free to the community: https://github.com/MaJerati1/xplat_Pavlov_MaJerati-Assets (**not downloaded or reviewed by us**; if used, review it as untrusted third-party content).

---

## Part 1: Ep.3, definition file and a minimal custom game mode on Shack (s31d9npfiOs)

### Definition file (0:00-3:24)
- Open `definition` in your UGC. **Do not touch Unique ID**; change the **Label/name** only; **leave Version alone** (bump on updates).
- **Map vs Quest Map:** this kit builds for both Shack and PC. **For Shack put your level in `Quest Map`**; putting it in `Map` "won't be able to upload unless you're making PC stuff"; PC maps go in `Map`. "Hidden" hides it from lists (author doesn't use it).
- **Compatibility** tags (default: Custom, Deathmatch, Team Deathmatch). **Custom** = you create the game logic from scratch. Untick Custom and keep Deathmatch/Team Deathmatch tags if you just want a plain DM/TDM map. Search & Destroy, CTF, Push, Prop Hunt need extra setup.
- **Custom Game Mode checkbox** forces the game mode to be "custom game mode" in server lists (then DM/TDM can't be used on it; author unsure). Give it a **Custom Game Mode Label** (e.g. `tutorial`); label only shows for game-mode UGCs in lists. Save (the author saves repeatedly).

### Create the game logic and its classes (3:24-6:44)
1. Right-click -> **Blueprint Class** -> parent **`GL_Base`** (the actor with the little actor icon; he has many) -> name it `GL_<yourmode>` (e.g. `GL_tutorial`) -> **drag it into the map**.
2. Select it in the Outliner: sections include game logic settings (**Respawn Time, Players Required To Start**...), and **Definition** (drag your definition onto it), **Global Info Class**, **Player Info Class**, **Player Proxy Class**. Defaults: use the example proxy or `Pavlov_PlayerProxy`; he creates his own for good practice.
3. Create **Player Proxy**: Blueprint Class -> search "player proxy" -> **Pavlov Player Proxy** -> name (`tutorial proxy`) -> assign in the GL's Player Proxy Class.
4. Create **Global Info**: Blueprint Class -> **Pavlov Global Info** -> name (`tutorial info`) -> assign in Global Info Class.

### Minimal game loop in the GL event graph (6:44-14:09)
- **Everything custom is in the event graph or in function overrides.** Clear the default nodes.
- Override **`On Custom Game Mode Init`** (called **once the map is loaded, only when the map is set to Custom Game Mode**; "super important", the game won't run otherwise). Chain: `Delay` (always use delays; don't run everything in the first frame) -> **`Set Game Mode Properties`** (drag the blue Properties pin -> **Make Pavlov Game Mode Properties**). Tick **Auto Respawn** (for a kill-around map), **Dynamic Spawns**, **No Teams** (free for all); leave others default (**Spawn Ghost On Login** = join as free-floating spectator; **Keep Bodies**; **Keep Pawn Alive**; respawn max delay) -> `Delay` (2 s) -> **`Set Round State` = `Starting`**.
- Override **`On Round State Changed`** -> **`Switch on EPavlovRoundState`** driven by **New State** (pins: Starting, Standby, Started, Ended):
  - **Starting:** optionally the built-in **Wait For Players Loop** (uses **Players Required To Start** on the GL actor) or just `Delay` -> `Set Round State` = **Standby**.
  - **Standby:** `Delay` -> **`Spawn And Possess Pawns`** (server command; **only available in custom game mode; effectively required**; spawns ghosts in as players at spawn points) -> `Set Round State` = **Started**.
  - **Started:** can be left empty. Result: a working free-for-all where you spawn with a pistol.
- **Pavlov_Spawn actors:** add a few. Team ID **-1 = any team**, 0 = blue only, 1 = red only. Tick **Dynamic** (great for respawn modes; avoids spawning in someone) (matches the GL's "Dynamic Spawns" property); **Only Team** restricts to the TeamID; **Special** is for Search & Destroy and "does require using 1 and 0" for the team number (see [../03-map-making-workflow.md](../03-map-making-workflow.md)).
- **Global Info** class defaults: **Limited Ammo Type** (Limited Generic = players spawn with limited ammo and must pick up more); also where **custom weapons/items must be added** (touched on, "a little complicated").

### Uploading to mod.io (17:00-21:00)
1. **Window -> Pavlov Workshop -> Upload Mod**; select the **UGC number** (UGC ids are created in order); add a **change note**.
2. **Platform:** with the Shack modkit (3) you can only choose **Android**; with the 5.1.1 PC kit you have **Android and Windows**: PC map = Windows only, Shack = Android only. Click **Upload Mod** (first upload is slow; wait for "upload complete").
3. On **mod.io** (logged in, otherwise no "My Teams"): **My Teams -> Mods** -> your mod -> **admin edit pencil**: set name, summary (defaults from the modkit **only the first time**; after that it can only be changed on mod.io), and change **visibility from Hidden to Public**; save. Status in My Teams becomes **Live**, and it appears in the in-game list.

---

## Part 2: "Customizing Custom GameLogics" (VM0ZFpByeMA)

### Two kinds of map logic
In the definition's **Compatibility** and **Custom Game Mode** you either make the map **custom** (you write the game logic) or follow a **standard mode** (TDM, SnD...). "Most mods I've seen are custom." With both Custom boxes ticked you must create your own game logic; **drag the definition, global info, player info and player proxy into the GL actor in the map or the map won't upload correctly.**

### Create: Blueprint Class -> **Pavlov Game Logic** parent -> `GL_<name>`
Event graph starts with Begin Play/Event Tick. **Overrides** list (Functions -> Override) shows `On Custom Game Mode Init`, `On Round State Changed`, `On Player Killed`, `On Player Left Server`, `On Player Joined Server`, etc. (or right-click the graph and type the name).
1. **`On Custom Game Mode Init`** -> `Delay` -> **`Set Game Mode Properties`** (Pavlov API; a **server-side** block). Enable "context sensitive" if nodes don't show. Make Pavlov Game Mode Properties fields: **no teams**, **scoring**/**no scoring**, **Auto Respawn** ("very important if you want players to respawn automatically; for a **last man standing** mode keep it **off** and let round states dictate"), **Keep Bodies** (off is better for performance), **Spawn Ghost On Login** (join as spectator, important so people don't start playing mid-round).
2. `Delay` -> **`Set Round State` = Starting**.
3. **`On Round State Changed`** has **Old State** and **New State**; use **`Switch on Pavlov Round State`** on New State (Starting, Standby, Started, Ended).

### Last-man-standing example he builds
- **Wait for players loop (Starting):** variable `NumPlayersToStart` (int, e.g. 2; set per map on the GL actor) vs **`Get Game State -> Get Player Array -> Length`** (>=). True -> `Set Round State` = **Standby**; false -> `Delay 10 s` -> `Set Round State` = **Starting** (loops).
- **Standby:** `Delay` -> **`Set Movement Disabled`** (checked: players can look but not move) -> **`Spawn And Possess Pawns`** (server command; spawns all ghosts at spawn points) -> `Delay 5 s` -> `Set Round State` = **Started**.
- **Started:** `Delay ~0.2-0.6 s` -> **`Set Movement Disabled`** (unchecked).
- **Ending the round:** handled in the **kill/leave events**: `On Player Killed` and `On Player Left Server` both give a **player status**; take its **Team ID**, branch per team (author duplicates the logic for team 0 and team 1): **For Each Loop over `Get Game State -> Player Array`**, `Get Pavlov Player Status`, count players **on that team and not dead** into a per-team **alive counter** variable (**reset the counter to 0 afterwards** or it keeps counting). If a team's alive count = 0 -> end the round.
- **`Reset Players` function:** For Each over the player array -> `Get Pavlov Player Status` -> **Branch (NOT Is Dead)** -> **Apply Damage** (huge, e.g. 9999, damage type knife) to kill everyone still alive -> `Delay 5 s` -> `Set Round State` = **Starting** (full loop).
- **Team assignment:** alternate teams as players join (each new player to the other team) so no balancing in the round-state logic; rejoin handling is up to you.
- Author's summary: **a custom game logic needs only two things: initialization (`On Custom Game Mode Init` + `Set Game Mode Properties`) and round-state handling (including `Spawn And Possess Pawns` and setting `Started`)**; waiting for players, resetting, etc. are extras. He recommends collapsing sections into functions. Finished BP is on his GitHub (see top).

### Related caveat worth keeping
Ep.4-style spawn logic: when spawning in the GL, **`Set Round State`**, delays and spawn commands are server-only; client-side UI needs a replicated event via the proxy (see [../04-gamelogic-proxies-modinitializer.md](../04-gamelogic-proxies-modinitializer.md)).
