# Retargeting hand animations from FPP to TPP

> Source: https://mod.io/g/pavlov/r/retargeting-hand-animations-from-fpp-to-tpp
> Author: Szyx_J | Added: 2023-11-07 | Updated: 2023-11-29 | Views: 373 | Comments: 1 | Tags: animation, CustomGun, CustomItem, Gun, Item, rigging
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 5 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Use a Blender (3.6) tool to batch-convert FPP hand animations to TPP characters.

---
Pavlov uses different animations for its items for the FPP hands and the hands of the TPP characters. The TPP animations can be authored manually, but we have created a Blender tool to avoid that. The tool comes with the modkit and is located in the Blender/AnimConverter folder.

The blender file comes with 2 folders, one to put your FPP animations in and the other where the generated TPP animations will be placed. The tool comes with one example animation file in the *1stPersonAnimations* folder.

![image](images/retargeting-hand-animations-from-fpp-to-tpp/e318f94b69.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-11-07051832.png -->

If you don't have the .fbx files for your hand animations, you can always export them from the engine (right-click -> Asset Actions -> Export), and place them into the folder. This way you can be certain that the animation stores the correct skeletal data.

![image](images/retargeting-hand-animations-from-fpp-to-tpp/4fdccd50be.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-11-07220305.png -->

The Blender file itself contains the FPP hand with its skeleton and the TPP avatar with its own skeleton. The TPP skeleton is set in a way that it imitates the FPP hand perfectly when it's manipulated. There is also the Python script visible on the right of the picture.

![image](images/retargeting-hand-animations-from-fpp-to-tpp/928df7312f.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-11-07204234.png -->

 

The script iterates over all the animations in the 1stPersonAnimations folder, applies them to the TPP skeleton, and exports the animations to the 3rdPersonAnimations folder. If the 1st person folder is filled with appropriate animations, all the user has to do is press the **Run Script** button.

![image](images/retargeting-hand-animations-from-fpp-to-tpp/9e078ed34f.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-11-07213216.png -->

After running the script, the *3rdPersonAnimations* folder will be populated with appropriate animations named by adding a "3rdPerson_" prefix at the beginning of each file name.
The resulting animations can be imported into the mod by dragging them into the content browser. In the import settings set the appropriate, 3rd person skeleton.

![image](images/retargeting-hand-animations-from-fpp-to-tpp/101e48feeb.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/beznazwy.png -->

The importer will throw some errors, but they can be ignored. If the animation looks correct it can be applied as an appropriate "Avatar sequence" (see the [Custom Gun Guide](https://mod.io/g/pavlov/r/custom-gun-guide)).


---

## Comments (mod.io API, 1)

- **-nukester-** (2023-12-01): noice
