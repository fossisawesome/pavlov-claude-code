# Custom gun guide

> Source: https://mod.io/g/pavlov/r/custom-gun-guide
> Author: Brav_Soldat | Views: 2,941 | Comments: 11 | Last updated: 3y 7mo before 2026-11-10 | Tags: CustomGun, Gun | Triage tier: A
> Saved as plain text (restored 2026-11-10 with the complete text; an earlier save of this file was accidentally replaced with a condensed version and then rewritten from a fresh scrape). **Screenshots/images are not included.** Prerequisite: [custom-gun-guide-pre-setup.md](custom-gun-guide-pre-setup.md). Video companion: [video-creating-custom-guns-nxw2cP2fICQ.md](video-creating-custom-guns-nxw2cP2fICQ.md).

---

Custom gun guide

Before creating a custom gun, some blueprints need to be created. This guide should help with both processes.

You also need to make sure you followed the previous guide: Custom gun guide (Pre-setup)

If you ever get stuck, look at the included gun examples to get a general idea on how something should be. Every gun is unique. (CustomMapTools/PavExamples/Guns)

## Creating the magazine

Navigate to "CustomMapTools/PavExamples/Guns" and right click on CustomMagazineBase, then create a child blueprint at the top.

Give your magazine a name and open it.

Over on the left, under the components list, click on "Mesh" then over on the right under the details panel, set the static mesh to your magazines loaded mesh.

Now click "Class Defaults" at the top middle of the window.

Over on the right, under the details panel, set the Normal and Empty mesh variables.

Set MaxBullets to the amount the magazine should have.

If using MagSlide, change any variables needed (hover over the variable names to get an explanation).

If using MagSlap, change any variables needed (hover over the variable names to get an explanation).

Scroll down and set any rotation offset (0, -75, 0 is a good start) as well as the sequence and 3rd person sequence.

You can either use an existing hand sequence another weapon uses, or make your own following this guide: Custom hand sequence guide

You must have a Sequence and Avatar Sequence set for this last step. Compile and save the magazine blueprint, then navigate to it in the content browser. Right click then Scripted Asset Actions then VRItem Update Avatar Anims.

This automatically sets the AvatarHandOffset and AvatarHandRotationOffset variables in the magazine.

## Creating the shell

Navigate to "CustomMapTools/PavExamples/Guns" and right click on CustomShellBase, then create a child blueprint at the top.

Give your shell a name and open it.

Over on the left, under the components list, click on "Mesh" then over on the right under the details panel, set the static mesh to your empty shell mesh.

Now click "Class Defaults" at the top middle of the window.

Over on the right, under the details panel, set the MeshLive variable.

Most guns eject to the right so tick RightVectorImpulse.

Change the SurfaceFX if the shell is bigger or smaller.

## Creating the bullet

Navigate to "CustomMapTools/PavExamples/Guns" and right click on CustomBulletBase, then create a child blueprint at the top.

Give your bullet a name and open it.

Now click "Class Defaults" at the top middle of the window.

Over on the right, under the details panel, set your variables. We really only care for InitialSpeed/Gravity/SurfaceFX for now.

Ignore the "Hidden" and "Testing" category variables for now, we'll learn how to use those with the bullet tester blueprint at a later point.

## Creating the gun

Navigate to "CustomMapTools/PavExamples/Guns" and right click on CustomGunBase, then create a child blueprint at the top. (Use the CustomHandgunBase if you're making a pistol)

Give your bullet a name and open it. [sic: the original text says "bullet"; it means the gun]

Over on the left, under the components list, click on "Mesh" then over on the right under the details panel, set the skeletal mesh to your gun mesh.

Next, click on the ReloadHandle and move it to where the charging handle is.

You can also click on the MuzzleParticle and change the scale of it. (0.9 is default)

Next, click on the VRMagazineSlot and move/ scale it to where the magazine goes in.

If you're using MagSlide, the VRMagazineSlot box needs to be up into the gun some like above.

Also the MagSlide variables.

Lastly, click on TwoHandGrip and move/ scale it where your offhand would grab.

You can hide the Offhand mesh to make things easier.

## Setting the essentials

Click "Class Defaults" at the top middle of the window.

Over on the right, under the details panel, search for "magazine". Set the MagazineClass to the magazine blueprint we made earlier.

Over on the right, under the details panel, search for "shell". Set the ShellClass to the shell blueprint we made earlier.

Over on the right, under the details panel, search for "bullet". Set the BulletClass to the bullet blueprint we made earlier.

Another variable that's important is StateClass, so search for it. Most guns use "VRGunState" but more special ones use others, look at the included gun examples. (CustomMapTools/PavExamples/Guns)

The rest of the ClassDefaults are up to you. Once again, look at the gun examples to get an idea on recoil/ other variables.

## Applying the animBP

Over on the left, under the components list, click on "Mesh" then over on the right under the details panel, set the AnimClass to your gun's animBP.

## Adding to the item list

Open your custom GlobalInfo, add the OnGlobalInfoInitialized event.

Right click and search for "Add Gun to List" and add the node.

Connect the nodes and set your variables, the most important items are the GunName and GunClass.

You can also add items with an array/ for loop. (Example of this at: CustomMapTools/PavExamples/CMP_GlobalInfoItemExample)

---

## Notes for this project (not part of the original guide)
- This older guide registers guns via **GlobalInfo -> `OnGlobalInfoInitialized` -> `Add Gun to List`** (inputs: **GunName**, **GunClass**). The 2025 video instead registers them in a **Mod Initializer** (`Add To List` component, Guns array element with ID, Gun Class, buy menu, damage...). Both exist; the Mod Initializer route is what content mods use (see [../05-mods-dependencies-servers.md](../05-mods-dependencies-servers.md)).
- Earlier docs said this page's text was truncated; it was not. The extra sections (**Applying the animBP**, **Adding to the item list**) are above.

---

## Images (mod.io API; local copies downloaded 2026-11-10, remote URL kept in comment)

1. ![image](images/custom-gun-guide/59e3f36410.png) <!-- src: https://i.imgur.com/iVXuvKA.png -->
2. ![image](images/custom-gun-guide/6ff0c34ad3.png) <!-- src: https://i.imgur.com/JVVM4Qz.png -->
3. ![image](images/custom-gun-guide/5c28dc320a.png) <!-- src: https://i.imgur.com/BP71G6N.png -->
4. ![image](images/custom-gun-guide/6e5ed8006b.png) <!-- src: https://i.imgur.com/F3NumJL.png -->
5. ![image](images/custom-gun-guide/d02da5a4c3.png) <!-- src: https://i.imgur.com/lrfZ0cm.png -->
6. ![image](images/custom-gun-guide/4c547d620c.png) <!-- src: https://i.imgur.com/M2t90R8.png -->
7. ![image](images/custom-gun-guide/79b732c2f5.png) <!-- src: https://i.imgur.com/RLmlmcf.png -->
8. ![image](images/custom-gun-guide/4689fe8115.png) <!-- src: https://i.imgur.com/43yoVP0.png -->
9. ![image](images/custom-gun-guide/c2b4d9e8f2.png) <!-- src: https://i.imgur.com/wwSHfDI.png -->
10. ![image](images/custom-gun-guide/cc49e1f4e3.png) <!-- src: https://i.imgur.com/mL7Yri0.png -->
11. ![image](images/custom-gun-guide/5c28dc320a.png) <!-- src: https://i.imgur.com/BP71G6N.png -->
12. ![image](images/custom-gun-guide/c71ac7041a.png) <!-- src: https://i.imgur.com/ItAie8J.png -->
13. ![image](images/custom-gun-guide/377d91c673.png) <!-- src: https://i.imgur.com/WlTA5Tc.png -->
14. ![image](images/custom-gun-guide/5c28dc320a.png) <!-- src: https://i.imgur.com/BP71G6N.png -->
15. ![image](images/custom-gun-guide/7645d8a623.png) <!-- src: https://i.imgur.com/AWuqlk6.png -->
16. ![image](images/custom-gun-guide/bb6b28370d.png) <!-- src: https://i.imgur.com/IlSUZ5O.png -->
17. ![image](images/custom-gun-guide/ca74793580.png) <!-- src: https://i.imgur.com/MvSeplh.png -->
18. ![image](images/custom-gun-guide/dea1faa87a.png) <!-- src: https://i.imgur.com/XXjT5WM.png -->
19. ![image](images/custom-gun-guide/f69b8d0fca.png) <!-- src: https://i.imgur.com/Jjt6w2I.png -->
20. ![image](images/custom-gun-guide/6b032e8499.png) <!-- src: https://i.imgur.com/l4tCEfc.png -->
21. ![image](images/custom-gun-guide/9261e50d93.png) <!-- src: https://i.imgur.com/iTX3Yxi.png -->
22. ![image](images/custom-gun-guide/5c28dc320a.png) <!-- src: https://i.imgur.com/BP71G6N.png -->
23. ![image](images/custom-gun-guide/368e129890.png) <!-- src: https://i.imgur.com/nokdfvD.png -->
24. ![image](images/custom-gun-guide/e5278cfd67.png) <!-- src: https://i.imgur.com/TDq6eQv.png -->
25. ![image](images/custom-gun-guide/993868f915.png) <!-- src: https://i.imgur.com/oXVC90T.png -->
26. ![image](images/custom-gun-guide/68d54af735.png) <!-- src: https://i.imgur.com/UpxF4VS.png -->
27. ![image](images/custom-gun-guide/a1ecd4c27c.png) <!-- src: https://i.imgur.com/NQQkyg5.png -->
28. ![image](images/custom-gun-guide/d2041215a6.png) <!-- src: https://i.imgur.com/drmo2hC.png -->
29. ![image](images/custom-gun-guide/63c6eb0cf2.png) <!-- src: https://i.imgur.com/4iFFdrR.png -->
30. ![image](images/custom-gun-guide/70eefb0ede.png) <!-- src: https://i.imgur.com/lKSFb1S.png -->


---

## Comments (mod.io API, 11)

- **GOOSEboy2** (2024-08-23): i can
- **CHICK-FiI-A** (2024-08-22): Just to ask you know how to make custom item or make one for it please
- **systemdownshot** (2024-05-15): hello, it was not that, it was some logic for a whitelist system i made, could you add me on discord to make the logic not break the mag? my user is lordvader8313
- **Brav_Soldat** (2024-05-13): that was a bug with shack, but was fixed. check the collision settings for the vrmagslot
- **systemdownshot** (2024-05-13): question, when i pick the gun up, the mag "breaks" and i cannot get another mag into the gun and the gun breaks any idea how to fix this?
- **Brav_Soldat** (2024-05-13): should be up to date
- **h0llyw00d24_** (2024-05-06): is this guide outdated or does it still work
- **Haircutman** (2024-05-12): my off hand dosnt want to  go on the grip and my hand is like wierd
- **gakaga** (2024-05-05): allright, thanks! great tutorial btw
- **Brav_Soldat** (2024-05-04): Add it to the gun list in the mod initializer instead, theres an example included in the modkit.
- **gakaga** (2024-05-04): How would I upload it to a mod of its own, instead of using a global info in a map?
