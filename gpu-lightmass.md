# GPU Lightmass

> Source: https://mod.io/g/pavlov/r/gpu-lightmass
> Author: markyxl | Added: 2025-03-17 | Updated: 2025-03-17 | Views: 420 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 4 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Use GPU for incredibly fast lighting builds.

---
If you have raytracing-capable GPU, you can leverage [GPU lightmass](https://dev.epicgames.com/documentation/en-us/unreal-engine/gpu-lightmass-global-illumination-in-unreal-engine) for much faster ligting builds.

 

To enable it, go to Edit -> Project Settings and:

- set Platforms -> WIndows -> Targeted RHIs to DirectX 12

- enable Engine -> Rendering -> Hardware Ray Tracing -> Support Harware Ray Tracing

- enable Engine -> Rendering -> Hardware Ray Tracing -> Path Tracing

Do NOT enable virtual textures as the official documentation says. It's not compatible with Pavlov (at least not Shack and at least not last time I tried it).

Close the window and open Edit ->Plugins, search for GPU Lightmass and enable it.

Restart the Unreal Editor and go grab some snack because it will be compiling a shitton of shaders now (it will be necessary only once tough).

Now you can open your project and you should have the menu item Build -> GPU Lightmass. Best place to dock the window is next to Details or World Settings.

![image](images/gpu-lightmass/095e30fbc6.png) <!-- src: https://image.modcdn.io/members/a7d1/21209130/profile/dock.png -->

Uncheck "Show Progress Bars", set Mode to Full Bake, uncheck "Viewport Realtime is ON" and press Build Lighting (do NOT use the standard Build->Build Lighting or Build All Levels). Depending on your hardware it should build by orders of magnitude faster than the old CPU lightmas.

![image](images/gpu-lightmass/4f48decd26.png) <!-- src: https://image.modcdn.io/members/a7d1/21209130/profile/build.png -->

If you want higher quality build increase GI Samples and Irradiance Caching Quality. For indoor maps enable "Use First Bounce Ray Guiding" for best results.

Do check out the official documentation of [GPU lightmass](https://dev.epicgames.com/documentation/en-us/unreal-engine/gpu-lightmass-global-illumination-in-unreal-engine) to learn about all the options.

Note that GPU lightmass produces slightly different results than the CPU one. Here are the differences I'm aware of:

- all emissive materials influence the lighting. You can actually use static meshes as lighting for the entire level

- in standard lightmass lights can pass through the invisible side of a wall (outside of the level) to the inside. In GPU lightmass it's not the case as the path-traced lighting works in the reverse direction (surfaces seek lighting sources rather than light casting light on surfaces)

- transparent materials might end up fully opaque. You can uncheck Visible in Ray Tracing in a Static Mesh's material setting to make the light pass through some important transparent objects like windows (or maybe this used to be an issue just in UE4, I don't recall encountering it recently)

 

 

As a bonus you also get the Path Tracing view mode in which you can instantly see how the lighting should end up (it doesn't take into account lightmap resolutions) but it's a great preview tool for guick lighting prototyping, and as a reference how your lighting should look after baking. If it differs a lot somewhere, your lightmap resolution or lightmap UVs might be messed up.

Lit: (without built ligtmaps)

![image](images/gpu-lightmass/90573ef827.png) <!-- src: https://image.modcdn.io/members/a7d1/21209130/profile/lit.png -->

Path tracing after 1s:

![image](images/gpu-lightmass/670e38cd58.png) <!-- src: https://image.modcdn.io/members/a7d1/21209130/profile/path.png -->
