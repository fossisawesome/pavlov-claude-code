# Common Mistakes Made By New Mapmakers

> Source: https://mod.io/g/pavlov/r/common-mistakes-made-by-new-mapmakers
> Author: AlexanderHille | Added: 2024-07-16 | Updated: 2024-07-16 | Views: 751 | Comments: 1 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 16 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: These are common mistakes I've seen on maps made by beginner mapmakers, and how to fix them.

---
This guide includes mistakes that I noticed that many beginner mapmakers make when making their map. I will go into how to fix these mistakes

The mistakes I go into include

1. Forgetting to build **lighting**

2. Not adding Phys Materials **(affecting bullet holes, footstep sounds, wallbangability)**

3. Having materials that are too **shiny or weird looking**

4. Using basic shape meshes to **build the geometry of the map**

5. Not knowing what to do with **Reflection Captures**

 

 

**1. Forget to build lighting**

Pavlov uses prebuilt lighting, meaning the map's lighting and shadows are calculated when the map is being made. If the mapmaker skips the step of building the lighting, then the map in game won't have any shadows, and lighting will be approximated by using the direction of the directional light.

![image](images/common-mistakes-made-by-new-mapmakers/ab3a6edba7.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/bestbuynolight.jpg -->

To build lighting, go to the **Build** tab at the top of the screen. There you will see an option to change the **Build Quality **which affects how long and precise the build lighting process will take. I recommend you select preview to quickly check how the lighting will look while you're making the map, and I recommend you select production when doing the final light build before finishing and uploading the map.

To begin the light building, click **Build All Levels**. 

![image](images/common-mistakes-made-by-new-mapmakers/5739682656.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/buildwindow.jpg -->

After your computer processes the lighting, which may take a while depending on the lighting quality you chose, the size of the map, and how many lights there are, the map will have lighting that will show in game.

![image](images/common-mistakes-made-by-new-mapmakers/ff7b6e222e.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/bestbuylight.jpg -->

**2. Don't know how to add Phys-materials**

Phys-materials are what tells the game what type of material a texture is, affecting things such as what bullet hole shows up when something is shot, what footstep sound plays when something is walked on, and if that thing is wall-bangable (with high caliber weapons such as rifles, snipers, deagle and revolver).

![image](images/common-mistakes-made-by-new-mapmakers/13770e53fe.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/nonematerial.jpg -->

The default Phys Material is **None**, which has the metal bullet hole when shot, without the metallic sound, and it is wall bangable. This means that if a mapmaker forgets to change the phys material then every surface in their map will be wall bangable.

You may have a problem where there are no results when going to change the Phys Material.

![image](images/common-mistakes-made-by-new-mapmakers/51f3e965cc.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/nophysproblem.jpg -->

To fix this, go into the PhysMaterials folder in the CustomMapToolsContent folder, select all the phys materials, then rightclick. Repeat with the contents of the phys materials in the **Thin **folder. When you do this, their Icons will change and you'll be able to go back and change the Phys Materials to them. Any unused phys materials will reset back to its unusable state when you close unreal engine, and you'll have to repeat the short process if you want to use them.

Now you should be able to change the phys materials in the details tab of your materials.

Note: If you want a material to be wallbangable, set it to one of the **Thin** phys materials.

**3. Materials are too shiny and weird looking**

Unreal Engine is a modern game engine, having it's material system be very complex so game developers can edit their materials in various ways. Because of this, the material system can be very overwellming for new mapmakers. These new mapmakers may forget to change the roughness of their materials, leaving some of them more shiny than they should be.

![image](images/common-mistakes-made-by-new-mapmakers/2f2aa2e8b8.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/shinycarpet.jpg -->

This image shows a floor with a material that has the default roughness. In the context of the floor being made of carpet, we don't want it to be this shiny. Theres a couple of ways to fix this.

First way is to go into the material, and check the box for the setting refering to **Fully Rough. **This setting makes the material only use a base color, which is great for performance on pavlov shack.

![image](images/common-mistakes-made-by-new-mapmakers/867d83632e.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/fullyroughytee.jpg -->

Another way to change roughness (or any other value in a material) is to use a scalarParameter node to edit the value

![image](images/common-mistakes-made-by-new-mapmakers/f38f4e32f2.png) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/scalareditor.png -->

![image](images/common-mistakes-made-by-new-mapmakers/b9476b0d05.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/paramrough.jpg -->

The great thing about this is that if you create a **Material Instance** of the material, then you'll be able to edit this value easily for that one instance

I highly recommend you use Material Instances because then you'd only have to edit one material, and any time you want to use another texture, make an instance of your main material to easily have a new material

![image](images/common-mistakes-made-by-new-mapmakers/9cf68affd5.png) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/matinstance.png -->

There is a folder in the modkit for materials that are optimized for shack. making instances of these materials is the easiest process if you don't want to learn to make your own materials

![image](images/common-mistakes-made-by-new-mapmakers/fd92ad6741.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/shackmats.jpg -->

**4. Don't know what to make the map with**

There are a couple ways to make the geometry of the map with. I would not recommend making it using the basic shapes that are in Unreal Engine. They are probably the least efficient tool to make a whole map out of.

![image](images/common-mistakes-made-by-new-mapmakers/57f7483f1d.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/meshshapes.jpg -->

I would much rather recommend using the **Geometry Brush** tab in the place actors window to build your map with, if you want to build your map directly in the Unreal Engine Editor. The Geometry brushes can have each of their surface's texture setting edited, and you can have a **subtractive** brush to cut out areas of an **additive** brush, which you can't do with the basic shape meshes (The option to change a brush from Additive to Subtractive is found in the details tab when a Brush is selected)

![image](images/common-mistakes-made-by-new-mapmakers/1f8188143c.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/geometrybrushthing.jpg -->

This short video shows the difference between Meshes and Brushes in Unreal Engine, and what you're able to do with Brushes.

Note: This video was recorded in Unreal Engine 4, instead of 5, which is why it looks different

Brushes are what I recommend if you wanna build your map directly in the Editor, but if you know how to, you can always make your map in another modeling program and import it into Unreal Engine.

 

**5. Reflection Captures are missing or don't cover the whole map**

Reflection captures are what pavlov use for reflections. They include a single point and a volume. The single point is where a 360 image is captured and anything in the reflection capture's volume that is reflective will use the 360 image for its reflection. any area that isn't covered with a reflection capture will not show reflections for anything. This is why some maps will not have reflections for guns or playermodels.

![image](images/common-mistakes-made-by-new-mapmakers/6497b86c4d.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/reflectioncapture.jpg -->

Reflection Captures are built when the lighting is built, but there is an option to build reflection captures without building the lighting in the build tab.

![image](images/common-mistakes-made-by-new-mapmakers/dc24b3f58d.png) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/reflectbuilt.png -->

If you have areas of your map with different appearances (like what is pictured below) then you should have a reflection capture for each area. In the example below, if there was only one reflection capture in the blue room that covered the whole map, then going into the red room would mean anything's that reflective (guns, playermodels) would have a blue reflection which wouldn't look right. have different captures for any areas with wildly different colors or brightness.

![image](images/common-mistakes-made-by-new-mapmakers/7c3b9e38f9.jpg) <!-- src: https://image.modcdn.io/members/a85e/14140695/profile/refleccolor.jpg -->

 

That is it for the common mistakes made by beginner Mapmakers

I hope this guide will lead to you making better maps.


---

## Comments (mod.io API, 1)

- **Pitufo1213** (2024-07-17): Another: Not to make basic ahh boxes and call them houses (90% of RP's) You guys know who you are.
