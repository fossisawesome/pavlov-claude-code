# 01 - Architecture and Concepts

## Versions and variants [V]

| Variant | Platform | Engine | Modkit branch | Definition field | Content platform tag on mod.io |
|---|---|---|---|---|---|
| Pavlov VR (PC) | Windows/Linux, Steam | UE 5.1.1 | `5.1.1` | `Map` | Windows (+Linux for server) |
| **Pavlov Shack** | Meta Quest (Android, arm64, Vulkan) | UE 5.1.1 | **`Pavlov-Shack`** | **`Quest Map`** | **Oculus** (client) + **Mac** (Shack dedicated server) |
| Legacy PC | Steam Workshop | UE 4.21 | `Pavlov-Legacy` / repo default | `Map` | obsolete; Workshop-based |

- Shack moved from UE4 to UE5 (Chaos physics) with mod.io support and an in-game mod browser. Some features were removed for performance ("Chaos is pretty fragile"). Release channels: `RC` (release candidate, newest) vs live.
- Quest has **no crossplay** with PC/PS5.
- The Modkit is a full UE project (`Pavlov.uproject`, `EngineAssociation 5.1`) with plugins: `CustomMapTools` (example blueprints, editor tools), `VRFramework`, `JsonUtils`, `modio_ue4`, plus engine plugins ApexDestruction, SteamAudio, ChaosVehiclesPlugin. Module `Pavlov` is Runtime. The Pavlov Workshop editor window lives under **Window -> Pavlov Workshop**. [V]
- Tutorial series note: the pavlovwiki "Getting Started" page still has UE4.21-era sections (Steam Workshop upload, FAQ). Treat the UE5.1.1 sections as authoritative and the UE4.21 parts as legacy.

## The three UGC types (Modkit 3.0) [V: mod.io "Modkit 3.0 FAQ and Best Practices" by Juntistik99]

| Type | What it is | Can depend on |
|---|---|---|
| **Map** | Level + definition. Either "legacy all-in-one" (map + its own game logic) or just a level when a custom Gamemode is used (its game logic is then ignored). Ticking **Custom** in the map's definition locks the map to its own GameLogic (a separate Gamemode cannot be loaded on it). | Mods |
| **Gamemode** | Overrides the GameLogic for a level. Definition points to a `Pavlov_GameLogic`. | Mods |
| **Content Mod** | Standalone content (assets, items, guns, level geometry). Has a `Pavlov_ModInitializer`. Must not rely on maps/gamemodes/mods. Should not alter the gameplay loop (use a Gamemode for that). | nothing |

Dependencies are one-way and set on the mod.io page (edit pencil -> Dependencies). Both dependency and dependent must be **Live** and published for the **same platform**. A Shack map using a PC-only mod will fail to load. Players auto-download dependencies before joining.

## Folder layout [V]

- Each UGC is a **plugin content folder**: `Plugins/UGC<id> Content/` (UE5). Creating a mod via Pavlov Workshop -> **Create Mod** generates it, with a unique `UGCxxxxxxx` code (the mod.io id). Wiki/legacy docs also mention `SVR_<name>` folders for Shack on the 4.21 kit. [V, legacy]
- **ALL assets used must live inside the UGC folder** or they will not be packaged. Do not nest UGC folders (path-length problems).
- The definition file is a Data Asset of class `Pavlov_Map` (lowercase name `definition`), placed directly inside the UGC folder. [V]

## Definition file fields [V]

| Field | Meaning |
|---|---|
| Unique Id | Do not change; `UGC<id>` |
| Label | Display name |
| Version | Bump when updating |
| Thumbnail | 512x512 |
| Map | PC level |
| **Quest Map** | **Shack level** (link this for Shack) |
| Hidden | Hide from map combo boxes |
| Compatibility | Game-mode tags used to filter the map browser (Custom, Deathmatch, Team Deathmatch...). Tags matter in-game; do not tick modes the map is not built for (Prop Hunt, Push...) |
| Custom Game Mode / Label | Force bare-bones mode; everything handled by your GameLogic; label shown in server browser |
| (Gamemode/Mod UGCs) | Assign `Pavlov_GameLogic` (Gamemode) or `ModInitializer` (Mod) |

## Core Blueprint class model [V from wiki + kit file names; behavior details [D]/[?]]

| Class | Role | Notes |
|---|---|---|
| `Pavlov_GameLogic` (a.k.a. "Pavlov Game Logic" actor) | Server-side match controller: round state events, player join/leave/kill, spawning, team auto-set, win checks | Placed in the level; assign Definition, Global Info Class, Player Info Class, Player Proxy Class. Examples: `Pavlov_GameLogic_Example`, `GL_Base`, `GL_Deathmatch`, `GL_TeamDeathmatch`, `GL_GunGame`, `GL_KOTH`, `GL_Zombies`, `GL_SingleRespawn`, `GL_Advanced`, `GL_FobExample` |
| `Pavlov_GlobalInfo` (example `CMP_GlobalInfoExample`) | Global per-match data/config: custom items table, player skin table, etc. | Spawned even if unset |
| `Pavlov_PlayerInfo` (`CMP_PlayerInfoExample`) | Per-player persistent data (cash, custom vars). Money system tutorial adds custom events here | |
| `Pavlov_PlayerProxy` (`BP_PlayerProxyExample`) | Per-player pawn-side logic: loadout, skins (`Set Player Skin`), UI/interactor attach, OnPlayerDeath | Server-authoritative; use switch-has-authority + delay on BeginPlay |
| Hand proxy (`BP_HandProxyExample`) | Per-hand logic | Used with widget interaction menus |
| `Pavlov_ModInitializer` | Content-mod entry point. Created on client and server, **not replicated**. Override `OnModInitialized` to register custom guns/items, access GlobalInfo and GameLogic | `Mod_Initializer_TTTRoles_Example` is a kit example |
| `Pavlov_Spawn` | Player spawn actor (TeamID, Dynamic, Only Team, Special flags) | |
| `PMF_MapEntryPoint`-style helpers | Community Infection kit uses these | third-party |

Replication model: standard UE multiplayer. Game logic runs on the server; client-only actions (menus, widgets) are done through run-on-owning-client events from the proxy. [V from the "Replacing the scoreboard" wiki guide: `callDoGiveInteractor` not replicated, `doGiveInteractor` run on client.]

## Platform/engine settings the kit ships (Pavlov-Shack branch `Config/DefaultEngine.ini`) [V]

`r.MobileHDR=False`, `r.ForwardShading=True`, `r.MobileMSAA=4`, `vr.MobileMultiView=True` (+`.Direct`), `r.Mobile.AllowMovableDirectionalLights=False`, `r.MobileNumDynamicPointLights=0`, `r.Mobile.EnableStaticAndCSMShadowReceivers=False`, Android: `MinSDKVersion=26`, `TargetSDKVersion=28`, `bBuildForArm64=True`, ES31 off, Vulkan on, `PackageForOculusMobile=Quest2`, ASTC textures. Also `Config/Android/*`, `DefaultDeviceProfiles.ini`, `DefaultScalability.ini`. The kit also ships `Releases/PavlovShack_1.0.0` and `Pavlov_1.0.0` and `Plugins/CustomMapTools/Binaries/{Android_ASTC,LinuxServer}` (pre-built target binaries). Do not change these casually.
