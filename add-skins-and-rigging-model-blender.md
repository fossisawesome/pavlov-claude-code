# Add skin and rigging model (Blender)

> Source: https://mod.io/g/pavlov/r/add-skins-and-rigging-model-blender
> Author: shadowmanxr | Added: 2023-09-20 | Updated: 2023-10-30 | Views: 994 | Comments: 3 | Tags: blender, mod, rigging, skin
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 9 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Add skins and rigging model (Blender) UE5.1.1 ModKit 2.0 Blender 3.6.0

---
Work PC and Shack version

UE 5.1.1

ModKit 2.0

Blender 3.6.0

#### Instructions:

1. First you should find in the modkit, a standard player model called SK_Mannequin ( Folder All/Content ) and export the model as fbx format.

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20212417.png)

2. Open blender and import this model as fbx format.

3. Remove the standard model while leaving the skeleton

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20212849.1.png)

4. Import your model into Blender. Most of all, your skeleton will not match your model. Then move on to the next point

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20213321.png)

5. Adapt the skeleton to your model by moving the bones in the skeleton editing mode.

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20213557.png)

6. First select the model, then the skeleton, press the shift key, then press the hotkey ctrl+P and select "With Automatic Weights". 

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20214149.png)

7. Most of all, the autoriging will not be perfect, you will have to fix it. Watch on YouTube how to rig models in a blender.

8. Select hierarchy

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20214659.png)

9. Export the model as a fbx model by selecting what you selected.

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-20214942.png)

Also select these items

![image](https://image.modcdn.io/members/af45/26066947/profileaddskins/screenshot2023-09-29153950.png)

10. Open the unreal editor and import the model without the skeleton.

11. Open the skeleton of the imported model for editing. And repurpose the skeleton to the skeleton of this model and add compatibility with the standard skeleton.

![image](https://image.modcdn.io/members/af45/26066947/profile/screenshot2023-09-20215734.png)

12. Everything is ready. Also don't forget to add the skin to the skins table.


---

## Comments (mod.io API, 3)

- **MASMD88** (2024-02-27): Thank you for the guide! just one question, how do you make it work from player proxy BP?
- **LacksomWasTaken** (2024-02-25): it works!
- **BritishColonist** (2023-09-21): in the next update for the modkit, the mannequin will be moving to Content > UE4_Mannequin > Mesh
