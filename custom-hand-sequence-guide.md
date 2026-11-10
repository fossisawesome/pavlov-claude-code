# Custom hand sequence guide

> Source: https://mod.io/g/pavlov/r/custom-hand-sequence-guide
> Author: Brav_Soldat | Added: 2023-03-30 | Updated: 2023-04-03 | Views: 737 | Comments: 0 | Tags: CustomGun, CustomItem, Gun, Item
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 13 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Follow this guide to create custom hand poses for your custom gun or custom item.

---
Sometimes when creating a custom gun, the included hand animations don't line up well. To solve this, a custom hand pose must be created. This guide should help with that process.

This can be done with the default hand pose (flat) but its easier to use an existing hand animation and modify it to fit better.

 

**Adding the preview mesh**

Navigate to the included hand skeleton and open it: (Content/Hands/Mesh)

![image](images/custom-hand-sequence-guide/c6a8fd2092.png) <!-- src: https://i.imgur.com/jeMkxZi.png -->

Right click the "hand" bone at the very top, then "Add Preview Asset" and search for your gun mesh:

![image](images/custom-hand-sequence-guide/535ffe7fb5.png) <!-- src: https://i.imgur.com/s37bYxM.png -->

Select the gun skeletal mesh (purple/pink asset) it should then look like this:

![image](images/custom-hand-sequence-guide/5c7cb2dc70.png) <!-- src: https://i.imgur.com/8XUhf1A.png -->

From here there are two options:

1. Modify this hand/ its current pose to fit the weapon. (flat hand)

2. Apply a hand pose already included in the modkit and modify it.

 

For this guide, we will be going with option #2 since its easier.

Up at the top, click on the "Preview Animation" dropdown and find a good starting animation to edit:

![image](images/custom-hand-sequence-guide/9be8ef36e6.png) <!-- src: https://i.imgur.com/KNpb8h8.png -->

Make sure to use the "_Weapon" or "_TwoHand" animations.

Once added it should look like this:

![image](images/custom-hand-sequence-guide/6dd19dd985.png) <!-- src: https://i.imgur.com/qZn4Z1w.png -->

The hand animation will probably be playing, make sure to pause it and drag the timeline slider all the way to the left: (0 position)

![image](images/custom-hand-sequence-guide/c332511749.png) <!-- src: https://i.imgur.com/yd2VVgJ.png -->

The hand mesh itself can be changed if naked hands are needed: (WWII guns)

![image](images/custom-hand-sequence-guide/9b7b0d17c4.png) <!-- src: https://i.imgur.com/UmZGEY8.png -->

Position the hand origin with the "root" bone:

![image](images/custom-hand-sequence-guide/cf67b6e765.png) <!-- src: https://i.imgur.com/J3pWbgb.png -->

Adjust the fingers until you are happy: (the final pose should be the index finger resting on the trigger)

![image](images/custom-hand-sequence-guide/c65e6af4e5.png) <!-- src: https://i.imgur.com/IZWIi5d.png -->

Once you are happy, click on the "Create Asset" dropdown at the top, then "Create Animation", and finally "Current Pose":

![image](images/custom-hand-sequence-guide/121cd8e59c.png) <!-- src: https://i.imgur.com/dPmURbA.png -->

A new window should open to name and save the new animation asset:

![image](images/custom-hand-sequence-guide/d104fd197e.png) <!-- src: https://i.imgur.com/fBP7Peq.png -->

This process can also be used to make TwoHandGrip poses:

![image](images/custom-hand-sequence-guide/b1d3d92de2.png) <!-- src: https://i.imgur.com/17blMbJ.png -->

These new animations can be used with the gun guide: [Custom gun guide](https://mod.io/g/pavlov/r/custom-gun-guide)

To remove the gun preview asset to try other weapons, right click on the "hand" bone and click "Remove All Attached Assets":

![image](images/custom-hand-sequence-guide/6c54603aec.png) <!-- src: https://i.imgur.com/B17R1e2.png -->
