# 11 - Gaps, Caveats, How to Close Them

## What was NOT verifiable from outside the editor
1. **Exact Blueprint API** of `Pavlov_GameLogic`, `Pavlov_PlayerProxy`, `Pavlov_PlayerInfo`, `Pavlov_GlobalInfo`, `Pavlov_ModInitializer` (event/function names beyond: `OnPlayerSpawned`, `OnPlayerDeath`, `OnModInitialized`, `Set Player Skin`, `Set Player Cash`, round-state events). The source module is closed. **Close the gap**: install the Pavlov-Shack Modkit, open example BPs (list in [04](04-gamelogic-proxies-modinitializer.md)), or drive the editor through the available `mcp__unreal-engine__unreal` MCP tool to enumerate classes/functions (`.uasset` files are binary and cannot be read as text).
2. **Video contents**: videos are being processed one batch at a time via local captions (no frames viewed). Done so far: see transcripts/ and the video-* files in guides/. Remaining ones in 10-sources-and-video-index.md are still title/chapter-only.
3. **Quest on-device test workflow**: no documented ADB/sideload dev flow. Known flow is upload to mod.io -> download in Shack (RC channel). Stage option in Workshop window may output a local pak (unverified location).
4. **Performance budgets** (tris, draw calls, memory, max map size) for Quest: not documented. Known only: 512 px textures, static lighting, Shack materials, masked-material tips.
5. **Which PC features are absent on Shack** (e.g., vehicles, destructibles, specific game modes, item IDs): not enumerated; "Why has [Feature] been removed?" answer is only "performance / Chaos physics".
6. **Python in editor**: the Shack gun guide mentions Python property names; whether the Modkit editor supports Python scripting for tooling is untested.
7. **Many wiki frameworks are UE4.21-era** and flagged "only works in 4.21"; porting status to UE5/Shack unknown.
8. mod.io guides: **all 82 now saved** via the API (see [13](13-modio-api-and-newly-found-guides.md)); images are downloaded for 27 high-value guides (guides/images/), links only for the rest. Wiki pages `Game_Settings`, `Pavlov_TV_API`, `PC_Mod_Managers`, `Weapons`, `Default_Maps`, `Gamemodes` (game-mode rules) only skimmed.
9. Wiki `Custom_Guns` page is truncated mid-guide; the full guide is the mod.io "custom-gun-guide" (URL partly mangled in the wiki) plus the 2025 videos.
10. Possible inconsistencies between sources: wiki Getting_Started says folder prefix `UGC` (PC) / `SVR` (Shack) for the old kit; Modkit 3.0 uses `UGC<modio id>` for everything. Press said Shack launched on the Meta store; one third-party listing said free vs $19.99, ignore.

## Suggested next research steps
- Install Modkit and dump class hierarchy/function lists into a doc (highest value).
- Transcribe the 25 videos; update docs 03/04/06 with exact node names.
- Read remaining mod.io guides (use browser scroll; guides list lazy-loads) and Pavlov Discord pinned messages in #shack-mapping-help.
- Check the repo's `Releases/PavlovShack_1.0.0` contents and `Config/Android/*` for packaging/budget hints.
- Verify guide dates (docs written 2026-11-03; kit and RC channel change often; check `Update_Changelog` and the repo commit log).
