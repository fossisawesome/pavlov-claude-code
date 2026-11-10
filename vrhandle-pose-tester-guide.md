# VRHandle tester guide

> Source: https://mod.io/g/pavlov/r/vrhandle-pose-tester-guide
> Author: Brav_Soldat | Added: 2023-05-04 | Updated: 2023-05-04 | Views: 376 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 10 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Follow this guide to get VRHandle hand poses looking good.

---
After creating a Custom Gun or VRItem, hand poses on their VRRHandles can be hard to get looking right. This guide should make that process easier.

You also need to make sure you followed the previous guide: [Custom gun guide](https://mod.io/g/pavlov/r/custom-gun-guide)

 

**Getting started**

Navigate to "CustomMapTools/PavExamples/Guns/HandleTester" and drag "BP_HandleTester" into the level:

![image](images/vrhandle-pose-tester-guide/ae569944a9.png) <!-- src: https://i.imgur.com/gSzzxGg.png -->

Then navigate to the custom gun/item in your UGC and drag it into the level as well:

![image](images/vrhandle-pose-tester-guide/3a10eed5bd.png) <!-- src: https://i.imgur.com/sLZA8XB.png -->

Click on BP_HandleTester and look at the details on the right:

![image](images/vrhandle-pose-tester-guide/91658255a1.png) <!-- src: https://i.imgur.com/R7z6Ajy.png -->

![image](images/vrhandle-pose-tester-guide/68839027a1.png) <!-- src: https://i.imgur.com/zmp0mY0.png -->

Click on the eyedropper to the right of "Gun Ref" and then click on your weapon in the level:

![image](images/vrhandle-pose-tester-guide/6d565577d2.png) <!-- src: https://i.imgur.com/e2LBwlN.png -->

The "Gun Ref" variable should update.

 

**Testing**

Change the Hand Type to the setting you want previewed:

![image](images/vrhandle-pose-tester-guide/f7532b1778.png) <!-- src: https://i.imgur.com/KSibJZ2.png -->

"Socket Name" should already be set to the correct name unless you used a different socket name for the charging handle in the guns skeletal asset, if so, update it. (If a VRItem, move the BP_HandleTester bp to the area the VRHandle is)

Next we want to pick the hand sequence we want to use:

![image](images/vrhandle-pose-tester-guide/4bd2951f5d.png) <!-- src: https://i.imgur.com/7hN17Xu.png -->

There's a lot to choose from or you can make your own following this guide: [Custom hand sequence guide](https://mod.io/g/pavlov/r/custom-hand-sequence-guide)

Now adjust the "Offset" and "Rotation Offset" variables until the hand is positioned how you like:

![image](images/vrhandle-pose-tester-guide/b6fa6dbaf4.png) <!-- src: https://i.imgur.com/k2xBcnX.png -->

Once you're happy, open your Custom Gun/ VRItem blueprint.

Over on the left, under the components list, click on "ReloadHandle" (or the name you gave the VRHandle) then over on the right under the details panel, scroll down until you find "Sequence Right Hand":

![image](images/vrhandle-pose-tester-guide/cd7f238382.png) <!-- src: https://i.imgur.com/4Lkfi82.png -->

Set the "Sequence" to the same one you chose earlier, and copy the "Offset" and "Rotation Offset" values into here.

Back in BP_HandleTester, you can click "Left Handed" to do the other hand. Don't forget to set "Sequence Left Hand" once you find the correct values!

![image](images/vrhandle-pose-tester-guide/245e5d3be2.png) <!-- src: https://i.imgur.com/lRyuZce.png -->
