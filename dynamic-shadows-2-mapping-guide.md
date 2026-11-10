# Dynamic Shadows 2 Mapping Guide

> Source: https://mod.io/g/pavlov/r/dynamic-shadows-2-mapping-guide
> Author: Stevie257 | Added: 2025-06-16 | Updated: 2026-07-15 | Views: 539 | Comments: 0 | Tags: Map Making, Mod
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 8 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A guide for mappers on how to properly configure their light(s) to work with the Dynamic Shadows 2 mod

---
This guide will show you how to set up your map for the [Dynamic Shadows 2](https://mod.io/g/pavlov/m/dynamic-shadows-2) mod and what settings you can change to customize their appearance.

##### Dynamic Shadows 2 uses Unreal Engine shadowsIf you're already experienced with using dynamic lighting in Unreal, you can probably skip this guide.However Pavlov, as well as this mod, do have some unique configurations that you may have to work around, so it may be worth it to skim over this guide anyways.

 

### Important Info

There are a few things you should consider before using dynamic lights

- Dynamic shadows don't work on shack

- Dynamic shadows will add extra performance cost to your map

- Dynamic shadows wont appear in the editor

- Pavlov uses the **forward renderer**, meaning **each light** that casts dynamic shadows adds more performance cost
You'll need to be mindful of where you place your dynamic lights, and if you have too many overlapping at a time all shadows may get disabled by the engine
More info about this should be available in the Unreal Engine documentation

- Point lights and rect lights cannot cast dynamic shadows

- Static lights and stationary lights can't cast dynamic shadows, however you can still bake their lighting data like normal
(you can combine baked bounce lighting and dynamic shadows for some lights, more info on that later)

- Dynamic shadows have a distance limit, which is customizable, but is present nonetheless

- **The Dynamic Shadows 2 mod is currently still a work in progress and may have issues**

Make sure none of these are a deal breaker for your map before continuing

 

### Map Setup

You'll need to configure your lights that you want to cast dynamic shadows
Only spot and directional lights can cast dynamic shadows, so this guide will mostly be about those types of lights

**Any lights you want to cast shadows will need to be set to "Movable"**

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/moveable.png)

 

#### Directional Lights

You may want to change some settings in your directional light, AKA the sun, to make things look better in-game.

These are the settings I used in my test map that I thought looked the best.

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/directionallightsettings.png)

*** Draw calls increase with the number of shadow cascades you have. 10 will probably be far too many for an ordinary map.
Keep an eye on the graphical statistics and visual appearance of your map and adjust the following settings accordingly.**

**
Dynamic Shadow Distance MovableLight** - The distance from the camera that shadows will be fully cutoff. They'll downscale in quality up to that point based on how many cascades you have and their distribution (explained below). Can be changed to basically whatever you want, but keep performance in mind.

**Num Dynamic Shadow Cascades** - Unreal uses cascaded shadow maps, which basically splits dynamic shadows into different levels of detail that decrease the farther the shadow is from the camera. This setting increases the number of detail levels. The more cascades you have the more detailed shadows up close will be, but this also decreases performance. I chose 10 for my test map and for the screenshots in this guide because the test map was very low detail with no props. Choose this setting carefully and try to keep as low a number as you can. 

**Distribution Exponent** - This controls the distribution of the cascades. A higher number puts more cascades close to the camera, and a lower number more evenly distributes them across the shadow distance. I chose 2 for my test map to give a more even spread the farther you get from shadows.

You can probably leave these settings default. Play around with them and see what looks and runs best on your map.

 

#### Spot Lights

Spot lights are pretty standard, I've gotten them to look fine in my test map without any special configuration. Just remember that lights need to be set to movable to cast shadows, and lights with a larger attenuation radius will cost more

 

#### SkyLight

Because dynamic lights don't get bounce lighting, you may still want to use a static skylight and bake your map lighting. More info on fully dynamic skylights in the next section.

|

**Static skylight baked at production quality using a dynamic directional light**

 |

**Movable skylight using a dynamic directional light with forced no precomputed lighting**

 |

|

A room in shadow with movable spotlights casting dynamic shadows

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/roombakedskylight.png)

 |
Same room with movable skylight and no precomputed lighting

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/roommoveableskylightnoprecomp.png)
 |

|
Cubes set as movable on the left and set as static on the right

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/bakedskylightoutside.png)
 |
Same cubes with movable skylight and no precomputed lighting

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/moveableskylightnoprecomp.png)
 |

 

### Finishing Steps

Once you've got your map set up you just need to add the Dynamic Shadows 2 mod to your map as a dependency to see the shadows in-game
**https://mod.io/g/pavlov/m/dynamic-shadows-2
**

 

### Tips and Tricks

#### Combining Baked Lighting with Dynamic Shadows

As mentioned before, static lights cannot cast dynamic shadows. However on spot and directional lights, you can get some of the benefits of baked lighting while still having dynamic shadows.

If you set your lights to **stationary **and bake your lighting, you should be able to bake their bounce lighting into your map. After you've baked your lighting **you'll need to set your lights back to movable for them to cast dynamic shadows**.

Here's a room with a spot light and a window to let the directional light shine through, using a static skylight, built at production quality. The spot and directional light were set as stationary for baking and then set to movable afterwards. Both are casting dynamic shadows on the characters.

![image](https://image.modcdn.io/members/0492/29223580/profiledynguide/bakedstationarytomoveableroom.png)

The issue with this method is these baked features are static, so you couldn't use this with a rotating directional light or a moving spotlight.

 

#### Day/Night Cycle

I was able to make a working day night cycle on my test map by combining a movable directional light, a dynamic skylight with Real Time Capture enabled, and a custom SkySphere with a custom material set to refresh every frame

If you're using a SkySphere in your map you'll need to make a custom copy of the ShySphere where you can change out it's sky material with your own custom copy of the sky material. Dynamic skylights with real time capture require something it thinks is the sky to pull colors from and the default SkySphere's material isn't marked as IsSky for whatever reason, so you'll need to make custom copies to change that. I can make this it's own dedicated guide later if people are interested.

![image](https://github.com/Stevie257/images/blob/6f3556fba4d9833ed8ffe19f7bb8b1e95a11c711/jared.gif?raw=true)

 

### Conclusion

I think that's about all I have. If you have any questions ask them in the comments or reach out to me on Discord and I'll answer them there and/or add to the guide, my username is Stevie257

You can play on the test map shown in the screenshots here
https://mod.io/g/pavlov/m/shadow-testing-map

Thanks for reading, and I hope your computer doesn't explode! ♥
