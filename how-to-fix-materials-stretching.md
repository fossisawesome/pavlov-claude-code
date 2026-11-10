# How to fix materials stretching.

> Source: https://mod.io/g/pavlov/r/how-to-fix-materials-stretching
> Author: Lynxorzo | Added: 2025-12-17 | Updated: 2025-12-17 | Views: 322 | Comments: 0 | Tags: General Guide, Materials/Textures
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 1 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This guide will teach you how to fix your materials stretching whenever you scale a block or object!

---
### How to fix materials stretching:

#### Part 1: Converting Textures to a Texture Object and creating "WorldAligned..."

1. Open whatever material your trying to fix.

2. Select your Base Color/Map, and Normal Map if Applicable.

3. Right click and click, "Convert to Texture Object"

4. Create a "WorldAlignedTexture" and connect your base map into "TextureObject (T2d)"

5. Connenct the "XYZ Texture" into "Base Color"

#### Part 2: Fixing the Normal Map (if applicable)

1. Create a "WorldAlignedNormal" and connect your normal map into "TextureObject (T2d)"

2. Connect "XYZ Texture" into "Normal"

#### Boom your done!

#### Part 3: Fixing the scale of the textures (OPTIONAL)

1. Create a "Constant" and right click it to convert it into a "Parameter"

2. Set the "Default Value" to "300" (this is just my liking)

3. Connect the Parameter to "TextureSize (V3)" on both the "WorldAlignedTexture" AND the "WorldAlignedNormal"

#### If done correctly it should look like this:

![image](https://image.modcdn.io/members/0717/36441047/profile/screenshot2025-12-16190559.png)

**Thank your for using my guide, if you have any issues/questions, DM .lynxorzo. on Discord or in the Pavlov Mod.io Community Server! You can also leave a comment below.**
