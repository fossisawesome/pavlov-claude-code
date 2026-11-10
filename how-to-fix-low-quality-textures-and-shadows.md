# How to fix low quality textures and shadows

> Source: https://mod.io/g/pavlov/r/how-to-fix-low-quality-textures-and-shadows
> Author: EconnAKZ | Added: 2024-03-21 | Updated: 2024-06-07 | Views: 899 | Comments: 6 | Tags: Help, Mapping, Mod, Shack, Shadow, Texture
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 17 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: If you're having issues with low quality textures and shadows on your Pavlov Shack map, this guide will teach you a few simple tricks to fix your map and make it look great.

---
### Textures

 

To get started, you will want to find all of your textures under the UGC folder, you can simply filter out your assets by clicking on this icon below and selecting 'Textures.'

![image](images/how-to-fix-low-quality-textures-and-shadows/07510d7965.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/icon.png -->

 

Next, press and hold the shift key and select the first and last texture in your folder.

 

![image](images/how-to-fix-low-quality-textures-and-shadows/930ef80db7.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/guide2.png -->

 

Right click on your selected textures and find and select 'Asset Actions.' Next you will want to click on 'Bulk Edit via Property Matrix' and another panel should appear. Press and hold the shift key and select all the tabs on the panel.

 

![image](images/how-to-fix-low-quality-textures-and-shadows/04587066b7.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/guide3.png -->

 

On the right side of the panel, select 'Level of Detail' and make sure the property 'Mip Gen Settings' is set to 'Sharpen 0.'

 

![image](images/how-to-fix-low-quality-textures-and-shadows/5e1f505301.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/sharpen.png -->

 

Close the property matrix and click the Save All button in the editor to save your changes. These changes will make sure your textures don't end up getting very blurry in game.

 

 

### Shadows/Lightmaps

 

The configuration for fixing your shadows is pretty much the same process as with the textures, however, be aware that building the lighting will rewrite the lightmap textures. This means you will have to redo this part of the process if you bake your lighting again. The process here is very simple, but it can be tedious depending on how many lightmaps you have generated for your map.

 

If you have not done so already, build the lighting on your map. After this is done, go to the World Settings and find the 'Lightmaps' option located under the 'Lightmass' tab.

 

![image](images/how-to-fix-low-quality-textures-and-shadows/ca5a197877.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/guide5.png -->

 

Click on the 'Lightmaps' option to show all of the lightmaps created for your lighting. 

 

![image](images/how-to-fix-low-quality-textures-and-shadows/dd5e1bb2d3.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/guide6.png -->

 

This part is a bit tedious; you will have to double click on each lightmap and change them all manually. Go ahead and select the first lightmap, a new panel should appear. In the 'Level Of Detail' section located at the top of the 'Details' area, change the 'Mip Gen Settings' and make sure that 'NoMipmaps' is the selected option. You can now save and close this panel out; you will have to do this process for the rest of your lightmaps. 

 

![image](images/how-to-fix-low-quality-textures-and-shadows/a14f784808.png) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/guide7.png -->

 

Please remember that you will have to do this process again if you decide to build the lighting.

 

### Conclusion

Once you have gone through these steps, the next time you upload your map and try it out in game, your textures and shadows should all appear normally. To show the results, here are a few side by side comparison pictures of the final results.

 

#### Bad Lighting and textures:

![image](images/how-to-fix-low-quality-textures-and-shadows/38e86c061f.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-185.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/05078603bd.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-185.4.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/61e9e60eae.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-185.1.jpg -->

-
![image](images/how-to-fix-low-quality-textures-and-shadows/46733ad367.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-185.3.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/9109be604c.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-185.2.jpg -->

 

#### Final product:

![image](images/how-to-fix-low-quality-textures-and-shadows/a286a55bd0.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-183.1.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/d163d5f866.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-183.2.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/d2b3ed2f39.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-183.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/a0f7f1ab3a.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-183.4.jpg -->

![image](images/how-to-fix-low-quality-textures-and-shadows/06a84a1816.jpg) <!-- src: https://image.modcdn.io/members/3fca/13551772/profile/com.oculus.vrshell-20240320-183.3.jpg -->


---

## Comments (mod.io API, 6)

- **zpaquette0908** (2024-07-19): yo i just wanna know how to put textures in my map i use pavlov mod kit and 5.1.1 unreal engine
- **Griffoster_Dev** (2024-05-30): how do i make a lightmap?
- **EconnAKZ** (2024-04-14): Sounds about right to me
- **sharpbelt636** (2024-04-14): to use diferent mipping levels would i just click uptop where it says mip level 0 and just choose mip level 1?
- **EconnAKZ** (2024-04-13): This is expected since you are completely turning off mips, I still need to update this doc with more information on stuff like that, but you could try using different mipping levels rather than shutting it off and seeing if it works better for ya. You could also try turning off the virtual texture option located in the project settings under the rendering tab.
- **sharpbelt636** (2024-04-13): without mip maps the textures look very tv static like from distance is there a way to prevent this?
