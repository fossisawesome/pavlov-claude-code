# Best practices for Shack materials

> Source: https://mod.io/g/pavlov/r/best-practices-for-shack-materials
> Author: Szyx_J | Added: 2023-12-05 | Updated: 2023-12-05 | Views: 1592 | Comments: 2 | Tags: graphics, materials, performance, shaders
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 8 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This guide will help your materials look and perform their best in Pavlov Shack.

---
When authoring materials for your *Shack* maps you are likely to encounter issues, either with the visuals or the performance on the target hardware. Here are the tips to make your map look and play its best:

**1. Only use Base Color textures**

Keep the materials as simple as possible in general. Texture sampling is expensive on Quest hardware. Normal and ORM textures will have diminished results because you should:

**2. Force the "Fully Rough" material option and disable "Use Lightmap Directionality"**

Both options are available in the Details panel of your base material.

The "Fully Rough" material option is highly recommended on every level surface for a *Shack* map. It reduces the complexity of the material significantly and is likely to have a massive impact on performance.

![image](images/best-practices-for-shack-materials/c08cf15d8f.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05033008.png -->

The "Use Lightmap Directionality" is forced to be OFF in the game anyway, so disabling it in the modkit will help you achieve a more accurate preview.

To regain some of the more correct shading (the "Fully rough" option doesn't conserve energy making the whole material generally dark) I recommend approximating the specular response with a simple node setup:

![image](images/best-practices-for-shack-materials/febbd49bc6.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05033421.png -->

(or a similar one)

It's worth mentioning that we recommend using full-quality, non "fully rough" materials for things like custom characters and weapons, or important props. It's worth it for them.

**3. Use the "Shared" sampler sources and set the texture groups appropriately.**

When sampling a texture, remember to set the sampler source to "Shared: Wrap" or "Shared: Clamp", depending on your needs. This will help texture filtering, even enabling Anisotropic filtering when appropriate.

![image](images/best-practices-for-shack-materials/a5cdb5f55c.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05041238.png -->

The option is available in the details panel when a *Texture Sample* node is selected. the "Shared: Wrap" option was selected here because the texture is meant to tile.

To ensure the best texture filtering, we recommend you set each level texture to "Project Group 01" as this group is designed for the *Shack *level textures. Texture groups can be assigned in the Texture asset settings:

![image](images/best-practices-for-shack-materials/c0d446e948.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05041923.png -->

**4. Use Vertex Interpolators.

***Shack *materials use lower float precision than their PC counterparts. for this reason, you may have encountered an ugly, pixelation bug on large maps that require tiling. The bug only appears in the headset, while looking seemingly correct in the modkit. Whenever some math (usually multiplication) is applied to the texture UV coordinates to make a texture tile over a large surface, some precision is lost, and the texture looks pixelated:

![image](images/how-to-fix-pixelated-textures/73ac98fb48.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05034831.png -->

The fix for this is thankfully very simple. We just need to put a *VertexInterpolator* node between the math and the texture sampler:

![image](images/how-to-fix-pixelated-textures/2f9800e9da.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035030.png -->

This fixes the pixelation of the tileble texture:

![image](images/how-to-fix-pixelated-textures/eaeefad921.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035406.png -->

**5. Use the "Period" option in the Time node**

Whenever you're trying to make any animated effect, be it a massive fire, moving clouds, or a flowing river, sooner or later you're gonna wanna animate your UV coordinates. That's where the float precision rears its ugly head again, the animation appears "jittered" and broken when played on the target hardware, while appearing correct on the modkit. The way to fix it is to use the "period" option in the time node to shift the timer generation to the CPU, and to clamp it in a range more comfortable for the float precision used on Quest. Choosing the right value for the period can be tricky depending on your use case, ideally, you want to set it to a value that will make your UV animation loop perfectly. When that value is impossible to calculate, or just annoyingly difficult, just set the period value to something big, like 120, this way a slight jitter in the animation will only happen once every 2 minutes.

Here's an easy *Panner *setup for a simple, flowing river, note the *VertexInterpolator *tip from the previous point remains true. The period of 2 was adjusted to match the speed of the panner, 2 x -0.5 = -1, which means that the texture will pan exactly once  before it jumps back to the original position, making the movement seem perfectly smooth.

![image](images/best-practices-for-shack-materials/69db83e5da.png) <!-- src: https://image.modcdn.io/members/0fb4/27379166/profile/zrzutekranu2023-12-05035649.png -->


---

## Comments (mod.io API, 2)

- **EYY3** (2024-02-18): Lovely tutorial! Would it be possible to explain how exactly the specular response approximation workaround works? I hate to take it as a blackbox... :)
- **Cheeto_V** (2023-12-05): Great stuff, and lovely solutions to hardware limitations
