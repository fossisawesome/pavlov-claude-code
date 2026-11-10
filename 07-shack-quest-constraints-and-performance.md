# 07 - Shack/Quest Constraints and Performance

Sources: wiki Getting_Started, Workshop_troubleshooting, Quest_Troubleshooting; mod.io guides (masked materials, dynamic shadows, Android packaging); kit `DefaultEngine.ini`.

## Hard rules [V]
- **Lighting**: all lights **Static**. Dynamic shadows **do not work on Shack**; the Dynamic Shadows 2 mod is PC only (forward renderer; only spot/directional can cast; must be Movable; has distance limits). `r.MobileNumDynamicPointLights=0`, movable directional lights disabled.
- **Textures**: **512x512** (larger gets downscaled). ASTC compression. Keep **UVs in 0-1**; outside = pixelated on Quest.
- **Materials**: must be **instances of the kit's Shack materials** (`CustomMapTools/Content/Materials/Shack`): `M_Shack_Rough_Simple`, `M_Shack_Rough_Precise`, `M_Shack_Rough_Emmisive`, `M_Shack_OnlyEmmisive`, `M_Shack_PlainColor`, `M_Shack_Masked`, `M_Shack_Translucent`. Never edit the base Shack material. Otherwise: invisible geometry (collision still works).
- **Collision**: set mesh collision complexity to "Use Complex as Simple" for quick player collision; inspect with Viewmode -> Player Collision.
- **Renderer**: mobile forward, MSAA 4x, no mobile HDR, multiview on, Vulkan, arm64 only, ASTC.
- Everything must be in the UGC folder. Keep package size small: players download maps over mod.io on a headset. Use QuickBMS on a staged pak to find large files.
- Player count: <=10 recommended on Shack servers, max 24.
- Physics: Chaos; some features removed for performance. Avoid heavy simulation/destruction (a destructible glass example exists in the kit).

## Masked materials on Shack [V mod.io, Marco_G17]
Masked is expensive on Quest but these are ~free: (1) **Use Alpha to Coverage** (material -> Mobile -> Advanced; MSAA smooths edges; mobile only, most important); (2) texture **Scale Mips for Alpha Coverage** with threshold ~0.75; (3) **Adjust Max Alpha** 1.0-10.0 (not for binary alpha).

## Tips for performance [mix V/D]
- Use Level Instances and shared Content Mods to cut upload size and duplicated assets.
- Avoid overlapping many lights with dynamic shadows (PC). Static light count is unrestricted but bake times grow.
- Reflection captures: required but keep count reasonable; box captures per room.
- Overdraw: use cutout alpha meshes sparingly (video: "Overdraw Fix Automated Cutout Alpha" by Hangry Bunnies From Mars).
- Quest heat throttles performance (cool down; lower render scaling in Pavlov settings).
- Budgets (community guide `optimization`): Quest 2 ~680K tris / 400 draw calls, Quest 3 ~740K / 500. Measure in-game with `stat scenerendering`/`stat unit`. Culling distance is half on Shack. Full details plus the official Shack material rules (Base Color only, Fully Rough, Shared samplers, Project Group 01, VertexInterpolator, Time Period) are in [12](12-modio-guides-triage-and-findings.md).

## Release channels and devices
Newest content works on the **RC** release channel; the main live channel will be merged later. Users on Quest 2/3. Switching RC <-> live may need the mobile Meta app + reinstall.
