# Video guide: "Pavlov VR - Rigging custom guns" (British Colonist, 2025, PC and Shack)

> Source: https://www.youtube.com/watch?v=J5u3qoJXzD0 (13:00). Evidence: YouTube **auto-captions only** (no frames viewed), read 2026-11-10; blender key presses are from speech and could be mis-transcribed. Transcript: [../transcripts/J5u3qoJXzD0.md](../transcripts/J5u3qoJXzD0.md). Software: **Blender 3.6** (newer works).
> Pinned comment (verified): "always up to date" (kit won't change the process). Credits **torskeravn's tutorial** https://youtu.be/7Vr1YFqxPmE as the original source of the technique ("slightly different"; worth watching). Mesh used: a low-poly AK from Fab (https://www.fab.com/listings/b52819fb-ae13-4131-94fa-051b117e6e18, **no longer public**). Related guides: custom-gun-guide-pre-setup, custom-gun-guide.

## Goal
One **single rigged mesh** (not many meshes on one skeleton) with a skeleton whose **bone names equal the vertex-group names**, exported as FBX for import into Unreal as the gun's skeletal mesh.

## 1. Reference mesh (0:19-1:24)
1. In the modkit: Plugins -> CustomMapTools Content -> `PavExamples/Guns/M4` -> right-click **`SK_M4v2`** (the video says "skore M4 V2") -> **Export** (e.g. to Downloads).
2. Blender: new project, delete the 3 default objects; **File -> Import -> FBX** the M4 mesh. Delete the mesh in Scene Collection (delete twice, to remove leftover data) and set its **rotation to 0 on all axes**. This leaves a scale/orientation reference.
3. Import your own gun mesh (must match the example's **scale and orientation**), align it to the reference, then hide the reference. Save often.

## 2. Vertex groups (2:11-5:13)
- Concept: give each moving part its own **vertex group** named exactly like the bone that will move it.
- Workflow the author prefers: separate each component that gets a bone (charging handle, trigger, selector/fire-mode if the mesh has one, plus magazines, bullets, shells which are NOT rigged here: hide them, but **center them before exporting**), assign vertex groups per component, then merge back.
  1. Edit Mode, **face select** mode; hover a face and press **L** to select linked; **Mesh -> Separate -> Selection** for each moving part.
  2. Select the main body -> Edit Mode -> Object Data properties -> **Vertex Groups** -> **+** -> rename (e.g. `body`) -> select all (**A**) -> **Assign**. Repeat per component with matching names.
  3. Object Mode: select each component, **main body last**, **Ctrl+J** to join (vertex groups merge too).
- If the magazine has no empty variant: separate the magazine from the bullets, duplicate, remerge the original or fill empty ones with bullet meshes.
- Warping bones later usually means **faces in multiple vertex groups**; each face may be in **only one** group.

## 3. Rigging method 1: build the skeleton from scratch (5:40-8:21)
1. Add -> **Armature**; scale up. Armature data -> Viewport Display -> **In Front**.
2. Position the first bone behind the gun; Edit Mode; Front view (press Y on the axis gizmo for flat view); rotate it sideways (Ctrl for snapping).
3. Select the bone tip, **E** to extrude (Ctrl-snap); right-click the new bone -> **Parent -> Clear** -> **Disconnect Bone**; align it with the **charging handle**. Repeat for the **trigger** (scale down, slight opposite angle).
4. Rename in Scene Collection: main bone = **`body`** (match its vertex group), then the charging handle and trigger bones. **Bone names must be spelled identically to the vertex groups or the rig won't work.**
5. Before parenting: select the mesh -> **Ctrl+A -> All Transforms**; do the same on the armature. Select mesh, then shift-select the armature -> right-click -> **Parent -> With Empty Groups**. Test in **Pose Mode**.

## 4. Rigging method 2: reuse a vanilla example skeleton (8:21-10:20)
Recommended for complex guns (e.g. bolt actions) because you can copy/paste the example's **AnimBP** and "not change many values".
1. Export an example gun mesh from `PavExamples/Guns` that is similar (video used **AK-47**), import to Blender, **scale = 1**; delete its gun mesh, keep the skeleton; Viewport Display -> In Front.
2. Most bones are unused for a simple rig: delete them (better for performance) or ignore them. Position the skeleton under the gun.
3. Edit Mode: align the bone called **`b_gun_slide`** (spoken "bore gun slide") with the charging handle and **`b_gun_trigger`** with the trigger, plus any others used. (Example bone names follow the `b_gun_*` pattern; the physics-asset guide uses root `b_gun_Root`.)
4. **Rename your vertex groups to match those bone names.** Then apply transforms and parent with empty groups as in method 1; test in Pose Mode.

## 5. Utilities (10:20-11:15)
- Center a bone on a point: Edit Mode, select the target geometry, **Shift+S -> Cursor to Selected**; Object Mode then Edit Mode on the skeleton, select the bone, **Shift+S -> Selection to Cursor** (spoken "selected to cursor").
- Warping parts: faces overlapping two vertex groups (see above).

## 6. Export FBX (11:15-12:54)
- Right-click the rigged mesh in Scene Collection -> **Select Hierarchy**; **File -> Export -> FBX**.
- Include: tick **Selected Objects**; untick Empty, Camera, Lamp, Other.
- Transform: **Forward = X Forward, Up = Z Up**. Scale **0.1** "most of the time" otherwise the mesh imports 100x too big (not always needed; check). Geometry: **Smoothing = Faces**. Armature tab: **untick "Add Leaf Bones"**.
- Save these settings as an export **preset** (+ icon at the top of the export dialog).

Next steps: import into Unreal, then [custom-gun-guide-pre-setup.md](custom-gun-guide-pre-setup.md) (physics asset, sockets, AnimBP) and [video-creating-custom-guns-nxw2cP2fICQ.md](video-creating-custom-guns-nxw2cP2fICQ.md). Skeleton name tip from the kit: `SK_M4v2_Skeleton` is the naming reference.
