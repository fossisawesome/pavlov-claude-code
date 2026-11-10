# Easy &amp; Simple Custom Weapon Skins

> Source: https://mod.io/g/pavlov/r/how-to-do-custom-weapon-skins
> Author: SmallDarkOne | Added: 2025-09-07 | Updated: 2025-09-07 | Views: 462 | Comments: 0 | Tags: Custom Skin, General Guide, Gun
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 0 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This guide introduces you to my new skin system intended for default/vanilla pavlov weapons.

---
##### Looking for a way to do custom weapon skins without blueprint knowledge?Welcome to the [Skin System Mod](https://mod.io/g/pavlov/m/smalls-skin-system#description) for Pavlov VR!

This mod allows you to apply and manage custom skins with ease while keeping everything fair and compatible with the base game.
Unlike other mods, this system cannot override paid skins or equipped skins. It only works with the default skins, ensuring that official cosmetic purchases remain untouched.
Designed for accessibility, the setup process is straightforward and requires no prior blueprint knowledge. Whether you’re a seasoned modder or a complete beginner, you’ll be able to get your skins running in just a few minutes.

Make sure to follow the installation guide on the [source mod](https://mod.io/g/pavlov/m/smalls-skin-source#description).

### How do I make custom weapon skins then?

Firstly, download the weapon model of choice from the [Pavlov Artists](https://discord.gg/VBawy5m4VF) discord.
Then, by using a tool like adobe substance painter, create the skin you'd like to use. Avoid using above 1024x1024 resolution if on shack!
After, export the skin and create the material (preferably instanced) in Unreal Engine; make sure that 'Used with Skeletal Mesh' is ticked in the material properties.
Finally, follow the guide on the source mod linked above. Make sure the Skin System Mod is a dependency on your map/mod.

**If you have any issues make sure to comment them on the SOURCE mod, not the skin system mod.**
