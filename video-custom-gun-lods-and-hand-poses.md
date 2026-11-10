# Videos: "Custom Gun LODs" and "Custom Hand Poses" (British Colonist, 2025, PC and Shack)

> Sources: LODs https://www.youtube.com/watch?v=tyzYy1YMMbk (0:56); Hand Poses https://www.youtube.com/watch?v=txxWu3t-ROg (4:00). Evidence: YouTube **auto-captions only** (no frames viewed), read 2026-11-10. Transcripts: [../transcripts/tyzYy1YMMbk.md](../transcripts/tyzYy1YMMbk.md), [../transcripts/txxWu3t-ROg.md](../transcripts/txxWu3t-ROg.md). Both have the pinned comment: "This tutorial will always be up to date, as the Pavlov modkit won't be receiving any major changes that would change the process of making a mod."

---

## A. Custom gun LODs (tyzYy1YMMbk)
Giving the gun LODs is "incredibly important for optimization" (Quest!).

1. **Download the LOD settings file** linked in the video's pinned comment: a Google Drive file (`https://drive.google.com/file/d/1TVSn4D9gOWF2GqXjYJx1-c7CX5u71zLG/view?usp=sharing`) **[NOT downloaded by us; third-party file; get it only with user approval and inspect it]**. Drag/drop it into the project's **`Content/Weapons`** folder using Windows File Explorer (it is a `.uasset`, so it must be placed on disk, not via the editor import).
2. Open your **gun skeletal mesh** in Unreal; scroll to the **LOD** section.
3. **LOD Settings = the file you downloaded** (spoken as "weapon LS", probably a `LODSettings` asset such as a weapon LOD-settings asset **[ASR?]**).
4. Set **Number of LODs = 4**, then click **Generate**.
5. Use the preview dropdown at the top center of the viewport to cycle LODs and check them.

Open question: whether the file works unchanged on Shack and what the vanilla `Content/Weapons` LOD settings asset is called. Inspect the Pavlov-Shack kit's `Content/Weapons` folder (the repo tree lists `Weapons` and `Weapons_WII`).

---

## B. Custom hand poses (txxWu3t-ROg)
Hand poses = **animation sequences** used by guns, magazines, and items (`Sequence`, `Avatar Sequence`, `Magnetic Grip Sequence`, `Avatar Magnetic Grip Sequence`; see [video-creating-custom-guns-nxw2cP2fICQ.md](video-creating-custom-guns-nxw2cP2fICQ.md)). The kit also has hand pose example meshes in `CustomMapTools/Examples/Items/HandPoses/` (e.g. `SM_PistolGrip`, `SM_RifleGrip`, `SM_VerticalGrip`, `SM_MagazineGrip`, `GM_PoseTester`).

### First-person hand sequence (0:03-2:01)
1. Open the hand mesh's **skeleton**: `Content/Hands/Mesh/` (spoken "content hands mesh skore handore skeleton" = `SK_Hand_*`-style names **[ASR?]**).
2. In the skeleton tree, right-click the **top bone `hand`** -> **Preview Mesh** -> choose the mesh you are making the pose for (the item).
3. Pose the hand freely, **or start from a vanilla pose**: **Preview Animation** (top left) -> choose from the array of hand sequences; adjust the pose; **pause the animation** (bottom of the screen). You can swap which vanilla hand mesh is previewed (beside Preview Animation).
4. When happy: **Create Asset -> Create Animation -> Current Pose**; choose a save path; **make sure the name doesn't collide with another sequence in that folder** (it will overwrite).
5. To clear the preview: right-click the hand -> **Remove All Attached Assets**.
6. **Limitation: it is currently impossible to have a different hand sequence depending on which hand holds the gun**, so make a pose that **mirrors perfectly** left/right.

### Third-person hand sequence (2:01-3:47)
Third-person animations (for the player model) must be created **separately** from first-person ones. The developers ship a **Blender script** that automates it:
1. Right-click and **Export** your custom first-person hand sequence (FBX).
2. In Windows File Explorer open the Pavlov project folder -> **`Blender`** -> **`AnimConverter`** (this folder exists in the Pavlov-Shack repo) -> drag the exported file into **`FirstPersonAnimations`**.
3. Open the **Blender project** from the AnimConverter folder -> click **Run Script** (top right).
4. In Explorer open **`ThirdPersonAnimations`**: the new file there is the third-person animation.
5. **Import** it into Unreal; for **Skeleton** choose the **UE4 mannequin skeleton** located at `Content/MovementAnimsetPro/UE4_Mannequin/...` (spoken "content movement anom set pro ue4 mannequin mesh"; the repo has a `MovementAnimsetPro` content folder). Expect "the exact same few errors" shown in the video; they can be ignored. Different errors mean something went wrong.
6. Use the resulting asset as the **Avatar (third-person) sequence**, then run **VR Item Update Avatar Anims** (Scripted Asset Actions) on the item so offsets update.
