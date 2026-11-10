# Rigging a custom skin using the Vankrupt Mannequin

> Source: https://mod.io/g/pavlov/r/rigging-a-custom-skin-using-the-vankrupt-mannequin
> Author: Szyx_J | Added: 2024-05-13 | Updated: 2024-08-21 | Views: 1355 | Comments: 1 | Tags: Blender, Custom Skin, Rigging, Skinning
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 46 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This guide will help you rig a custom player skin for Pavlov using the Vankrupt Mannequin.

---
To make creating custom skins easier, we provide a mod that contains the SK_Vankrupt_Mannequin.fbx file. The mod can be found here: https://mod.io/g/pavlov/m/vankrupt-mannequin-for-custom-skins . This file contains the Pavlov skeleton with a lot of unnecessary bones removed, it will streamline the rigging process for less advanced users. 

**1. Get the file.**

You get the file by downloading the Source of the aforementioned mod:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/311ccaede8.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-14012528.png -->

The file in question needs to be unpacked from the archive, it's in the Content folder:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/90f9411c49.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-14012728.png -->

I use Blender, and the tutorial's been written with it in mind. with that stated, import the file using these settings:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/18e1baeb60.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-27014314.png -->

This is how it should look like:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/81a9e7f686.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15190727.png -->

The bone hierarchy in this skeleton is a simplified version of the official UE4 mannequin, it only includes the skinned bones:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/33bc61786a.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15190946.png -->

Feel free to preview the bone weights by jumping into the **Weight Paint **mode and selecting appropriate **Vertex Groups **from the **Data** panel. You can also select the skeleton and the model (make sure the model is selected second, therefore is the active model) and jump into the **Weight Paint** mode, this way you'll be able to cycle through the **Vertex Groups** by selecting the corresponding bones.

Most of the provided model's weights follow the Epic's skinning:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/fd808a39af.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193134.png -->

This version comes with a facial rig that works with in-game eye tracking and voice-activated mouth movements. The bones and skinning are pretty self-explanatory:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/7ff583daf8.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193204.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/376d0f11c4.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193218.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/dd55c73ace.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193320.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/839062cef2.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193337.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/df2bf8d8e7.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193358.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/5419793766.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-15193424.png -->

 

**2. Get your Custom Skin into the scene.**

You can import the custom skin model, append it from a Blender file, or even model it in this project, doesn't matter. The important part is to have the custom skin mesh in the same scene as the imported skeleton. For this guide, we'll be working with this here Jigglybuff:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/1cc2d8a638.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23035222.png -->

The important thing about Pavlov's custom skins is that we can't alter players' proportions too much, they need to follow the base-game models pretty closely to make the game's physics and rules work. As provided, Jigglybuff doesn't match the mannequin too well and needs to be altered:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/b8f64b0afa.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23035620.png -->

Jigglybuff came with a skeleton of its own, which helped a lot with aligning it to the mannequin proportions. After posing it closely to the target I applied the **Armature** modifier and made the rest of my adjustments in **Edit mode. **If your skin doesn't have a skeleton you might consider creating a temporary rig for this purpose alone, but you'll most likely be fine staying in **Edit Mode** and making liberal use of the **Proportional Editing **option. Feel free to move, scale and rotate verticles as needed. You can set the 3D cursor as the transformation orientation and set its location to match a joint to emulate the functionality of a skeleton. Here's the JigglyBuff matched to the mannequin's proportions and pose:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/8d568dca77.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23042545.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/aff579f805.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23043311.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/46e59aad38.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23042602.png -->

Relatively plenty of work needs to be put in to make sure all the hands' joints fit closely enough, this will ensure all weapon-interaction animations look good:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/86cbe22e5a.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23042618.png -->

The facial bones are a bit of an exemption, you can edit their positions and proportions to match the skin's. Jigglybuff has massive eyes and a tiny mouth, I've adjusted the skeleton's bones accordingly. All facial bones animate by rotating.

A good rule of thumb is to put the eye bone origins exactly in the centre of the eyeballs and aim them forward. The eyelids should be set slightly behind the eyes in a way that would make them close by rotating the top lid around its X-axis by around 18 degrees. The eyebrow bones can be shifted to match the model's eyebrows roughly, they move the brow by rotating around its X-axis as well.  You can do it in the skeleton's **Edit Mode:**

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/c22333ce31.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23154109.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/3cba21e7f0.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23160430.png -->

If you're making a more realistic character, feel free to stick with the provided locations, or export the Nato skin from the modkit and see how they correlate with the facial proportions and how they're skinned. You can also forego the facial animations and skin all the facial verts to the head bone.

 

**3. Skin your character.**

The nice thing about the Jigglybuff's and the mannequin's proportions matching is that we can get a headstart on the skinning process by *transferring the bone weights* from the mannequin to the custom skin. To start, we need to make sure that the custom skin's armature modifier is applied, and that all the **Vertex Groups** from the old skeleton are deleted:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/d1eb35e1a8.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23043436.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/d3a453dd34.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23043357.png -->

If your custom skin didn't come rigged this step is not necessary.

To transfer the **Vertex Groups** we'll use the **DataTransfer** modifier with these settings:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/f5c0880925.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23043913.png -->

The most important part is to make sure we apply the modifier to the custom skin mesh (Jigglybuff in this case) and the **Source** mesh is the mannequin mesh. After we press the **Generate Data Layers** button and apply the modifier, our custom skin should have all these **Vertex Groups ** added to it:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/3581039ad2.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23043956.png -->

After that we can finally parent the Jigglybuff mesh to the skeleton by selecting it first, the skeleton second and using the **Set Parent To** functionality (ctrl + P). Choose the Armature Deform option:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/038a4e2719.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23044023.png -->

Congratulations! You just did the bare minimum. If you're happy with the results you can skip to the exporting part of the guide. We are going to massage the weights a bit, as our Jigglybuff has some skinning issues:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/b6d126ef7b.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23044135.png -->

Feel free to look for a skinning tutorial for Blender to perfect your custom character, this guide will not go into details of the process but will show how I tweaked the skinning on this particular model.

You can delete the mannequin model at this point, we've extracted all the info we needed from it.

The majority of the work can be done by entering the **Weight Paint **mode after selecting the skeleton first, and the model second. This allows us a liberal use of the **Blur** and **Average** tools to smooth the hard borders of the weights transferred from the mannequin:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/491b1a5b61.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23142155.png -->

Just smoothing most of the groups will get you quite far. In some cases I needed to put in a bit more work and actually repaint some weights to make the deformations look good. This is especially worth doing around the shoulder area, as it moves a lot in-game:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/b36e6f6502.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23142307.png -->

Most of the careful skinning had to be done on the facial bones, as Jigglybuffs facial structure didn't match the mannequin's at all, so all the transferred weights had to be repainted from scratch:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/84bd8a27a8.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23154211.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/4cb3104da5.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23154226.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/d699ba4d34.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23154329.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/81b78db2cb.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23154348.png -->

You'll notice I've applied very light/subtle weights to the lids and the eyebrows. This is because Jigglybuff doesn't really have those, and I just wanted a little suggestion of those movements to show through in his animations. This is how he deforms after all the weights have been adjusted:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/e688352d70.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23154040.png -->

After you're happy with the skinning, make sure to **Normalize **all weights and to **Limit** total bone influences over each verticle to 4, this will help the model's performance in-game. You can do it from the **Weight Paint** mode:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/5061da76ef.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-27031424.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/cae001841a.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-27031439.png -->

**(UPDATE 21.08.24)**

Not necessary, but recommended:
To make full use of the PC-only leg IK system, we need to merge special, non-skinned, IK bones to our skeleton.
The IK bones were added to the mod source in an update:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/566471104c.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-08-21171408.png -->
   
![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/4de325c1a0.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-08-21171538.png -->

Import the IKBones.fbx file into your custom skin scene using the same settings as the original skeleton.

Select first the newly imported (root_IKBones) skeleton, then the original one (root).

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/d46a0a63bd.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-08-21172104.png -->

Press ctrl+ j to join them.

**(/UPDATE 21.08.24)**

 

We can finally export our custom skin to a .fbx file. Select both the mesh and the skeleton and choose these export settings:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/7d80e2e1c2.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23165244.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/fd9d1ae2e3.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-23165402.png -->

 

**3. Set up your character in the Modkit.**

Drag the .fbx you've just exported into the modkit's Content Browser. Check these settings:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/8edccb2c88.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-26224359.png -->

**Make sure you choose the right skeleton when importing! **Choose the UE4_Mannequin_Skeleton located in the /Game/Movement/AnimsetPro/UE4_Mannequin/Mesh location. It **might** work if you choose the other mannequin skeleton (as they should have the same hierarchy), but I can only vouch for the one from the AnimsetPro folder!

The model's vertex normals are likely to be off after importing. If so, go into the skeletal mesh editor and change this setting:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/9c51435087.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-26224814.png -->

When authoring the character's material I recommend following the [Best practices](https://mod.io/g/pavlov/r/best-practices-for-shack-materials). But in short: Pack your textures into channels, Use the "Shared" sampler sources and set the texture groups appropriately (to the character, character normal and character specular groups). Beyond that, it might be worth checking the **High Quality Reflections** option in the material details pannel. It will help the skin look slightly better on the PC version of the game.

For the final tweaks, I recommend going into the skeletal mesh editor and overriding the mesh's physical asset with the default one:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/608bff199c.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-26232746.png -->

and setting up some LODs:

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/2cec717441.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-26225951.png -->

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/3a705118e1.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-26231108.png -->

Congratulations! Your custom skin skeletal mesh is skinned, imported, and ready to be implemented!

![image](images/rigging-a-custom-skin-using-the-vankrupt-mannequin/70a722279a.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2024-05-26231032.png -->


---

## Comments (mod.io API, 1)

- **Fishy!** (2024-06-11): jiggle puf
