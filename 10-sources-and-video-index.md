# 10 - Sources and Video Index

## Primary documentation
- Wiki main: https://pavlovwiki.com/index.php/Main_Page. **Trick: raw wikitext** via `http://pavlovwiki.com/index.php?title=<Page>&action=raw` (curl works; much better than WebFetch summaries). Pages used: Getting_Started, ItemIDs, Community_Modkit_Tools, Community_Gamemodes, Workshop_troubleshooting, Helpful_Videos, Making_Skins, Custom_Guns, Changing_the_character_model, Replacing_the_scoreboard, Modeling_in_Blender, Bot_Navigation, Quest_Troubleshooting, Gamemodes, Default_Maps, Weapons, Vehicles, Attachments, Pavlov_TV_API, PC_Mod_Managers, Setting_up_a_dedicated_server, Rcon_Overview_and_Commands, Game_Settings, Update_Changelog. (Local copies existed only in a session scratchpad; refetch with the URL pattern.)
- Modkit repo: https://github.com/vankruptgames/PavlovVR-ModKit (branches `Pavlov-Shack`, `5.1.1`, `Pavlov-Legacy`). Tree via `https://api.github.com/repos/vankruptgames/PavlovVR-ModKit/git/trees/Pavlov-Shack?recursive=1` (response was truncated: 3118 entries; use `contents` API for subfolders). Raw files: `https://raw.githubusercontent.com/vankruptgames/PavlovVR-ModKit/Pavlov-Shack/<path>`. README only links a class-overview playlist: https://www.youtube.com/playlist?list=PLsnITcSCPeMo37POY0NSJWHZ8qfH7tWHD
- Balance table repo: https://github.com/vankruptgames/BalancingTable
- mod.io: https://mod.io/g/pavlov/r (80 guides, SPA lazy-loaded; scrape in a real browser, e.g. iframe + innerText). Mod pages `https://mod.io/g/pavlov/m/<slug>`.
- Press: Road to VR "Pavlov Shack Revamps Modding, Now on the Official Meta Quest Store" (UE5 move, Modkit 3.0 multi-mod servers, mod.io crossplay downloads, PC still needed for authoring).
- Unofficial legacy guide (4.21): linked from wiki Getting_Started (Google Doc).
- Discords: https://discord.gg/pavlov-vr (#workshop-help, #shack-mapping-help), Pavlov Artists (resources/bake maps), PavlovScore.

## mod.io guides read (relevant to Shack)
| Slug | Topic |
|---|---|
| 421-to-511-upgrade-guide | Port UE4.21 content to 5.1.1 |
| modkit-30-faq-and-best-practices | UGC types, dependencies, game.ini, RCON mods |
| pavlov-shack-custom-gun-development-guide | Gun BP generic fields/state classes (Oct 2026) |
| how-to-fix-failed-to-package-for-android | Android cook failures |
| masked-materials-shack | Alpha to coverage etc. |
| how-to-upload-in-the-pavlov-modkit | Upload with Android platform |
| please-read-if-you-make-custom-maps | Tools mod backdoor warning |
| dynamic-shadows-2-mapping-guide | PC-only dynamic shadows |
| money-system-achievement-system | Player cash events |
| how-to-host-pavlov-servers-on-windowslinux | Docker server |
| vrselection-guide | Selection glow component |
| tired-of-copy-and-pasting-level-instances, how-to-fix-weird-sky-sphere, how-to-import-uassets-into-your-ugc-simple, how-to-make-a-public-teleporter, all-pavlov-ids | Misc |
Not yet read (titles only): how-to-create-your-own-better-bolt-action-rifles, how-to-host-your-forestracks-community-server, whitelisted-function, locking-a-widget, how-to-make-a-scroll-menu-in-the-modkit, how-to-make-a-gate, buyable-door-wincrement-score-12, how-to-get-all-skin-models1, this-is-how-to-getmake-your-mods-ids (video youtu.be/7Dcuh3vqsJo), police panic button radio, how-to-skid, voting disable, plus ~50 more of the 80 (use the page's Sort/Filter, scroll to load).

## YouTube playlist A: "Pavlov Modding Tutorials" (MaJerati, UE 5.1.1 Modkit 3, 2023) PLYnjmKV0nHWGAfzKYR40Ahx8G1D6TsT9D
Watch URL: `https://www.youtube.com/watch?v=<id>`. Only descriptions/chapters read; transcripts unavailable (caption fetch returned empty). [D]
| # | Id | Title |
|---|---|---|
| 1 | 4NXrmgKthq4 | Setting up Pavlov Modkit 3 (UE 5.1.1) |
| 2 | ED8MG83XFTg | Building a basic map (spawns, kill zones) |
| 3 | s31d9npfiOs | Basic custom GameLogic & mod.io (GameLogic, GlobalInfo, Proxy, publishing) |
| 4 | R_NpSnUqS2k | Player proxies, spawning guns, skins |
| 5 | Tti273LnaHc | SkinBoxes, WeaponBoxes, variables |
| 6 | F7bzjno2A08 | Build lighting and revert to old files |
| 7 | 7kL7k7nwOW8 | Teleports, interact boxes, VIP teleporters (00:15 basic, 10:28 grab, 15:50 VIP) |
| 8 | 4rGOKs-sP2A | OBSOLETE LSWCM (use 1TYkJzv6-XI) |
| 9 | UnKNe8L-P0g | Custom skins & tables, hands, skeletal meshes |
| - | Zp8d4JYgDLs | How NOT to spawn a chicken |
| - | t--gr9uJR1o | Spawning chickens & multi-use BPs (switch statements) |
| - | hjrBEUrNhV4 | Custom skins (Auto-Rig Pro) |
| - | SehhU3-X5fM | Background music & 3D audio |
| - | aubVoeG8geQ | Basic money system |
| - | VM0ZFpByeMA | Customizing custom GameLogics (init, round states, spawning, last-man-standing, reset) |
| - | TOHa12MQ6mQ | OBSOLETE keycard door |
| - | 9PrRyTpZhPk | Better keycard door system |
| - | 1TYkJzv6-XI | New LSWCM & VSWCM setup |

## YouTube playlist B: 2025 "[Future]" series for PC and Shack PLl8BNAEpjVUHTO5kJgLSHP05eHeLYDedO
| Id | Title (chapters) |
|---|---|
| kg0hw5ni-O0 | Setting up your first map (needs, install UE, modkit, mod.io account, login, create UGC, map, reflections & lighting, game logic, spawns, thumbnail, definition, upload, mod.io page, in-game test), 14 min |
| 0eJ1j0JRF2Y | Creating and using content mods (shared assets, mod initialiser, editing stats of existing guns, using content mods), 6 min; read pinned comment |
| J5u3qoJXzD0 | Rigging custom guns (reference mesh, vertex groups, two rigging methods, export) |
| nxw2cP2fICQ | Creating custom guns, 35 min (see [06](06-custom-guns-items-skins.md)) |
| tyzYy1YMMbk | Custom gun LODs (56 s) |
| txxWu3t-ROg | Custom hand poses (first/third person sequences) |
| jJfGH65y1J8 | How to create a push map (settings, loadout proxy, objective theory/setup, spawn points, OOB volumes) |
Other videos from the wiki Helpful_Videos: tv1Oof5MoQA (Sir Daddy Spankus, 2020), FGcqxa5ZGdU (BritishColonist setup), g6qwk1vJ488 / XvDfRuYXI10 / KlxXufos_-M (Mark Dey: Game Logic / Global Info / Custom Items overviews, older kit), tdfxZ2XUYGE (UV/lightmap black areas), NP7XnnIvkOs (Substance 3D).

## Video processing status (updated 2026-11-10)
Processed from auto-captions + pinned comments (no frames): `nxw2cP2fICQ` (creating custom guns), `J5u3qoJXzD0` (rigging), `tyzYy1YMMbk` (LODs), `txxWu3t-ROg` (hand poses). Guides: see `guides/video-*.md`; transcripts: `transcripts/`. Still title/chapter-only: all of playlist A (MaJerati) and `kg0hw5ni-O0` (first map), `0eJ1j0JRF2Y` (content mods), `jJfGH65y1J8` (push map). Also referenced but not processed: torskeravn rigging tutorial https://youtu.be/7Vr1YFqxPmE.
- Processed 2026-11-10 (captions only): `KlxXufos_-M` (Custom Items overview, UE4-era) -> guides/video-custom-items-overview-KlxXufos_-M.md. Sibling videos from the same series, not yet processed: `g6qwk1vJ488` (Game Logic overview), `XvDfRuYXI10` (Global Info overview).
- Processed 2026-11-10 (captions only): `g6qwk1vJ488` (Game Logic overview) and `XvDfRuYXI10` (Global Info overview) -> guides/video-game-logic-and-global-info-overview.md. The series' later video (Player Proxy and skins) is not on the wiki's list; search the uploader "Lance S" / Vankrupt channel if needed.
- Processed 2026-11-10 (captions only, no frames): playlist A videos `s31d9npfiOs` (Ep.3), `VM0ZFpByeMA`, `R_NpSnUqS2k` (Ep.4), `Tti273LnaHc` (Ep.5), `7kL7k7nwOW8` (Ep.7), `UnKNe8L-P0g` (Ep.9), `t--gr9uJR1o`, `SehhU3-X5fM`. Still unprocessed from playlist A: `4NXrmgKthq4` (Ep.1 setup), `ED8MG83XFTg` (Ep.2 basic map), `F7bzjno2A08` (Ep.6 build lighting), `Zp8d4JYgDLs` (chicken, superseded), `hjrBEUrNhV4` (custom skins, Auto-Rig Pro), `aubVoeG8geQ` (money system), `9PrRyTpZhPk` (keycard door), `1TYkJzv6-XI` (LSWCM), obsolete `4rGOKs-sP2A`/`TOHa12MQ6mQ`. Playlist B unprocessed: `kg0hw5ni-O0` (first map), `0eJ1j0JRF2Y` (content mods), `jJfGH65y1J8` (push map).
- Transcripts in `transcripts/` were re-cleaned (doubled rolling-caption text collapsed) on 2026-11-10; some stutter remains.

- mod.io API (key-based) is the reliable way to read guides and mods: see [modio-api/README.md](modio-api/README.md). The website guide list stalls at 30/60 of 82.
