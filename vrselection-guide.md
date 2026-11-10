# VRSelection Guide

> Source: https://mod.io/g/pavlov/r/vrselection-guide
> Author: Holosight_M4 | Added: 2026-05-17 | Updated: 2026-05-17 | Views: 288 | Comments: 0 | Tags: Blueprint, VRSelection
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 7 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: How to use the HORRIBLE component known as "VRSelection"

---
**VRSelection is a component that allows you to make your blueprints glow similarly to items ingame, this mod.io guide will walk you through how to use it properly**

Start off by adding the VRSelection component to your blueprint, just like so

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17181616.png)

Then you are going to want to select your "VRSelection" component, navigate to the right side of the screen and click "Proxy Mesh Material" and then click selection overlay

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17181959.png)

The selection overlay is what gives the "glowing" effect

Now you are going to want to create a function called "Activate" and a function called "Deactivate" once you've done that, it should look like this

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17183922.png)

After this, double click the "Activate" Function to edit it then add an input thats an actor to the node that says "Activate", then drag off that pin and create a "Cast to VRController" node, after that, add a generic haptic node and connect the casting to the target, Like this

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17182706.png)

After that, you want to add a branch to check if the controller is valid, and then activate the VRSelection CMP

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17182816.png)

Then you are going to work on the "Deactivate", its similar to this one however its has alot more code, which is why Im just gonna send a screenshot of what you have to do instead of describing it

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17184130.png)

And finally, get your interactbox/mesh and get these 2 events from them

![image](https://image.modcdn.io/members/8099/51067591/profile/screenshot2026-05-17184403.png)
