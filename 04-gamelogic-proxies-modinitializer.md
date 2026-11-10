# 04 - The "Coding" Layer: GameLogic, Proxies, Info Classes, ModInitializer

All Pavlov scripting is **Unreal Engine Blueprint** (visual scripting) on classes provided by the Modkit's closed `Pavlov` module. There are no text-code APIs. Exact event/function names are only partly documented; **open the example Blueprints listed below in the editor and read them**; they are the real API reference. [V that no text scripting exists; names below are from docs/kit file lists/video chapters]

Note: the mod.io Shack custom-gun guide mentions Python field names (`generic_scalar1`, `generic_flag1`), which hints the editor has Python/UE reflection names for those variables; this is the UE property name mapping, not a modding scripting language. [?]

## Where to learn by example (inside the Modkit: Plugins/CustomMapTools/Content, enable "Show Plugin Content")
| Asset | Teaches |
|---|---|
| `Blueprints/Pavlov_GameLogic_Example`, `Examples/GL_Base` | Minimal game logic skeleton |
| `Examples/DeathMatch/GL_Deathmatch`, `GL_TeamDeathmatch` | FFA/team scoring loops |
| `Examples/GunGame/GL_GunGame` | Progressive loadouts |
| `Examples/KOTH/GL_KOTH`, `BP_HillObjective` | Objectives, scoring zones |
| `Examples/SingleRespawnMode/GL_SingleRespawn` | Round-based elimination |
| `Examples/Zombies/GL_Zombies` | AI/wave style mode |
| `Examples/Advanced/GL_Advanced` | Advanced features |
| `Examples/Items/FOB/GL_FobExample`, `ModItem_FOB`, `EQS_FOB`, `S_FobInfo` | Custom item + forward base |
| `Examples/Items/Flashlight/ModItem_Flashlight` | Custom item (ModItem_*) |
| `Examples/Items/CustomItemTableExample` | Registering custom items in a data table |
| `Examples/Items/HandPoses/*` (`GM_PoseTester`, `SM_PistolGrip`, `SM_RifleGrip`...) | Hand pose sequences for custom items |
| `Examples/PlayerSkinTable` | Player skin data table (row name -> skeletal mesh) |
| `Examples/Proxies/BP_PlayerProxyExample`, `BP_HandProxyExample`, `CMP_GlobalInfoExample`, `CMP_PlayerInfoExample` | Proxy / info pattern |
| `Examples/TTTv2/*`, `Mod_Initializer_TTTRoles_Example` | Mod initializer registering roles, UI badge/banner |
| `PavExamples/Guns/AK47/*` | Full custom gun (gun, mag, bullet, shell BPs, AnimBP, physics asset, skeleton) |
| `PavExamples/Attachments/*` | Custom sight/scope/suppressor/grip/bayonet/canted bases |
| `PavExamples/Grenades/*` | Custom grenades (MK2, M24 with AnimBP) |
| `PavExamples/AvatarSkins/*` | Avatar skin + flying helmet |
| `PavExamples/Destructible/*` | Destructible glass |
| `PavExamples/BP_TestItemSpawner`, `EditorTools/BP_ItemVisualizer` | Spawning/preview tooling |
| `Blueprints/BP_LootSpawnerProxy` | Loot spawning |
| `Examples/BP_VehicleSpawnerProxyExample` | Vehicle spawner |

## GameLogic (per MaJerati "Customizing Custom GameLogics", VM0ZFpByeMA chapter list) [D]
Order of work: **Gamelogic paths -> definition config -> create GL BP (subclass of Pavlov_GameLogic) -> initialize GL -> Round State events -> WaitForPlayer loop -> spawn players & movement -> Started Round -> Players leaving/joining/killed -> auto-set teams -> check remaining players per team -> 0-players-on-team check -> round reset (end state)**. His asset repo: https://github.com/MaJerati1/xplat_Pavlov_MaJerati-Assets

Key mechanics:
- Round state events (waiting, started, ended) drive the loop; custom modes build a Last-Man-Standing style check on player death.
- Players join/leave/killed events (OnPlayerSpawned, OnPlayerDeath, etc.) exist on game logic and proxy. [V names OnPlayerSpawned/OnPlayerDeath from the scoreboard guide]
- Setting Custom on the map definition = custom gamemode forced.
- In a **Gamemode UGC**: leave the Definition field blank inside the `Pavlov_GameLogic` BP and assign your own proxy/global info; assign the GL in the UGC definition. [V]

## Player skins [V wiki + D videos]
1. Create BP subclass of `Pavlov_PlayerProxy`; in the event graph call **Set Player Skin** (server/authority only; default skin name is None). Run from BeginPlay via **Switch Has Authority -> Delay 1s -> Set Player Skin**.
2. Copy `PlayerSkinTable` into your UGC; add rows (row name -> skeletal mesh). Meshes must target the **UE4 mannequin skeleton** `SK_Mannequin` (CustomMapTools/Mannequin/Mesh).
3. In your `GameLogic` copy, set Player Proxy Class to your proxy; set Global Info class (CMP_GlobalInfoExample copy) with Player Skin Table = your table.
Videos: Ep. 4, Ep. 9, "How to make Custom Skins" (Auto-Rig Pro workflow).

## Money system pattern [D/V]
Custom functions on PlayerInfo: Add, Subtract/Spend, Check money. Server custom event (Run on Server) with inputs PlayerState + int calls `Set Player Cash` on the Game Logic. Widgets cast to your PlayerInfo and call the custom events (mod.io "Money System: Achievement System"; video aubVoeG8geQ with buyable items, delivery job, balance checker).

## UI: widget interactor menus (replace scoreboard) [V wiki, by HTHazard]
- `widgetInteractor` actor with Widget Interaction component (pointer index 10, interaction distance ~750); input actions ScoreBoardLeft / TriggerRight; Pointer Keys = left mouse button.
- `Menu_Widget` UMG with buttons (onClicked/onHovered).
- `VrWorldMenu` actor with Widget component hosting it.
- Player proxy: `callDoGiveInteractor` (not replicated) -> `doGiveInteractor` (Run on owning client) spawns menu + interactor and attaches to hands client-side; destroy on OnPlayerDeath. Game logic calls it from OnPlayerSpawned.
- mod.io guides: scroll menus on widget interactor, locking widget buttons by role/owner/staff (Kaimes), whitelisted functions (xe_nova), disabling voting.

## ModInitializer (content mods) [V]
`Pavlov_ModInitializer` actor in your Mod UGC; set it in the mod definition. Override **`OnModInitialized`** to add custom guns/items (same role the GlobalInfo hook played in the older kit). Use it to spawn extra content and reach GlobalInfo/GameLogic. Video 0eJ1j0JRF2Y: sharing assets between maps, setting up initializer, **editing stats of existing guns**. [D]

## Custom items & item IDs
Mod makers publish item IDs in the mod page description (or video 7Dcuh3vqsJo referenced on mod.io). IDs work in RCON `GiveItem`, weapon/vehicle spawners, buy menu. RCON `ItemList` lists base + current-map custom items (truncated at a max). Mods can add items to the player buy menu.

## Teleports, keycards, spawners, audio (video-derived recipes) [D]
- Teleporters (Ep.7: basic, grab, VIP): trigger box BP + set actor location; public teleporter guide on mod.io.
- Keycard reader: dynamic version without OnComponentEndOverlap (replicated custom event, instance in map) 9PrRyTpZhPk.
- LSWCM/VSWCM (KENNITHH): visual loot/vehicle spawner with colored model preview. Copy its Content into modkit Content, **move Blueprints folder into UGC**, fix up redirectors, drag BP into map. (Old repo version verified only for 4.21; the new-video 1TYkJzv6-XI addresses UE5.)
- Chicken/AI spawner, multi-use BPs with Switch statements (Zp8d4JYgDLs, t--gr9uJR1o).
- Audio: UE5.1 supported formats, import into UGC, background ambience, spatialized audio and attenuation (SehhU3-X5fM). Corrupt OGG/WAV can break Android packaging.
- VRSelection component (mod.io guide): add to BP, set Proxy Mesh Material to selection overlay, implement Activate/Deactivate with haptics, hook interact box events -> gives in-game "glow when hovered".

## Community frameworks (mostly UE4.21-era; may not work on UE5/Shack) [V list from wiki]
Visual loot spawner (KENNITHH), Advanced Movement (Yoshi), Advanced Bomb Spot, Launch Pads (Xandon), Push Advanced Pack (Golden), Custom Shops (Zetch505), Skin Box, Bow & Arrow, Kill Confirmed, Zombies, Parkour, Custom CTF (Shack support), Gravel Wars, VIP escort, Infection (Coomzy `Pavlov-PMF`, Skeedard), Prison Break; Shack: Showdown, PavZ/PavZ2 (PavlovScore Discord). Always check each repo for UE5/Shack support before use.

## Game Logic / Global Info details from the official overview videos (added 2026-11-10)
See [guides/video-game-logic-and-global-info-overview.md](guides/video-game-logic-and-global-info-overview.md): the Starting/Standby/Started/Ended round-state loop, `On Round State Changed`, `Set Game Properties` fields (teams always scoring, force no scoring, cash reward/penalty, keep bodies, dynamic spawns, spawn ghosts, round time), `On Player Spawned` / `On Player Killed` signatures, the list of globally exposed functions (`Get Player Status`, `Spawn Item`, `Set Player Team`, `Load/Save String From/To File` on community servers, `Get UTC Time`...), and the Global Info (match-lifetime, replicated, `Get Global Info`, Limited Ammo Type, Disable Voting/Attach Mode, Custom Item Table, Player Skin Table). Older UE4-era videos; verify names against the Shack kit examples.

## Shack/UE5-era tutorial series detail (added 2026-11-10)
- Game logic + definition + mod.io publishing: [guides/majerati-gamelogic-and-publishing-ep3-and-customizing.md](guides/majerati-gamelogic-and-publishing-ep3-and-customizing.md) (`On Custom Game Mode Init` -> `Set Game Mode Properties` -> `Set Round State`; `On Round State Changed` switch; `Spawn And Possess Pawns`; wait-for-players loop; last-man-standing; **Shack maps go in `Quest Map`, upload platform Android**).
- Proxies, skins, spawn items, volumes, skin tables, custom hands, teleporters (grab/VIP), multi-use triggers: [guides/majerati-proxies-skins-volumes-teleports-multiuse.md](guides/majerati-proxies-skins-volumes-teleports-multiuse.md).
- Audio (WAV only in 5.1, looping, sound cues, attenuation): [guides/video-audio-background-music-and-3d-audio-SehhU3-X5fM.md](guides/video-audio-background-music-and-3d-audio-SehhU3-X5fM.md).
