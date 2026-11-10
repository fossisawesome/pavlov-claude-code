# Custom gun guide (Pre-setup)

> Source: https://mod.io/g/pavlov/r/custom-gun-guide-pre-setup
> Author: Brav_Soldat | Views: 1,879 | Last updated: 3y 7mo before 2026-11-10 (UE5-era kit; the 2025 videos say the process has not changed) | Tags: CustomGun, Gun | Triage tier: A
> Saved 2026-11-10 as plain text. **Screenshots/images are not included.** This is the written twin of the first half of [video-creating-custom-guns-nxw2cP2fICQ.md](video-creating-custom-guns-nxw2cP2fICQ.md); follow with [custom-gun-guide.md](custom-gun-guide.md).

---

Before creating a custom gun, some things need to be imported/set up. This guide should help with that process.

You also need to make sure your assets are **X-facing**, this will make your life a lot easier.

If you ever get stuck, look at the included gun examples to get a general idea on where something should be. Every gun is unique. (`CustomMapTools/PavExamples/Guns`)

## Importing the assets
There are 5 main assets needed to create a custom gun: gun mesh, magazine mesh (full and empty), shell casing (full and empty). (Note: elsewhere described as gun, mag full, mag empty, bullet, shell = 4 static meshes + 1 skeletal.)

Import them like any other assets. The gun mesh is a **skeletal mesh** while the rest are normal **static meshes**.

The bone names for the gun mesh can be anything, but it's good practice to follow the format used by the included example guns (`CustomMapTools/PavExamples/Guns/M4/SK_M4v2_Skeleton.uasset`).

## Editing the physics asset
Open the physics asset. By default UE5 has the primitives and bone tree hidden, so enable those in the top left: **"Show Primitives"** and **"Show all Bones"**.

Add primitives: right-click the root bone -> **Add Shape** -> **Add Box**. Add multiple and move/scale them to line up with the weapon.

Click any added shape and make sure **"Simulation Generates Hit Events"** is true for the primitives (Details panel). This makes the weapon play sounds when dropped and colliding with geometry.

## Editing the skeleton asset
Open the skeleton asset for your gun mesh, or click the skeleton icon in the top right of the physics asset.

Right-click the **root bone** and add sockets: `Magazine`, `MagInsert`, `ShellEjectionSocket`, `Muzzle`, `Suppressor`.

Right-click the **charging handle bone** and add: `Chamber`, `ChargingHandle`.

- Add a preview asset to the `Magazine` socket (right-click -> Add preview asset -> magazine mesh); move the socket so the preview mesh is in the right place.
- Do the same for `MagInsert`; move it to **where the insert animation should start**.
- `Muzzle`/`Suppressor`: move them to the end of the gun. `Muzzle` sits at the end of the barrel; `Suppressor` needs to be a little bit **in** the barrel (add a preview asset to place it). **The rotation of the Muzzle socket matters: it needs to be X-facing.**
- `ShellEjectionSocket`: move to the ejection port area (where the shell blueprint will spawn later). **Rotation matters: X-facing and angled slightly up.**
- `Chamber`: line up with the bolt face. Adding a preview asset really helps: the casing should rest on the end of the bolt face.
- `ChargingHandle`: middle of the charging handle.

Look at the included gun examples for general socket placement. Every gun is different.

### Other sockets
There are other sockets to add for additional attachments, covered in the attachment guide (linked from the original page; not captured).

## Creating the animBP
1. Right-click the gun's skeletal mesh -> **Create** (top) -> **Anim Blueprint**. Name it and open it.
2. Click **Class Settings** (top middle). In Details set **ParentClass = `VRGunAnimInstance`** (exact name, verified here).
3. Open the **AnimGraph** tab (if hidden, double-click "AnimGraph" on the left).
4. Right-click -> search **"local space ref"** -> add the node. Right-click again -> search **"modify bone"** -> add it.
5. Connect the **white T-pose icon** on the local space ref node to the **blue T-pose icon** on the modify bone node. The **LocalToComponent** node auto-generates/connects.
6. Click the **ModifyBone** node: set **BoneToModify** = the charging handle bone; **TranslationMode = "Replace Existing"**; **TranslationSpace = "Bone Space"** (do this for any other ModifyBone nodes, translation or rotation).
7. Right-click the **Translation** pin on the ModifyBone node -> **Split Struct Pin**.
8. Right-click in the open graph -> search **"slide time"**. **SlideTime goes 0.0 to 1.0**, so multiply it to move the bolt/charging handle. Depending on the rig, X, Y or Z could be used. In this guide's example Z was the correct direction and **-14.0** worked (the video's gun used Y x 7; **yours will differ**).
9. Compile and save; click the SlideTime node and change its value in Details to preview in the mesh preview (top left) and tune the multiplier. **Set SlideTime back to 0.0 when done.**
10. Repeat for the **trigger bone** and the **firemode bone** (test values by changing the variables' default values and watching the preview).
11. Once all ModifyBone nodes are set up, drag from the **blue T-pose** to the **white T-pose** on the **Result** node (a **Component to Local** node auto-generates). Compile and save the animBP.

You are now ready to follow the Custom Gun Guide ([custom-gun-guide.md](custom-gun-guide.md)).

---

## Images (mod.io API; local copies downloaded 2026-11-10, remote URL kept in comment)

1. ![image](images/custom-gun-guide-pre-setup/aefa4a96da.png) <!-- src: https://i.imgur.com/f91IoJa.png -->
2. ![image](images/custom-gun-guide-pre-setup/9d831a644f.png) <!-- src: https://i.imgur.com/oay1cdn.png -->
3. ![image](images/custom-gun-guide-pre-setup/81000cbb9a.png) <!-- src: https://i.imgur.com/qlD3ukM.png -->
4. ![image](images/custom-gun-guide-pre-setup/facbcdaa6f.png) <!-- src: https://i.imgur.com/SHrbk0d.png -->
5. ![image](images/custom-gun-guide-pre-setup/2bfe4f93d7.png) <!-- src: https://i.imgur.com/xUBovdF.png -->
6. ![image](images/custom-gun-guide-pre-setup/7a691e55ef.png) <!-- src: https://i.imgur.com/O5ULK2k.png -->
7. ![image](images/custom-gun-guide-pre-setup/bc32ab0094.png) <!-- src: https://i.imgur.com/lodt20c.png -->
8. ![image](images/custom-gun-guide-pre-setup/705c94ca9a.png) <!-- src: https://i.imgur.com/QcfSw5Q.png -->
9. ![image](images/custom-gun-guide-pre-setup/e0123478b6.png) <!-- src: https://i.imgur.com/9jVCBDv.png -->
10. ![image](images/custom-gun-guide-pre-setup/3035d9b8f4.png) <!-- src: https://i.imgur.com/RPiE96m.png -->
11. ![image](images/custom-gun-guide-pre-setup/f214925a39.png) <!-- src: https://i.imgur.com/BYIL4AY.png -->
12. ![image](images/custom-gun-guide-pre-setup/4ed127390d.png) <!-- src: https://i.imgur.com/GlPEyr7.png -->
13. ![image](images/custom-gun-guide-pre-setup/be834f7a44.png) <!-- src: https://i.imgur.com/EqSHbO9.png -->
14. ![image](images/custom-gun-guide-pre-setup/f95c072f2d.png) <!-- src: https://i.imgur.com/3UlTdjG.png -->
15. ![image](images/custom-gun-guide-pre-setup/b62d7b50dd.png) <!-- src: https://i.imgur.com/3vd4NUR.png -->
16. ![image](images/custom-gun-guide-pre-setup/fe01dcf95d.png) <!-- src: https://i.imgur.com/3WQNyGf.png -->
17. ![image](images/custom-gun-guide-pre-setup/900cf12018.png) <!-- src: https://i.imgur.com/zBQuvDl.png -->
18. ![image](images/custom-gun-guide-pre-setup/235daead8f.png) <!-- src: https://i.imgur.com/qmIvPIw.png -->
19. ![image](images/custom-gun-guide-pre-setup/416a8034fb.png) <!-- src: https://i.imgur.com/lgNDRJ6.png -->
20. ![image](images/custom-gun-guide-pre-setup/ebc11368b1.png) <!-- src: https://i.imgur.com/6McQPtm.png -->
21. ![image](images/custom-gun-guide-pre-setup/a178977dc3.png) <!-- src: https://i.imgur.com/3QDfbv9.png -->
22. ![image](images/custom-gun-guide-pre-setup/02e94310da.png) <!-- src: https://i.imgur.com/zcNTNR4.png -->
23. ![image](images/custom-gun-guide-pre-setup/708b7a0bca.png) <!-- src: https://i.imgur.com/y6mqO0D.png -->
24. ![image](images/custom-gun-guide-pre-setup/fd51977d3b.png) <!-- src: https://i.imgur.com/VCNvaGo.png -->
25. ![image](images/custom-gun-guide-pre-setup/0d9573e6a7.png) <!-- src: https://i.imgur.com/SDqOYoA.png -->
26. ![image](images/custom-gun-guide-pre-setup/0fec6840da.png) <!-- src: https://i.imgur.com/qNXey7v.png -->
27. ![image](images/custom-gun-guide-pre-setup/a2128e2c86.png) <!-- src: https://i.imgur.com/BwFhT1C.png -->
28. ![image](images/custom-gun-guide-pre-setup/4c61044fe5.png) <!-- src: https://i.imgur.com/RfG1CBX.png -->
29. ![image](images/custom-gun-guide-pre-setup/8e972f74f9.png) <!-- src: https://i.imgur.com/JGlgTe7.png -->
30. ![image](images/custom-gun-guide-pre-setup/dc085d7cc2.png) <!-- src: https://i.imgur.com/xX0dYhi.png -->
31. ![image](images/custom-gun-guide-pre-setup/3edc899601.png) <!-- src: https://i.imgur.com/d9DlO32.png -->
32. ![image](images/custom-gun-guide-pre-setup/5a624c3591.png) <!-- src: https://i.imgur.com/YdWhxYD.png -->
33. ![image](images/custom-gun-guide-pre-setup/37834a2906.png) <!-- src: https://i.imgur.com/c8hxvse.png -->
