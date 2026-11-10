# 08 - Troubleshooting Lookup

Mostly from wiki Workshop_troubleshooting / Getting_Started FAQ / Quest_Troubleshooting and mod.io "Failed to Package for Android". [V]

| Symptom | Fix |
|---|---|
| Map not in Offline map list | Definition exists in the UGC folder; Game Logic placed in map; definition linked in Game Logic; level linked in definition (Shack -> **Quest Map**); right game-mode tags (untick Custom if not custom) |
| Loaded into `Datacenter` | Missing/incorrect spawns for the mode; (PC) workshop item not Public/Unlisted; removed/privated dependency mod |
| "Definition not found" | UGC id mismatch; definition not directly in UGC folder; multiple UGC folders; save/reopen project |
| Map not loading, goes to lobby | Definition link; Game Logic missing |
| **Failed to Package for Android** | Message is not the real error. Open Output Log, scroll up to first `Error:` / `PackagingResults: Error:` / `Ensure condition failed` / `Unknown Cook Failure`. Suspects: corrupt WAV/OGG (BulkData/Invalid Payload), imported/skeletal meshes, materials, BPs with compile errors, migrated assets. Remove newest assets one by one. Fix up redirectors, Save All, restart. Delete **Saved** and **Intermediate** (never Content). |
| Textures/models missing or invisible | Assets outside UGC folder; unresolved redirectors (Fix Up Redirectors); Shack not using Shack material instances; test by deleting everything except Content and re-extracting the kit; check collision |
| Build -> large black areas | Lightmap UV problems; EngineFix dll if actors vanish after Build All |
| Weapons/items nearly black | Add reflection captures overlapping play area (see [03](03-map-making-workflow.md)) |
| "Bad size" spawn label / cannot pass visually open areas | Spawn clipping; collision; reload project; nudge meshes and rebuild |
| Map file size only a few MB | Assets not in UGC folder; cook/stage error |
| Network Checksum mismatch | Server runs same version; restart server; delete `Android/data/com.vankrupt.pavlovbeta/files/maps/SVR_<name>` on Quest; reboot Quest; rejoin |
| Shack map doesn't show/update | Delete the map from the Quest, open/close Shack, re-upload; overwriting is not always enough |
| Import stuck at 100% | Import into a different folder |
| "preload dependency data ... Event Driven Loader" | Disable event-driven loading (project settings) or use newest modkit |
| Moving map into new project breaks | Migrate into Content, move into UGC, **Fix Up Redirectors**, recompile all BPs |
| Mod.io Send button does nothing | Antivirus blocking; whitelist |
| Quest app update loops / won't start | Delete app data, uninstall, reboot, reinstall; remove other branches/accounts; uninstall Live before RC; factory reset last resort |
| Grey checkerboard gun skin | Material "Used with skeletal mesh" |
| Bots don't move | Nav Mesh Bounds Volume missing or edited; unconnected areas need Nav Link Proxy |
| Bow logic etc. break | Known incompatible in TTT, SND, HIDE, PUSH, PROPHUNT (legacy bow kit) |

Where to ask: Pavlov Discord `#workshop-help`, `#shack-mapping-help` (https://discord.gg/pavlov-vr); TTCM Modding Community (https://discord.gg/XUGqgf72he); support@vankrupt.com. When asking, post the **first real error** in the Output Log.
