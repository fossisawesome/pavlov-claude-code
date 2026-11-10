# Video guide: "Pavlov VR Mod Kit: Custom Items overview" (Lance S / Vankrupt, older UE4-era kit)

> Source: https://www.youtube.com/watch?v=KlxXufos_-M (17:39). Description is only the repo link https://github.com/vankruptgames/PavlovVR-ModKit; no pinned comment. Evidence: YouTube **auto-captions only** (no frames viewed), read 2026-11-10. Transcript: [../transcripts/KlxXufos_-M.md](../transcripts/KlxXufos_-M.md). Names are as heard; ones marked **[ASR?]** may be mis-transcribed.
> **Version caveat:** recorded for the UE4.21 kit (the wiki lists it under "older"). The *item class and its overridable functions* match the `ModItem_*` / example items still in the Shack kit (`ModItem_Flashlight`, `ModItem_FOB`, `CustomMapTools/Content/Examples/Items/`), so the concepts carry over. **The registration step (custom item data table in GlobalInfo) may have been replaced or supplemented by the Mod Initializer `Add To List` approach in the UE5 kit** (see [video-creating-custom-guns-nxw2cP2fICQ.md](video-creating-custom-guns-nxw2cP2fICQ.md) section 12 and [../05-mods-dependencies-servers.md](../05-mods-dependencies-servers.md)). Verify in the editor, e.g. open `CustomItemTableExample` and `Mod_Initializer_*` examples.

## What a custom item is
"Custom items act as native Pavlov items": they receive input, go in the player's inventory and can be held in the hand.

## 1. Create the item (0:00-2:06)
1. Content Browser: right-click -> **Blueprint Class** -> search **`Pavlov custom item`** (heard "Pavlov custom item"; the parent is the Pavlov custom item class) -> select, name it, open it.
2. It **must live inside your UGC folder** (for Shack the generated folder may be named differently, e.g. the SVR-style folder in the old kit; in the UE5 kit it is `Plugins/UGC<id> Content`).
3. Top toolbar **Class Defaults** -> Details panel -> category **Pavlov API -> Custom Item** exposes the basic variables:
   - **Offsets for the hand** (pick offset / pick rotation offset; see section 3).
   - **Holding animation** (a few predefined grips to choose from; e.g. he picks one named "pilgrim" **[ASR?]**).
   - **Inventory Offset**: where the item sits in the inventory slot, relative.
   - **Never Destroyed For Inactivity**: if ticked the item is never cleaned up when sitting in the world. Otherwise a **self-destroy delay** timer applies; "a very good practice to set one" (destroys the item once inactive for that duration).
   - **Inventory Disable**: item cannot go in the inventory.
   - **Exclude Slots**: inventory slots the item may not be placed in.

## 2. Configure the item (2:06-3:52)
- Add a **Static Mesh** (a **Skeletal Mesh** also works), **drag it over the root to make it the root component**. He uses the flashlight mesh.
- **Event graph** is nearly empty. **Override these functions** (My Blueprint -> Functions -> Override):
  - **`Un Use`** (spoken "unused"): called when the **trigger is released**.
  - **`On Use`**: called when the **trigger is pressed**.
  - **`On Pickup`**, **`On Drop`**.
  - **`Can Pick Up Item`** (and a "can't" variant heard): runs when someone tries to pick the item up; **return true to allow, false to deny**. It receives the **pawn** attempting the pickup.
- **Static mesh collision** (important):
  - **Generate Overlap Events = true**.
  - Collision Presets = **Custom**; **Object Type = Grabbable** (a Pavlov object channel); click **Ignore** in the top box (ignore all), then set **Block** for **WorldStatic** and **Overlap** for **WorldDynamic**.

## 3. Hand pose / offset configuration with the Hand Pose Tester (3:52-6:40)
1. Content: **Plugins -> (CustomMapTools) Examples -> Items -> `HandPoses`** folder contains all vanilla-style hand poses. The same folder has the **`HandPostTester`** tool (heard "hand post tester"; in the repo list: `GM_PoseTester`) **[ASR?]**.
2. Drag the tester into a level. Details: **Holding Animation** (right or left hand), **Pick Offset**, **Pick Rotation Offset**, and an **Item** field where you assign your item's mesh/actor. Click the **root** component of your actor, then **Setup** to preview the hand on your item.
3. Zero the values to see the default; adjust **rotation** until the item faces forward; note that the **pivot** (root) position matters: in the example he moved the pick offset back by **7** units.
4. **Right-click Pick Offset -> Copy**, then in your item's **Class Defaults -> Pick Offset -> Paste**; do the same for **Pick Rotation Offset**; also **select the same grip/holding animation**.
5. To preview the other hand: tick/untick the box, click **Setup Item** again. If the material looks glitched in the preview, re-tick the box to refresh the actor ("we're just changing the variable, not running Setup").

## 4. Example: restrict who can pick up (6:40-7:56) (CTF flag)
Override **Can Pick Up Item**: from the incoming **pawn** -> **Get <player> Status** (the Pavlov player status of that pawn; "Get Bob status") -> compare the player's **Team ID** with the flag's team ID: if **not equal -> true (can pick up)**, otherwise false. **If the status can't be retrieved, return false** (team unknown, so deny).

## 5. Example: replication, a toggle flashlight (7:56-14:37) (`Examples/Items/Flashlight/ModItem_Flashlight`)
Principles: client input only happens on the owning client; state shown to others must be **replicated**.
1. **On Use** (trigger pressed): add a **Do Once** (optional, a half-second cooldown gate) -> **Get Owning Pawn** (confirm someone owns it) -> call a function **`Switch Flashlight`** (his custom event "flashlight changed"/`SwitchFlashlight`).
2. Make `Switch Flashlight` a **Custom Event** with **Replicates = Run on Server** (shows as "Execute on Server" in grey text on the call node). It always runs on the server, so you don't check authority yourself.
3. On the server: Get Owning Pawn again -> **invert the boolean** (`Light On = NOT Light On`) and **Set** it.
4. Variable **`Light On`** (boolean): Details -> **Replication = RepNotify** (None = only the owner sees it; Replicated = sends value but no notification; **RepNotify = notifies everyone when the value changes** and auto-creates function **`OnRep_<VariableName>`**, here `OnRep_LightOn`).
5. In **`OnRep_LightOn`** (runs on every client when the value changes): if `Light On` is true -> **Set Visibility** of the **spotlight component** visible, else **hidden**. The flashlight actor has a **SpotLight component** under the mesh.

## 6. Add the item to the mod: the custom item data table (14:37-17:08) (UE4-era step)
1. Content Browser: right-click -> **Miscellaneous -> Data Table** -> in the row struct dropdown choose **`CustomItemData`** (heard "custom item data") -> OK -> name it (e.g. `CustomItemTable`).
2. Open your **Global Info** (the example is the `CMP_GlobalInfoExample` copy in your UGC) -> **Class Defaults** -> set the **Custom Item Table** property to your data table -> compile & save.
3. Chain: **Game Logic -> Global Info Class -> Global Info -> Custom Item Table -> rows** (this was set up in his first video).
4. In the table, **+ Add Row**: **Row Name = the item ID** (use **unique, easy-to-remember** names; this is the name used to **look up and spawn** the item), **Custom Item Class = your item BP**. Add as many rows as you need. Remove with the X. Save.
   - *UE5 kit:* check `Examples/Items/CustomItemTableExample` (still in the Shack kit) and whether `Add To List` in the Mod Initializer is now the preferred way; the gun video registers guns that way.

## 7. Spawning the item (17:08-17:27)
In your **Game Logic**'s **spawn function** (the one that runs when a player spawns) call **`Spawn Item`** with **ID = the row name** (e.g. `flashlight`). Options: spawn in **dominant hand** or in **inventory**, and **which inventory slot**. (Items spawned by ID also work with RCON `GiveItem`/item spawners per [../09-reference-ids-rcon-gamemodes.md](../09-reference-ids-rcon-gamemodes.md).)

The video ends by pointing to the next video: **Player Proxy and adding skins to the player skin table** (Mark Dey series: Game Logic overview `g6qwk1vJ488`, Global Info overview `XvDfRuYXI10`).

## Open questions to verify in the UE5 / Shack kit
- Exact current parent class name and function signatures (open `ModItem_Flashlight`).
- Whether `Can Pick Up Item`/`On Use` have changed pins.
- Shack-specific: keep meshes/materials within the Shack material rules ([../07-shack-quest-constraints-and-performance.md](../07-shack-quest-constraints-and-performance.md)); a light component adds cost on Quest (**dynamic lights are not supported on Shack**; use an emissive material instead of a spotlight for a flashlight there) [?].
