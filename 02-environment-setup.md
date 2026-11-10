# 02 - Environment Setup (Windows PC authoring for Quest)

## Accounts [V]
1. **Epic Games** account + Epic Games Launcher.
2. **mod.io** account (https://mod.io/g/pavlov). **Verify the email** or you cannot create maps.

## Unreal Engine [V]
- Install **Unreal Engine 5.1.1** (exactly; Shack and PC both use 5.1.1) from the Epic Launcher.
- During install tick: **Starter Content, Engine Source, Android (required for Shack), Linux**.
- (Legacy only: UE 4.21.x.)

## Modkit [V]
- Download ZIP of the **Pavlov-Shack** branch: https://github.com/vankruptgames/PavlovVR-ModKit/tree/Pavlov-Shack (PC kit is `/tree/5.1.1`).
- Extract to a **short path** (path length causes issues), open `Pavlov.uproject`. First load sits at ~45% while shaders compile; wait.
- Repo also has a YouTube "class overviews" playlist (linked in its README): https://www.youtube.com/playlist?list=PLsnITcSCPeMo37POY0NSJWHZ8qfH7tWHD (not reviewed).

### EngineFix (the "Build All hides actors" bug) [V]
Copy `EngineFix/UnrealEditor-UnrealEd.dll` over `<UE_5.1>/Engine/Binaries/Win64/UnrealEditor-UnrealEd.dll`. It fixes actors being hidden after **Build -> Build All Levels**.

### Login [V]
Window -> **Pavlov Workshop** -> Account tab -> accept mod.io ToS -> enter email -> paste the emailed code. (If "Send" does nothing, antivirus can block it; reported fix on mod.io.)

## Upgrading from 4.21 content [V: mod.io "4.21 to 5.1.1 Upgrade Guide"]
Condensed: install UE 5.1.1 -> extract new kit -> copy only old `Content` over new `Content` -> login -> Create Mod -> **move** old UGC folder into `Plugins/UGCxxxxx Content` -> Fix up redirectors -> set new definition (link map, name, game modes) -> rename old UGC folder (no nesting) -> **Build All Levels** with UE5 lightmass -> replace old definition references (also in Game Logic in the level) -> select correct game-mode tags -> fix up redirectors again -> Upload Mod tab: select UGC, change notes, platform -> Stage or Upload.

## Android/Quest notes
- Packaging for Shack = "Android" target in the Pavlov Workshop Upload tab (ASTC textures). Failed cook is the usual blocker: see [08](08-troubleshooting.md).
- If the Workshop says "Pavlov installation not found" for a Shack build (legacy 4.21 workaround): create `steamapps\common\PavlovVR\Pavlov.exe` blank file in any Steam library and restart UE. [V, legacy]
- For on-device testing/diagnostics: Quest map cache lives at `...\Internal shared storage\Android\data\com.vankrupt.pavlovbeta\files\maps\SVR_<MapName>` [V]. Quest users opt into the **RC** release channel to get the newest Shack. No Quest sideload/dev workflow was documented (see gaps).

## Other tools [V]
- **Blender** (free) for modeling; export FBX with Z-up, scale 100x if unit issues, "Limit to Selected", path mode Copy. Kit ships `Blender/AnimConverter`. A Blender MCP is available in some Claude setups.
- Textures: ambientcg.com, polyhaven.com. Substance Painter / Quixel Mixer / Blender for skins.
- Auto-Rig Pro (Blender add-on) used by tutorial author for character skins.
- QuickBMS on a staged `.pak` finds oversized files (SizeMap misses post-resize size).
