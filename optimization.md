# Oculus/Shack and PC Optimization

> Source: https://mod.io/g/pavlov/r/optimization
> Author: SmallDarkOne | Added: 2024-07-20 | Updated: 2026-02-22 | Views: 1521 | Comments: 2 | Tags: Map Making, Optimization, Optimizing, PCVR, Shack
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 0 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Just a basic way to learn optimization recommendations for Shack and PCVR.

---
### Shack and PCVR Optimization Guide — Introductionary

 

Optimization is especially critical for Shack, the standalone and lower graphic version of PCVR, to deliver an optimal user experience. Unlike PCVR, which can leverage high-end hardware for rich, detailed graphics and complex things; Shack operates on top graphical chips yet with limited processing power and graphical capabilities. 

 

**Dictionary:**

- Triangles: In 3D modeling, triangles are the basic building blocks used to create and render complex shapes. They are the simplest type of polygon, and any 3D model is composed of many triangles arranged to form detailed surfaces.
      

- Drawcalls: This refers to the process of sending commands from the CPU to the GPU to render objects on the screen. Each draw call represents a request to draw a specific set of objects, materials, or textures. Reducing the number of draw calls can improve performance, as each call involves overhead and switching between different assets or states.

 

|
Use console command: stat scenerendering |
  |
**Quest 2** |
  |
**Quest 3** |
  |
**PCVR (Recommended)** |

|
**Max Triangles** |
**   ** |
680K |
**   ** |
740K |
**   ** |
1.5 Million |

|
**Max Drawcalls ** |
**   ** |
400 |
**   ** |
500 |
**   ** |
1100 |

 

 

### Reducing Draw Calls and Optimizing Rendering

 

Reducing draw calls and optimizing rendering features significantly impacting methods.
There are many ways to do this:

- **Static Mesh Batching and Instancing**: Group static meshes with the same material and use instanced static meshes for repeated objects.

- **Use Fewer Materials and Textures**: Combine textures into atlases and use shared materials.

- **Level of Detail (LOD)**: Implement LODs for meshes and materials to reduce complexity for distant objects.

- **Merge Static Meshes**: Use the Merge Actors tool or Blueprints to combine meshes.

- **Optimize Occlusion Culling**: Enable occlusion culling and use cull distance volumes for small objects.

- **Simplify Collision Meshes**: Use simple collision shapes.

- **Efficient Blueprints and Level Streaming**: Optimize Blueprints and use level streaming to load/unload parts of the world.

- **Material and Shader Optimization**: Use material instances and simplify shaders.

- **Reduce Overdraw**: Minimize transparent materials and avoid layered objects.

- **Culling and Visibility Settings**: Use visibility and distance culling to hide off-screen or distant objects.

- **Texture Streaming**: Use mipmaps and compress textures to ensure efficient texture streaming.

- **Distance Culling**: Ensure distance culling to avoid rendering off-screen or distant objects.

- **Reflection Optimization**: Optimize reflection capture settings and adjust screen space reflection quality.

- **Volumetric Effects**: Use lower quality settings for volumetric fog and lighting.

- Precomputed Visibility: Enable in world settings and add a volume around play space, it will help cull things not shown at the moment.

It is recommended to at least learn most of these on the list and some apply to certain situations.
Culling distance in the engine is (for some weird reason) half in Shack.
With these techniques you should try to reach the suggested triangle/drawcall count in the introductionary for your specific device.

When comparing statistics to monitor performance, you must get in-game statistics as the Unreal Editor is inaccurate and accounts things from content drawer and editor itself etc. Below are some commands you can use with an "Execute Console Command" node in a basic actor blueprint linked to begin play, this means the commands run in game and provide stats for you.

- "stat unit" - Gives stats on draws and prims and a few more useful stats.

- "stat summary"- Gives amount of memory used currently.

- "stat detailed" - stat unit but has way more statistics and a render time graph.


---

## Comments (mod.io API, 2)

- **Meowmont** (2024-08-12): Fr
- **MaxweIl** (2024-08-08): if all the crappy RP maps read this, there would be an optimization revolution
