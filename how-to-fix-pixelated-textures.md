# How to fix pixelated textures

> Source: https://mod.io/g/pavlov/r/how-to-fix-pixelated-textures
> Author: zaynethedev | Added: 2025-06-07 | Updated: 2025-10-14 | Views: 491 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 6 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This tutorial shows you how to fix pixelated textures in your game.

---
Have you ever developed your map, with all the textures looking good on the editor, but in-game they look all pixelated? Well, here's a tutorial on how to fix it!

**Use Vertex Interpolators.

***Shack *materials use lower float precision than their PC counterparts. for this reason, you may have encountered an ugly, pixelation bug on large maps that require tiling. The bug only appears in the headset, while looking seemingly correct in the modkit. Whenever some math (usually multiplication) is applied to the texture UV coordinates to make a texture tile over a large surface, some precision is lost, and the texture looks pixelated:
[![image](images/how-to-fix-pixelated-textures/73ac98fb48.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05034831.png -->](https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05034831.png)

The fix for this is thankfully very simple. We just need to put a *VertexInterpolator* node between the math and the texture sampler:
[![image](images/how-to-fix-pixelated-textures/2f9800e9da.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035030.png -->](https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035030.png)

This fixes the pixelation of the tileble texture:
[![image](images/how-to-fix-pixelated-textures/eaeefad921.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035406.png -->](https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035406.png)

### If the above does not resolve (rare cases)

Go into the material that is pixelating, and scroll down to the **Mobile** tab.

![image](images/how-to-fix-pixelated-textures/55350d9ee4.png) <!-- src: https://image.modcdn.io/members/ec7c/31471931/profile/thing1.png -->

Now change **Float Precision Mode** to **Use Full-precision for every float** and save the material. 

![image](images/how-to-fix-pixelated-textures/6a6a38e946.png) <!-- src: https://image.modcdn.io/members/ec7c/31471931/profile/thing2.png -->

Now, open the actual texture file that the material is using. You should see an option in the **Level Of Detail** tab, called **Texture Group**. Change it to either **Weapon**, or **World**.

![image](images/how-to-fix-pixelated-textures/14a7a51ca0.png) <!-- src: https://image.modcdn.io/members/ec7c/31471931/profile/thing3.png -->

Now, just save the texture, and republish the map! The issue should be fixed. If it isn't, message me on Discord! My username is **zaynethedev**!

Find more information from the Pavlov Technical Artist here: https://mod.io/g/pavlov/r/best-practices-for-shack-materials
