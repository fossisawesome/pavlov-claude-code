# 12 - mod.io Guides: Full Triage and New Findings

Read 2026-11-03 from https://mod.io/g/pavlov/r. The page says "80 guides" but the infinite-scroll list only ever exposed **60**; 3 more were reached by slug from cross-references (`best-practices-for-shack-materials`, `modkit-version-upgrade-best-practices-post-511`, `custom-gun-guide`). **~17-20 guides remain unseen** (probably unlisted/hidden or older; the first guide listing is sorted newest-first). All 63 read were skimmed; the priority ones in full. mod.io's authenticated JSON API needs an api_key, so scraping used same-origin iframes. Images/screenshots are not captured: many guides are screenshot-driven, so node wiring is often missing from text.

**Full text of every tier A and B guide (46 files) is saved in [`guides/`](guides/)**, one file per guide, named by mod.io slug, each with source URL, author, views and tier in its header. Use the index at the bottom of this file. The sections below are summaries and cross-cutting findings; go to the saved file for exact steps and node names. Images are not included in the saved text.

Rating key: **A** = official/technical, accurate, directly useful for Shack work. **B** = decent community recipe, verify before use. **C** = low value, redundant, video/Discord-only, or risky.

## Tier A: read these

| Guide (slug) | Author | Why useful |
|---|---|---|
| `best-practices-for-shack-materials` | Pavlov technical artist (official) | Best Shack material guide (details below) |
| `optimization` ("Oculus/Shack and PC Optimization") | SmallDarkOne | Only source of actual **Quest budgets** |
| `custom-gun-guide` (+ Pre-setup, rigging, hand-sequence guides referenced) | official | Step-by-step custom gun BP creation with real class/variable names |
| `how-to-create-your-own-better-bolt-action-rifles` | BritishColonist | Source-plugin based advanced gun base; shows ModInitializer registration pattern |
| `pavlov-shack-custom-gun-development-guide` | jackpavlovmod2010 | Gun state classes/generic fields (see [06](06-custom-guns-items-skins.md)) |
| `modkit-30-faq-and-best-practices` | Juntistik99 (official) | UGC types, dependencies, Game.ini mods |
| `modkit-version-upgrade-best-practices-post-511` | Mark Dey (official) | How to update the kit without recooking |
| `421-to-511-upgrade-guide` | Juntistik99 | 4.21 to 5.1.1 porting |
| `how-to-fix-failed-to-package-for-android` | D1NIX | Debug packaging failures |
| `how-to-fix-pixelated-textures` | zaynethedev | Shack float-precision pixelation fix |
| `masked-materials-shack` | Marco_G17 | Alpha-to-coverage etc. |
| `gpu-lightmass` | markyxl | Much faster lighting bakes (PC with RT GPU) |
| `archery-modkit-guide` | KodaTheProto | Pattern for **source plugins**, `VRI_BowBase`, dependency setup |
| `conquest-mod-setup` | Brav_Soldat | Worked example of building a mode on top of Push |
| `video-tutorial-collection` | Juntistik99 | Index of official/community video series (all in [10](10-sources-and-video-index.md)) |

## Tier B: situational recipes

| Guide | Takeaway |
|---|---|
| `get-started-with-mods-maps` (Turdlar) | Orientation: knowledge splits into UE-generic / Pavlov Modkit / mixed / Blender. Points to MaJerati + BritishColonist videos. UE4 guides mostly apply to UE5. Free UE-marketplace models compatible with 5.1 |
| `money-system`, `easy-money-system`, `how-to-make-basic-custom-money-system`, `money-system-achievement-system` | Money = **replicated** variable on your custom PlayerInfo; set on server via GameLogic; cast to *your* PlayerInfo class (blueprint won't paste otherwise). Also `Set Player Cash` |
| `how-to-make-money-saving` (su-sukana) | Needs **community server**: override `Player Joined Server` -> `Break Pavlov Player Status` -> `Get Player Name` -> `Load String From File`; branch -> `Set Player Cash`; on `Event On Player Left Server` -> `Save String To File` (needs `bCustomServer=true`) |
| `how-to-disableenable-fall-damage` | GameLogic BeginPlay -> `Set Fall Damage` (target Pavlov Game Logic) |
| `how-to-disable-votekick`, `how-to-dissable-voting-better-then-kadens` | GlobalInfo: `Disable Voting` node on BeginPlay, or class default **Disable Voting** |
| `disable-radio` | PlayerInfo BeginPlay -> `Set Radio Channel`; channel 2 reserved for police/admin |
| `hiding-the-base-pavlov-scorebard` | Blueprint Function Library with soft class ref -> class ref conversion (`Conv_SoftClassPathToSoftClassRef`); long copy-paste node text |
| `how-to-make-a-basic-menu-for-beginners`, `pavlov-in-game-custom-menu` (MasterHyp, widely used), `how-to-create-a-ban-function-within-your-custom-pavlov-menu`, `locking-a-widget`, `how-to-make-a-scroll-menu-in-the-modkit` | Widget menu stack; MasterHyp menu = drop `PavlovVR_InGameCustomMenu` into Content, compile all, **move** into UGC plugin, Fix Redirectors, use its PlayerInfo; one GameLogic per level |
| `vrselection-guide` | VRSelection component glow |
| `how-to-do-custom-weapon-skins` (SmallDarkOne) | Skin System mod: only overrides default skins, not paid ones. **Avoid >1024x1024 on Shack**, instanced material, "Used with Skeletal Mesh" |
| `how-to-add-dependencies-to-you-modmapgamemode` | My Content -> Manage -> Dependencies -> Save |
| `how-to-make-a-teleporter`, `how-to-make-a-vip-teleporter`, `how-to-make-a-public-teleporter`, `buyable-door-wincrement-score-12`, `tired-of-copy-and-pasting-level-instances`, `how-to-fix-weird-sky-sphere` | Small recipes (trigger boxes; level instances; sky sphere from mod example map) |
| `practice-mode-custom-tools-guide` (Stevie257) | Building tools for a practice-mode mod (not read in detail) |
| `dynamic-shadows-2-mapping-guide` | PC only |
| `how-to-fix-materials-stretching` | WorldAlignedTexture/Normal nodes; check Shack cost before using |
| `please-read-if-you-make-custom-maps` | Security warning (see [05](05-mods-dependencies-servers.md)) |
| `how-to-host-pavlov-servers-on-windowslinux` | Docker hosting |

## Tier C: skip or treat with care
- Trivial/redundant: `how-to-open-pavlov-modkit`, `how-to-close-the-pavlov-modkit`, `how-to-import-uassets-into-your-ugc-simple`, `how-to-upload-in-the-pavlov-modkit` (the last is correct but trivial), `all-pavlov-ids` (copy of wiki ItemIDs).
- Video/Discord-only (no content in the guide): `how-to-host-your-forestracks-community-server`, `this-is-how-to-getmake-your-mods-ids` (youtu.be/7Dcuh3vqsJo), `how-to-useput-the-police-panic-button-radio-in-your-game` (youtu.be/WbrLmJR1STc), `how-to-make-custom-skins-for-shack-and-pc` (youtube 9S_ckWbUfXc), `how-to-make-a-gate`, `how-to-make-a-mirror-101`, `how-to-make-rgb-mat-in-ue5-101` (assets on a Discord).
- **Do not follow / legal-ToS risk**: `how-to-rip-mdl-files-from-garrys-mod`, `how-to-get-all-skin-models1` (Google Drive of game models), `how-to-skid` (points to Discord users, unclear/low-quality). Don't use ripped or redistributed assets in published content.
- `mod-downloader` (ModioDirect): third-party downloader, unvetted. `how-to-make-your-itemsmodles-into-blueprints` (GLB import; generic UE).

## New technical findings (merge into earlier docs)

### Quest budgets [V: `optimization`, SmallDarkOne]
| | Quest 2 | Quest 3 | PCVR (recommended) |
|---|---|---|---|
| Max triangles | 680K | 740K | 1.5M |
| Max draw calls | 400 | 500 | 1100 |
Measure **in game**, not in the editor (editor counts content-drawer stuff): put `Execute Console Command` nodes in a BeginPlay actor with `stat scenerendering`, `stat unit`, `stat summary` (memory), `stat detailed`. **Culling distance is effectively half on Shack.** Reduction toolbox: instancing/batching, fewer materials/atlases, LODs, merge actors, occlusion culling + cull distance volumes, simple collision, material instances, minimize transparency/overdraw, precomputed visibility volume around play space, lower volumetric quality.

### Shack material rules [V: official `best-practices-for-shack-materials`]
1. Only **Base Color** textures (texture sampling is expensive; normal/ORM wasted).
2. Force **"Fully Rough"** on the base material and disable **"Use Lightmap Directionality"** (forced off in game anyway). Approximate specular with a simple node setup if too dark. Keep full-quality materials for characters, weapons, key props.
3. Texture Sample sampler source **Shared: Wrap / Shared: Clamp**; set level textures to texture group **"Project Group 01"** (Shack level textures).
4. Put a **VertexInterpolator** between UV math (tiling multiplies) and the sampler; fixes headset-only pixelation from low float precision. Fallback: material Mobile tab -> **Float Precision Mode = Use Full-precision for every float**; texture group Weapon or World; republish.
5. For animated UVs use the Time node's **Period** (e.g. 2 x -0.5 panner = exactly one loop; or ~120 if loop length is unknown).
Note a texture-size discrepancy: wiki says 512 (downscaled above), skin guide says <=1024 for skins. Level textures: 512; characters/weapons may use more.

### Source plugins (new workflow) [V: archery + bolt-action guides]
Pavlov Workshop has a **"Download Source Plugin"** tab: pick a published mod's source (e.g. "Archery Modkit", "bolt") -> **Add To Project** -> restart editor. Then either (a) keep the plugin and set it as a **dependency** on your mod on mod.io, or (b) move its content into your UGC. Create `Pavlov_ModInitializer` BP, set it in the definition, override **Event On Mod Initialized** (guard with `Is Valid` on `Global Info`), register content. Archery base class: `VRI_BowBase` (components: Bow mesh, Top/Bottom String Root, Resting Pos; class default Bow Pivot Offset Z = -(RestingPos.Z + 5.5)). Bolt-action base: `Gun_BetterBoltActions_Base`, two magazines (full stripper clip + single bullet), "invisible grip" needs **your own unique ID** added in the mod initializer list. Make sure Pav examples sit in their normal location or dependencies break.

### Custom gun BP recipe (official `custom-gun-guide`) [V]
Create **child blueprints** (right-click base -> Create Child Blueprint) from `CustomMapTools/PavExamples/Guns`:
- `CustomMagazineBase`: Mesh component = loaded mesh; class defaults Normal mesh / Empty mesh, **MaxBullets**, MagSlide or MagSlap variables, rotation offset (start `0,-75,0`), **Sequence** + **Avatar (3rd-person) Sequence** (reuse another weapon's hand sequence or make one); then right-click asset -> **Scripted Asset Actions -> VRItem Update Avatar Anims** (auto-fills AvatarHandOffset/RotationOffset; requires both sequences).
- `CustomShellBase`: Mesh = empty shell; **MeshLive**; tick **RightVectorImpulse** (most eject right); SurfaceFX by size.
- `CustomBulletBase`: **InitialSpeed, Gravity, SurfaceFX** (ignore Hidden/Testing category; used by `BP_BulletTester`).
- `CustomGunBase` (`CustomHandgunBase` for pistols): Mesh = skeletal mesh; move **ReloadHandle** to charging handle, **MuzzleParticle** scale (0.9 default), **VRMagazineSlot** box (inside gun for MagSlide), **TwoHandGrip** box; class defaults **MagazineClass, ShellClass, BulletClass, StateClass** (usually `VRGunState`).
- If stuck, copy behavior from `CustomMapTools/PavExamples/Guns`.

### Other API/node names seen [V as quoted in guides]
`Set Fall Damage` (Game Logic), `Disable Voting` (Global Info), `Set Radio Channel` (PlayerInfo), `Set Player Cash`, `Break Pavlov Player Status`, `Player Joined Server` (override), `Event On Player Left Server`, `Load String From File` / `Save String To File` (community server only), `Event On Mod Initialized`, `Global Info`, `Execute Console Command`, `Conv_SoftClassPathToSoftClassRef`.

### Lighting speed-up (PC) [V: gpu-lightmass]
Project Settings: Windows Targeted RHIs = DirectX 12; Hardware Ray Tracing + Path Tracing on; do **not** enable virtual textures (incompatible with Shack); enable **GPU Lightmass** plugin; use **Build -> GPU Lightmass** (Full Bake), not Build All Levels. Differences: emissives light the scene, transparent materials may bake opaque, light does not leak through back faces.

### Conquest/Push rules (conquest-mod-setup) [V]
Uses `BP_PushCapArea` (`CustomMapTools/Blueprints/Push/CapAreaObjective`). Total cap areas = wanted objectives + 2 (bases). Objective 0 = team 0 base, last id = team 1 base. Unique Objective Id per area; max 6 cappable letters. Settings: Tick Amount (100/N = N seconds... as written), Cap in Vehicle. Every cap area needs spawns for both teams; fallback spawns supported. Pair with a "push time adjuster" mod.

## Index of saved guides (`guides/`)

### Tier A
- [Best practices for Shack materials](guides/best-practices-for-shack-materials.md)
- [Oculus/Shack and PC Optimization](guides/optimization.md)
- [Custom gun guide](guides/custom-gun-guide.md)
- [How to create your own better bolt action rifles](guides/how-to-create-your-own-better-bolt-action-rifles.md)
- [Pavlov Shack | Custom Gun Development Guide](guides/pavlov-shack-custom-gun-development-guide.md)
- [Modkit 3.0 FAQ and Best Practices](guides/modkit-30-faq-and-best-practices.md)
- [Modkit version upgrade best practices (Post 5.1.1)](guides/modkit-version-upgrade-best-practices-post-511.md)
- [4.21 to 5.1.1 Upgrade Guide](guides/421-to-511-upgrade-guide.md)
- [How to fix Failed To Package For Android](guides/how-to-fix-failed-to-package-for-android.md)
- [How to fix pixelated textures](guides/how-to-fix-pixelated-textures.md)
- [How to Improve Masked Materials on Shack](guides/masked-materials-shack.md)
- [GPU Lightmass](guides/gpu-lightmass.md)
- [Archery Modkit Guide](guides/archery-modkit-guide.md)
- [Conquest Mod Setup](guides/conquest-mod-setup.md)
- [Video Tutorial Collection](guides/video-tutorial-collection.md)

### Tier B
- [Get started with Mods & Maps](guides/get-started-with-mods-maps.md)
- [Economy/Money System](guides/money-system.md)
- [Easy Money System!](guides/easy-money-system.md)
- [How to make basic custom money system!](guides/how-to-make-basic-custom-money-system.md)
- [Money System: Achievement System](guides/money-system-achievement-system.md)
- [How To make money saving](guides/how-to-make-money-saving.md)
- [How to Disable/Enable Fall damage](guides/how-to-disableenable-fall-damage.md)
- [How to Disable VOTEKICK](guides/how-to-disable-votekick.md)
- [How to dissable Voting( better then Kadens)](guides/how-to-dissable-voting-better-then-kadens.md)
- [Disable Radio (in your custom map)](guides/disable-radio.md)
- [Hiding the base Pavlov Scorebard](guides/hiding-the-base-pavlov-scorebard.md)
- [How to make a basic menu for beginners!!! NOT FINISHED I TRIED HIDING](guides/how-to-make-a-basic-menu-for-beginners.md)
- [Pavlov In-Game Custom Menu (Updated)](guides/pavlov-in-game-custom-menu.md)
- [How to create a ban function within your custom Pavlov menu!](guides/how-to-create-a-ban-function-within-your-custom-pavlov-menu.md)
- [Locking a widget button (UPDATED 2x)](guides/locking-a-widget.md)
- [How to make a scroll menu in the modkit](guides/how-to-make-a-scroll-menu-in-the-modkit.md)
- [VRSelection Guide](guides/vrselection-guide.md)
- [Easy & Simple Custom Weapon Skins](guides/how-to-do-custom-weapon-skins.md)
- [How To Add Dependencies To You Mod/Map/Gamemode](guides/how-to-add-dependencies-to-you-modmapgamemode.md)
- [How To Make A Teleporter](guides/how-to-make-a-teleporter.md)
- [How to make a Vip Teleporter](guides/how-to-make-a-vip-teleporter.md)
- [how to make a public teleporter](guides/how-to-make-a-public-teleporter.md)
- [Buyable Door W/Increment Score](guides/buyable-door-wincrement-score-12.md)
- [Tired of Copy and pasting? / Level Instances](guides/tired-of-copy-and-pasting-level-instances.md)
- [How To Fix Weird Sky Sphere!](guides/how-to-fix-weird-sky-sphere.md)
- [Practice Mode Custom Tools](guides/practice-mode-custom-tools-guide.md)
- [Dynamic Shadows 2 Mapping Guide](guides/dynamic-shadows-2-mapping-guide.md)
- [How to fix materials stretching.](guides/how-to-fix-materials-stretching.md)
- [PLEASE READ IF YOU MAKE CUSTOM MAPS, YOU ARE EFFECTED.](guides/please-read-if-you-make-custom-maps.md)
- [How to host pavlov servers on Windows/Linux](guides/how-to-host-pavlov-servers-on-windowslinux.md)
- [[WIP] How To make a whitelisted function](guides/whitelisted-function.md)

Tier C guides were intentionally not saved (trivial, redundant, video/Discord-only, or ToS-risky); see the Tier C list above.

## Added 2026-11-10
- [Custom gun guide (Pre-setup)](guides/custom-gun-guide-pre-setup.md): tier A, read in full (confirms `VRGunAnimInstance`, sockets, ModifyBone/SlideTime steps).
- [custom-gun-guide](guides/custom-gun-guide.md) was re-saved with the complete text (previous save lacked nothing but was briefly overwritten; the "page truncated" claim in earlier notes was wrong).
- [Hey here's everything I know!](guides/hey-heres-everything-i-know.md): **tier C / security-sensitive**. Alt-account link dump by the author of the backdoored "Tools" mod; saved for provenance only. Contains a Drive link to that mod's files and to extracted skin models and a commercial add-on; **do not download**. Only reusable data: the attachment-flag table (already in the gun video guide) and unverified pause-menu coordinates.


## Update 2026-11-10 (API)
This triage was written from the 63 guides visible on the website. The API shows **82**, all now saved in `guides/`; the extra ones (incl. `modkit-faq`, `custom-vehicle-guide`, `common-mistakes-made-by-new-mapmakers`, the hand-pose guides, bipod/zoom, `pavlov-mod-studio`) are triaged in [13](13-modio-api-and-newly-found-guides.md). The tier C guides listed above are also saved now, with warning banners where needed.
