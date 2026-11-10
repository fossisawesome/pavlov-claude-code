# 06 - Custom Guns, Items, Attachments, Skins

Sources: wiki `Custom_Guns` (by Ceezy; partial page), `Making_Skins`, `Changing_the_character_model`; mod.io "Pavlov Shack | Custom Gun Development Guide" (jackpavlovmod2010, Oct 2026), "How to create your own better bolt action rifles" (BritishColonist), "How to do custom weapon skins" (SmallDvrkOne, skin system); 2025 video series (chapters). Kit examples under `PavExamples/`. Advanced topic: learn the AK47 example first.

## Custom gun pipeline [V wiki] (follow with 2025 videos nxw2cP2fICQ / J5u3qoJXzD0 / tyzYy1YMMbk)
1. **Import assets**: gun = *skeletal mesh*; magazine (full + empty) and shell casing (full + empty) = static meshes. Bone naming free but follow example (`b_gun_Root`).
2. **Physics asset**: enable primitives + all bones; add Box shapes covering the gun on the root bone; set **"Simulation Generates Hit Events" = true** (drop sounds).
3. **Skeleton sockets**: on root bone add `Magazine`, `MagInsert`, `ShellEjectionSocket`, `Muzzle`, `Suppressor`; on charging-handle bone add `Chamber`, `ChargingHandle`. Preview-asset the magazine on `Magazine`; position `MagInsert` where insert animation begins; `Muzzle` at barrel end, **X-facing**; `Suppressor` slightly inside the barrel.
4. **Animation Blueprint** (`ABP_*`) driving bones from gun variables.
5. **Gun blueprints**: Gun, Magazine, Shell, Bullet BPs (see `Gun_AK47_Example`, `Magazine_AK47_Example`, `Shell_AK47_Example`, `Bullet_AK47_Example`).
6. Video chapter checklist (nxw2cP2fICQ): reload handle, mesh location, magazine slot, two-hand grip, mag/shell/bullet refs, gun state, inventory slots, attachments, sound effects (+custom), recoil (+fix, in-editor test), fire mode, hand poses, class defaults, **adding guns to the list** (via ModInitializer / item table), test in game. Rigging: J5u3qoJXzD0 (vertex groups, rigging methods, bone centering, export). LODs: tyzYy1YMMbk. Hand poses (first/third person sequences): txxWu3t-ROg.

## Gun Blueprint technical reference (Shack) [V mod.io, Oct 2026]
Generic fields on gun BPs: `GenericScalar1/2` (float), `bGenericFlag1/2/3` (bool), `GenericVector1/2`. Meaning is **weapon-specific, mostly animation**; there is no universal meaning. Verified usage examples:
- M4: Scalar2 = ReloadHandle X -> anim select; Flag1 handle grab/ungrab; Flag2 HasAttachment; Flag3 name compare.
- MG42: Scalar1 dust-cover rotation; Scalar2 `b_gun_belt` Y translation; Flag1 BeltInPlace; Flag2 belt-grab blend; Flag3 bHasMagazine. PKM similar.
- Revolver: Flag1 cylinder open; Flag2 chamber/reset blend. Shotgun: Scalar1 chamber/pump; Scalar2 feeder bone alpha. MP40: Scalar1 ReloadHandle X.
Gun **state classes**: `VRGunState` (AK47, M4, M9, MP40, MP5, MG42, PKM, M1 Garand, M1A1), `RifleGunState` (Kar98), `RevolverGunState`, `PumpActionGunState` (shotgun).
Implementation notes: trace Event -> Field write -> AnimBP reader -> Bone/Blend; preserve original field assignments and reset events; check timelines, clamps, selectors; use custom named variables unless inherited logic requires generic fields; **replication/authority behavior unconfirmed**.

## Attachments / grenades [V file lists]
Bases to subclass: `CustomSightBase`, `CustomCantedBase`, `CustomGripBase`, `CustomSuppressorBase`, `CustomBayonetBase`, `CustomGrenadeBase`. Examples: reddot, scope with `ZeroingTableExample`, canted, vertical grip, suppressor, Kar98 bayonet, MK2/M24 grenades. Wiki attachment info: removing attachments = hold the weapon horizontally in front of chest; rifle laser can't coexist with flashlight; zero distances: red dot 25 m, holo 35 m, ACOG 75 m, 8x 100 m.

## Editing stock gun stats
Content mod ModInitializer can edit stats of existing guns (video 0eJ1j0JRF2Y). Server can also use a balance table: `BalanceTableURL="vankruptgames/BalancingTable/main"` (https://github.com/vankruptgames/BalancingTable). [V/D]

## Skins
- **Gun skins**: official-ish workflow = Substance Painter (or Quixel Mixer/Blender) using bake maps from the Pavlov Artists Discord; mod.io "skin system" by SmallDvrkOne. Grey checkerboard => enable **"Used with skeletal mesh"** in the material. Guns with two materials (AK12, AK47) need special handling. Do not edit the client; use content mods.
- **Player/character skins**: see [04](04-gamelogic-proxies-modinitializer.md); rig to the UE4 mannequin skeleton (Auto-Rig Pro/Blender), put in `PlayerSkinTable`. Symmetrical models matter for skinning. Default-skin edits break when gore/damage triggers.
- Skin boxes / weapon boxes with variables: Ep.5 (Tti273LnaHc). Retargeting: UE retarget manager to mannequin.
- mod.io "How to get all skin models" guide exists (not read).

## Full video walkthrough (added 2026-11-10)
The complete step-by-step from the 35-minute tutorial is in [guides/video-creating-custom-guns-nxw2cP2fICQ.md](guides/video-creating-custom-guns-nxw2cP2fICQ.md): physics asset, Shack texture groups (**Weapon / Weapon Normal Map**), the 7 exact sockets, AnimBP (`Modify Bone`, Slide Time, Trigger Ratio), duplicating `PavExamples/Guns` (never the bases), magazine/shell/bullet/gun class defaults, attachment slots + the vanilla **compatibility flag table**, sound layers, recoil (incl. the **recoil curve horizontal-recoil bug fix**), fire modes, behavior flags, and registering the gun in the Mod Initializer. Transcript: [transcripts/nxw2cP2fICQ.md](transcripts/nxw2cP2fICQ.md). Evidence is auto-captions only (no frames), so a few class names are marked `[ASR?]` there.

## Complete custom-gun documentation set (added 2026-11-10)
Follow in this order: rigging [guides/video-rigging-custom-guns-J5u3qoJXzD0.md](guides/video-rigging-custom-guns-J5u3qoJXzD0.md) -> [guides/custom-gun-guide-pre-setup.md](guides/custom-gun-guide-pre-setup.md) (physics asset, sockets, AnimBP) -> [guides/custom-gun-guide.md](guides/custom-gun-guide.md) (mag/shell/bullet/gun BPs, item list) -> [guides/video-creating-custom-guns-nxw2cP2fICQ.md](guides/video-creating-custom-guns-nxw2cP2fICQ.md) (full class-defaults walkthrough, attachment flags, recoil fix, Mod Initializer registration) -> [guides/video-custom-gun-lods-and-hand-poses.md](guides/video-custom-gun-lods-and-hand-poses.md). Reference: [guides/pavlov-shack-custom-gun-development-guide.md](guides/pavlov-shack-custom-gun-development-guide.md) (gun states/generic fields), [guides/how-to-create-your-own-better-bolt-action-rifles.md](guides/how-to-create-your-own-better-bolt-action-rifles.md). Untrusted link dump (do not download): [guides/hey-heres-everything-i-know.md](guides/hey-heres-everything-i-know.md).

## Custom items (non-gun) (added 2026-11-10)
Full walkthrough in [guides/video-custom-items-overview-KlxXufos_-M.md](guides/video-custom-items-overview-KlxXufos_-M.md) (older UE4-era video, concepts still match the kit's `ModItem_*` examples): create a child of the Pavlov custom item class inside the UGC, set Pavlov API -> Custom Item defaults (pick offset/rotation, holding animation, inventory offset, self-destroy delay, inventory disable, exclude slots), override `On Use` / `Un Use` / `On Pickup` / `On Drop` / `Can Pick Up Item`, set collision (Grabbable object type, block WorldStatic, overlap WorldDynamic, overlap events on), use the Hand Pose Tester to tune the hand, replicate state with a Run-on-Server event plus a **RepNotify** variable, then register the item (custom item data table in GlobalInfo in the old kit; verify Mod Initializer `Add To List` for the UE5 kit) and spawn it by ID with `Spawn Item`.
