# 03 - Map-Making Workflow (Shack)

Source: pavlovwiki "Getting Started", Workshop_troubleshooting, Bot_Navigation, mod.io guides, MaJerati Ep.1-3 and 2025 "Setting up your first map" video (kg0hw5ni-O0, chapters). [V unless noted]

## Steps
1. **Create Mod**: Pavlov Workshop -> Create Mod -> name/description (logo optional for maps). Choose type Map / Gamemode / Mod. Generates `UGCxxxxxxx`.
2. Open the UGC folder in Content Browser, create a level (Ctrl+S saves; default name `NewMap`). Put the level **inside the UGC folder**.
3. Add basics: `BP_Sky_Sphere` (Engine content; or copy the nicer sky sphere from CustomMapTools mod example map, per mod.io "Fix weird sky sphere"), Directional Light, Sky Light.
4. Open `definition`: set Label, link **Quest Map** to your level (Shack) (and/or Map for PC), set Compatibility tags / Custom.
5. Place **Pavlov Game Logic** actor; set Definition = your definition; Global Info Class = `Pavlov_GlobalInfo`, Player Info Class = `Pavlov_PlayerInfo`, Player Proxy Class = `Pavlov_PlayerProxy` (or your subclasses).
6. Place **Pavlov_Spawn** actors (see flags below).
7. Place mandatory entities (below), build lighting, save.
8. Upload: Pavlov Workshop -> **Upload Mod** -> pick UGC -> platform **Android** (Shack) / Windows (PC) -> change notes -> Stage (local test) or Upload.
9. On mod.io: My Content / My Teams -> Edit -> name, summary, logo -> **Go Live**. (Separate logo from the in-game thumbnail.)
10. Test in Shack (RC channel). If stale, delete the map folder on the Quest, restart, re-upload.

## Spawns (Pavlov_Spawn)
- TeamID: -1 any, 0 Blue (defenders / Allied in WW2 TDM), 1 Red (attackers / Wehrmacht).
- Dynamic: tick for Deathmatch (avoids spawning inside players).
- Only Team: with TeamID restricts spawn; needed for S&D.
- Special: marks S&D team spawn; **only one per team**; allows 5-10 players from one spawn.
- Red/white "Bad size" label = spawn clipping into geometry. Raise slightly off floor (press **End** to snap then lift a couple of inches) and fix collision.
- No/wrong spawns => players dumped into the `Datacenter` map.

## Mandatory / common actors
- **Lights**: must all be **Static** (no Stationary/Movable). Sky/Directional "Indirect Lighting Intensity" 2-6 for VR clarity. Editor lighting is inaccurate: **Build -> Build All Levels** (or Lighting Only) to preview. Unlimited light count.
- **Reflection Captures** (sphere/box): required, otherwise weapons render black. Dark guns fix: overlap capture with playable area; or giant sphere capture + smaller ones per room; or bright hidden room trick (10x10x10 m, ~200k-300k unit lights) as fallback.
- **Bomb plants** for SND: >=1, up to A/B (`Is B` checkbox). Bomb sits at root of red arrow, leave ~5 units from wall.
- **KOTH**: `BP_KOTHObjectiveProxy` (hill) and optional `BP_KOTHSettingsProxy` from CustomMapTools content (enable "show plugin content").
- **Materials**: Physical Materials set bullet behavior (default and **thin** variant lets bullets pass). Use the **Shack-specific materials** (`M_Shack_*`) and instances.
- **Bot navigation**: one **Nav Mesh Bounds Volume** covering all walkable space; do **not** edit its details; **P** shows nav; `Nav Link Proxy` bridges disconnected areas (one-way option).
- **Blocking Volumes**: invisible walls, ramp over stairs (prevents VR camera hopping), smooth narrow areas.
- **Pavlov Kill Volume**: 1000-2000 units below the map; also hazards (lava, trains).
- **Pavlov Ladder Volumes**: player sticks to collidable surfaces in volume; rectangular only; don't overlap.
- **Level Instances** (mod.io guide): select actors -> right-click -> Levels -> Create Level Instance; editing one updates all copies. Great for repeated buildings.

## Mode-specific kit blueprints (CustomMapTools/Content/Blueprints) [V file names]
`BP_CTFProxy`, `BP_CTFSettings`, `BP_HNTObjectiveProxy` (Hide), `BP_PropVolume`, `Util_PropHuntOrganizer`, `BP_LootSpawnerProxy`, `BP_Door`, `BP_Destructible`, `BP_FireExtinguishVolume`, `BP_InstanceTool`, `BP_TraitorActionProxy`, `BPI_MatchRounds` (interface), `BPFL_PavlovTemplate` (function library), TTTv2 (`ExampleTTTv2Items`), Push (`BP_PushSettings_Example`, `BP_PushLoadoutProxy_Example`, `BP_PushObjective_Example`, `BP_Push_Objective_Actor`, `BP_PushCapArea`, advanced objective example). Push map video: jJfGH65y1J8 (settings, loadout proxy, objective theory/setup, spawn points, out-of-bounds volumes). [D]

## Migrating a map from another UE project
Right-click level -> Migrate -> choose the UGC folder as destination -> right-click Content root -> **Fix Up Redirectors in Folder** -> open ALL Blueprints and recompile -> close/reopen and check output log. Move files in small groups; re-run fix up each time. Copying to a new UGC: rename the folder to the new UGC id, fix redirectors, recompile BPs, then copy the Content folder.

## Gotchas
- Definition must sit directly in UGC folder; only one primary UGC folder when staging.
- Changing the definition later: update every reference (game logic in level too).
- `Network Checksum mismatch`: server must run the same map version; restart server; delete cached map folder from Quest; reboot Quest; rejoin. (PC: unsub/resub.)
- Level Instance / copy-paste maps get nicer lighting via lightmass settings; keep UV0 in 0-1 or textures look pixelated on Quest. Black patches after Build = UV/lightmap UV (see UE lightmap UV channel video tdfxZ2XUYGE referenced by wiki).
