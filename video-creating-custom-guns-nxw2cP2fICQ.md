# Video guide: "Pavlov VR - Creating Custom Guns" (British Colonist, 2025, PC and Shack)

> Source: https://www.youtube.com/watch?v=nxw2cP2fICQ (35:01). Evidence: YouTube **auto-captions only** (no frames viewed), read 2026-11-10. Spoken names may be mis-transcribed by ASR; names marked **[exact]** were cross-checked against other docs (wiki Custom_Guns, mod.io custom-gun-guide). Anything marked **[ASR?]** is a likely mishearing. Full cleaned transcript: [../transcripts/nxw2cP2fICQ.md](../transcripts/nxw2cP2fICQ.md).
> Prerequisites the author states: watch his earlier videos "content mods / mod initializer" (0eJ1j0JRF2Y) and "rigging custom guns" (J5u3qoJXzD0); read the mod.io custom gun guides; **read the pinned comment** (holds the socket names to copy/paste, compatibility-flag list, hand-sequence guide links, vanilla damage spreadsheet).

## 1. Mesh requirements (00:35)
- Gun mesh = **skeletal mesh with a physics asset**.
- Four **static** meshes: magazine **full**, magazine **empty**, **bullet**, **shell**.
- Organize in a folder inside your UGC (e.g. `Mesh`).

## 2. Physics asset (00:56-01:58)
- Enable Primitives and Bone Tree display (hidden by default), top left.
- Right-click root bone -> Add Shape -> Add Box; delete the default capsule; size boxes to cover the gun length and other parts.
- On every box: **Simulation Generates Hit Events = true** (so the weapon plays sounds when dropped/colliding).

## 3. Shack texture settings (01:58-02:33)
Without these the gun looks glossy or fully white on Shack:
- Color map -> Texture Group = **Weapon**.
- Normal map -> Texture Group = **Weapon Normal Map**. Other maps are fine.

## 4. Skeleton sockets (02:33-06:00) **[exact names, per wiki + mod.io]**
Open the mesh's skeleton, right-click bone -> Add Socket. Names must be spelled exactly; rename via top right or double-click.
- On **root bone** (5): `Magazine`, `MagInsert`, `ShellEjectionSocket`, `Muzzle`, `Suppressor`.
- On **charging handle bone** (2): `Chamber`, `ChargingHandle`.
Placement:
1. `Magazine`: right-click -> Add preview asset -> your magazine mesh; move so the mesh sits in the gun correctly (final inserted position).
2. `MagInsert`: same preview mesh; copy the Magazine socket's location/translation, then move it to where the **insert slide animation starts**.
3. `Muzzle`: tip of barrel, **X axis facing forward**, centered.
4. `Suppressor`: like Muzzle but moved back **into** the barrel a bit; optionally preview a suppressor mesh.
5. `ShellEjectionSocket`: at the ejection port; where the shell BP spawns; **rotation matters: X-facing and angled slightly up**.
6. `Chamber`: line up with the bolt face; **add a preview mesh** to align it.
7. `ChargingHandle`: center of the charging handle.

## 5. Animation Blueprint (06:35-09:38)
1. Right-click gun mesh -> Create -> **Anim Blueprint**, name freely.
2. Class Settings -> Parent Class = **`VRGunAnimInstance`** (verified exact name via mod.io `custom-gun-guide-pre-setup`).
3. In AnimGraph: add **Local Space Ref** (spoken "local space ref"), add **Modify Bone**, connect Local Space Ref's white pin -> the blue pin on Modify Bone input (the **Local to Component** node auto-generates).
4. Modify Bone details: **Bone to Modify** = charging handle bone; **Translation Mode = Replace Existing**; **Translation Space = Bone Space** (do the same for any other Modify Bone node, translation or rotation).
5. Right-click the Translation pin -> **Split Struct Pin**.
6. Variable **Slide Time** (0 to 1; 0 = start, 1 = end; values outside 0-1 are not visible in game). Add a **Multiply** node: Slide Time x N into the axis the gun was rigged on (the example used **Y x 7**; yours differs: X, Y or Z).
7. Compile/save; click the Slide Time node and change its value in Details to preview in the top-left preview window; **set Slide Time back to 0 when done**.
8. Repeat for the **trigger** bone using the **Trigger Ratio** variable (not Slide Time), and a **fire-mode** bone if the mesh has one (the example mesh has none, so no animation). Compile and save.

## 6. Create the Blueprints by duplicating an example (09:38-10:57)
- Content Browser: Plugins -> CustomMapTools Content -> `PavExamples/Guns` -> pick an example similar to your gun (first gun: something simple like an assault rifle, e.g. AK).
- Duplicate **`Gun_AK47_Example`**, **`Magazine_AK47_Example`**, **`Shell_AK47_Example`**, **`Bullet_AK47_Example`** (names inferred from the kit file list; spoken as "gun AK-47 example" etc.). Rename them, then move all four into a folder in your UGC.
- **Pistol**: duplicate a pistol example that uses the **handgun base**.
- **Never duplicate the two gun bases** (`CustomGunBase`, `CustomHandgunBase`). For a fresh gun not based on an example, create a **child blueprint** of the base instead (that is what the examples are).

## 7. Magazine BP (10:57-12:51)
- Components -> Mesh = loaded mesh.
- Class Defaults: **Empty Mesh**, **Normal Mesh** (loaded), **Max Bullets**, **bullet type** the gun uses.
- **Mag Slide** variables (left default in the video); **Allow Mag Slap** (remove the mag by slapping another magazine against it).
- Scroll down: **rotation offset**, **first-person sequence** and **third-person (Avatar) sequence** (reuse another weapon's hand sequence or make your own; not covered).
- After changing the third-person sequence or its offset: right-click the magazine -> Scripted Asset Actions -> **VR Item Update Avatar Anims** (auto-sets **Avatar Hand Offset** and **Avatar Hand Rotation Offset**).

## 8. Shell BP (12:51-13:36)
- Mesh component = your shell mesh; Class Defaults **Mesh Live** = shell mesh.
- Tick **Right Vector Impulse** if the gun ejects to the right (most do); untick if it ejects left.

## 9. Bullet BP (13:36-14:11)
- Simple gun: change nothing. Advanced: customize tracers / impact particles.

## 10. Gun BP: components (14:11-19:17)
- Components -> **Mesh** = gun mesh (sometimes compile/save then close/reopen BP for the mesh to refresh). Details -> **Animation -> Anim Class** = your Anim BP.
- Mesh flickering in/out = bad physics asset: search **Bounds** and increase the scale to ~**10** (only if flickering).
- **ReloadHandle**: move to the charging handle. The kit shows no hand previews by default: with ReloadHandle selected click **+** -> Skeletal Mesh -> a hand mesh from the examples (spoken "skore handore NT" **[ASR?]**), rename "right hand charging", tick **Hidden In Game**, set **Collision = No Collision**; copy/paste for left hand and set its **Y scale = -1**. Under ReloadHandle details -> **VR Handle** -> **Sequence Right Hand**, **Sequence Left Hand**: copy values onto the previews, then tune offsets/sequences on the previews and copy the results back into the dropdowns. Untick **Visible** to hide previews.
- If the gun mesh misaligns with the primary hand: use a custom hand sequence, or edit the mesh translation (best in Blender): open the mesh, search "translation", edit, **Reimport Base Mesh**; if the source file is missing, export from your 3D tool or from Unreal and point to that file.
- **VR Magazine Slot**: move/scale to where the magazine inserts. With Mag Slide the box must sit **slightly inside the gun** or the mag auto-reinserts when removed.
- **TwoHandGrip**: move/scale to where the off hand grabs (fix off-hand mesh later).

## 11. Gun BP: Class Defaults (19:17-33:43)
Search tips used: "mag", "shell", "bullet", "inventory", "attachments", "sound", "recoil", "fire mode", "sequence".
- **Magazine / Shell / Bullet class** = your BPs.
- **Chamber Mesh Live** = bullet mesh; **Chamber Mesh Shell** = shell mesh. **StateClass**: most guns use **VRGunState**; special guns need other states (not covered; see custom gun dev guide).
- **Inventory**: slot dropdown (which holster slots the gun fits); **Inventory Offset** (scale/rotation in inventory); **Custom Inventory Offset** array per-slot (an on-screen image in the video shows slot IDs).
- **Attachments** (5 types): **Pitini** (video's spoken form of the Picatinny rail slot **[ASR?]**; scopes/sights), **Grip**, **Suppressor**, **Accessory** (bayonets, flashlights), **Canted**. One attachment per slot; slots cannot be added (maybe via code). Text field = **socket name on the gun skeleton** (must match). **Compatibility flags 1-32**: only attachments with a matching flag fit, and the attachment type must also match (a bayonet cannot go on a Pitini socket). Vanilla flag list is in the **pinned comment**. **Default Attachments**: attachments spawned on the gun; **vanilla attachments must be "fake referenced"** (not covered); custom attachments can be referenced directly. **Attachment Mode Range** (angle) and **Attachment Mode Hold Time** (seconds) control entering attachment mode.
- **Sound** (search "sound"): three shooting layers: **First Person** (client-side, plays at the barrel tip), **First Person 2D** (client-side, no attenuation/replication, for layering), **Third Person** (server-side, other players hear it); three alternates for **suppressed** shots (leave empty if no suppressor). Some complex examples keep sounds in the event graph. Vanilla sound cues live in the "new audio" folder as **fake references (silent in editor)**. For custom audio duplicate and modify the **M4 example sound cues** to keep correct attenuation.
- **Recoil**: many individual variables; most modders **copy values from a similar example gun** (open M4 example, search "recoil", copy values across). **Known bug in the newest modkit: custom guns have no horizontal recoil** because the **recoil curve** uses the wrong vector. Fix: click the search icon on the recoil curve, find the `M4`-named vector curves, **duplicate** one, name it exactly **`recoil curve`** (spelled like the original; wrong spelling may crash the game), set the gun's Recoil Curve to your duplicate. Ignore if later kits fix it.
- **Recoil Simulator**: place the `RecoilSimulator` actor ("recoil simulator" in Place Actors) in any level; set **Gun Class**, tick **Enable Simulation**, click **Fire Weapon**; **Full Auto** (rounds per click), **Two Hand Gripped** to preview two-hand recoil.
- **Fire Mode**: default fire mode options **Semi-automatic**, **Automatic**, **Manual** (cock after each shot), **Burst** (3 rounds, hardcoded). Below it: which fire modes the gun offers.
- **Hand sequences**: **Sequence** (first-person primary hand), **Avatar Sequence** (third-person primary), **Magnetic Grip Sequence** (first-person off hand), **Avatar Magnetic Grip Sequence** (third-person off hand). Leave off-hand ones blank if unchanged. Run **VR Item Update Avatar Anims** after editing third-person ones. Custom hand poses are in video txxWu3t-ROg.
- **Behavior flags**: **Eject Shell**; **Show Chambered Mesh**; **Bolt Lock Till Ammo** (handle can't unlock unless a mag with bullets is inserted); **Bolt Lock Manual** (hold the handle back a few seconds to lock open); **Chamber On Magazine** (releases bolt when a new mag is inserted); **Open Bolt** (round chambers when pulling the handle, can't push forward manually; advised against for a first gun); **Lock Bolt** (last round locks bolt back); **Auto Unchamber** (unchamber on mag release); **Two Hand Support Only** (off hand doesn't affect rotation; pistol-like handling); **Disable Two Hand Reload** (mag only via release button; typical for pistols); **Support To Mag Release** (drop mag by pressing the mag button).
- **Muzzle Zero Bias**: very important for aligning iron sights/scope with the projectile (separate video). **Grip Offset VAR**: edit off-hand position in Unreal; copy those changes to the grip offset to take effect in game.
- **Bullet Spray**: number of projectiles per shot (<1 = one). Each projectile does the same damage (damage is set in the mod initializer).

## 12. Registering the gun in the Mod Initializer (31:56-33:43)
- Uses the example mod initializer by "dark cat" shown in his content-mod guide. Click the **Add To List** component -> **Add To List** -> **Add Element** under **Guns** -> expand the element.
- **ID**: your choice; author recommends **one word, all lowercase, no special characters** (capitals/underscores caused guns to be missing from the buy wheel). Check it doesn't collide with another modder's item ID; publish IDs on your mod.io page.
- **Gun Class** = your gun BP.
- **Buy menu** dropdown: which buy-menu section (or not purchasable), which teams can buy, **price**, **Buy Menu Image** (icon for buy wheel and kill feed; without it the wheel shows the ID and the kill feed is blank).
- **Loot Mesh**: mesh shown in Push loadout lockers and when spawned by an item spawner.
- **Magazine Count**: full mags of ammo the player gets in limited-ammo modes (e.g. Push).
- **Damage settings**: self-explanatory; common practice is to copy values from a similar vanilla gun (pinned comment links a spreadsheet of all vanilla gun damage values).

## 13. Testing (33:43-34:56)
1. On a server you admin: run the mod and spawn the gun by ID with RCON.
2. Otherwise: a **test map** with your mod as a **dependency**; buy the gun from the buy wheel or spawn it with an item spawner: `CustomMapTools Content -> PavExamples -> BP_TestItemSpawner` (author notes it only worked when the map used a **custom Global Info**).

## Gaps this video does not cover (explicitly deferred by the author)
Custom hand sequences/poses (video txxWu3t-ROg), gun states, fake-referencing vanilla attachments/sounds, custom attachments, custom icons, muzzle zero bias, gun LODs (tyzYy1YMMbk), rigging (J5u3qoJXzD0).

---

## Appendix: pinned comment (verified text, fetched via yt-dlp 2026-11-10)

Author note: the process "will always be up to date, as the Pavlov modkit won't be receiving any major changes that would change the process of making a mod." Links: rigging https://www.youtube.com/watch?v=J5u3qoJXzD0 ; content mods https://www.youtube.com/watch?v=0eJ1j0JRF2Y ; **table of all vanilla gun stats** https://github.com/vankruptgames/BalancingTable/blob/main/BalancingTable.csv ; mod.io guides `custom-gun-guide-pre-setup` (https://mod.io/g/pavlov/r/custom-gun-guide-pre-setup, **not yet read**) and `custom-gun-guide`. Discords: https://discord.gg/pavlov-vr (official).

**Sockets (exact, 7):** `Magazine`, `MagInsert`, `ShellEjectionSocket`, `Muzzle`, `Suppressor`, `Chamber`, `ChargingHandle`

**Vanilla attachment compatibility flags** (a slot accepts an attachment only if flags match **and** the type matches; flags go 1-32):

| Slot | Flag: attachment |
|---|---|
| Sights (Pitini) | 1 Reddot, 2 Holo, 3 ACOG, 4 Scope, 5 Scope Kar98, 6 Scope LeeEnfield, 7 Scope Mosin, 8 Scope Springfield, 9 Pistol Reddot, 10-32 unused |
| Grip | 1 Grip Vertical, 2 Grip Angled, 3-32 unused |
| Suppressor | 1 Rifle Suppressor, 2 Pistol Suppressor, 3-32 unused |
| Accessory | 1 Rifle Laser, 2 Pistol Laser, 3 Rifle Flashlight, 4 M1Garand Bayonet, 5 Mosin Bayonet, 6 Kar98 Bayonet, 7 LeeEnfield Bayonet, 8 Trenchgun Bayonet, 9 Springfield Bayonet, 10-32 unused |
| Canted | 1 Canted Reddot, 2-32 unused |

**Comment-section gotcha (viewer report, unanswered in the fetched comments):** at 11:17 the magazine static mesh from your own import may not appear in the Mesh dropdown (and the narrator's mag is named `Tutorial_Mag` while the dropdown shows `TutorialMagFull`): confirm you imported the full and empty meshes as **static meshes** inside the UGC and refresh/compile; may be version-dependent.
