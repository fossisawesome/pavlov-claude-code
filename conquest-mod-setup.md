# Conquest Mod Setup

> Source: https://mod.io/g/pavlov/r/conquest-mod-setup
> Author: Brav_Soldat | Added: 2025-01-20 | Updated: 2025-01-25 | Views: 284 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 9 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A rundown of the settings required for the Conquest mod to work.

---
The Conquest Mod relies heavily on the Push mode, which handles most of the logic. This mod mainly spawns custom objectives in place and overrides the Push spawning logic. 

I designed it to be simple to setup, and use what is already available in the modkit. That being said, for this mod, we use the "BP_PushCapArea" located at CustomMapTools/Blueprints/Push/CapAreaObjective for objective placement.

It is best to use the push time adjuster mod with this mod: [Push Time Mod](https://mod.io/g/pavlov/m/mod-push-time-adjuster-30-min)

 

Rules to follow:

Loadout rooms should be near the play area, override their location (pushsettings bp) and find a good spot.

Each cap area **must** have its own objective id, none can be shared.

The total number of cap areas needed, is however many objectives you want + 2. For example, if I want 3 objectives (A, B, C) the total amount I would need in my level would be 3 + 2 which is 5. The two "extra" objectives, are the bases for each team which are **not** capable.

There are only 6 letters to choose from so technically the max amount of cappable objectives is 6. Team bases are excluded from this because they get their own unique icons. (They can be set to "A")

Objective 0 will **always** be team 0's base, the last objective will always be team 1's base. For example, earlier my total was 3 + 2 which is 5, that means my objective ids would be 0, 1, 2, 3, and 4. Objective id 0 would be team 0's base, and objective id 4 would be team 1's base. This will obviously change based on the amount of objectives in the level so keep that in mind.

Player spawns are setup almost exactly the same way as push, every cap area needs spawns for both teams. There is an option for fallback spawns which I will explain further down.

 

Objective setup:

![image](images/conquest-mod-setup/05824046f9.png) <!-- src: https://i.imgur.com/4m5DNSQ.png -->

Tick Amount: How many points are taken/ added to the objective per second (100/ **10** would be 10 seconds, 100/ **5** would be 20 seconds, 100/ **1** would be 100 seconds, etc)

Cap in Vehicle: If the objective can be captured while in a vehicle (obviously)

Objective Id: Unique value each cap area gets (no duplicates)

Objective Marker: Letter icon the cap area uses (Home bases are excluded since they use their own icon)

 

Objective Tags:

In the level, adding actor tags to each cap area bp allows the mapper to change some extra settings.

Tag index **0** and **1** is used for setting up factions, so that the conquest flag better fits the teams skin. The factions are built into the mod with their own id:

![image](images/conquest-mod-setup/7d15104caa.png) <!-- src: https://i.imgur.com/uihvGXj.png -->

An example of using said tags:

![image](images/conquest-mod-setup/8f4e3454aa.png) <!-- src: https://i.imgur.com/F1fivwG.png -->

So team **0 (blue)** would be US, and team 1** (red)** would be MEC

If **no** faction is specified in index 0 and 1, then the flag will be **solid blue or red**.

The "taken0" tag in the image means the objective will start off in team 0's possession. Keep in mind that conquest bleeds tickets if one team owns more flags than the other, so if one team starts with a flag, the other team should as well. In this case, another objective should have the "taken1" tag.

Some other optional tags are "hide" (hides the ring mesh for the objective) and "noflag" (hides the flag and flagpole) 

Here's what that would look like:

![image](images/conquest-mod-setup/50b146baae.png) <!-- src: https://i.imgur.com/gana6FM.png -->

There would be no factions set here, so add those two first, then these tags if needed*

The last tag is special and has to do with spawns: "radius:X"

![image](images/conquest-mod-setup/d544bcc402.png) <!-- src: https://i.imgur.com/r3s1JSF.png -->

The value in the radius tag determines the distance for fallback spawns. For example, players that **own** the objective, can spawn at spawns that are **less than** the distance specified from the flag (1400 here) If an enemy is taking the objective, the owning player will spawn at spawns that are **greater than or equal** to 1400 units from the flag.

![image](images/conquest-mod-setup/eb41ce6c04.png) <!-- src: https://i.imgur.com/qDxyINw.png -->

To get the distance needed, go into top down view:

![image](images/conquest-mod-setup/6d26e8f049.png) <!-- src: https://i.imgur.com/HMzgTwH.png -->

Then using the middle mouse button, click and drag to the spawn:

![image](images/conquest-mod-setup/4baebe8387.png) <!-- src: https://i.imgur.com/9MwVXcR.png -->

There's no need to get precise with it, as long as its roughly the right distance.

 

Vehicle spawns:

The last thing is vehicle spawning. Luckily its the exact same as normal push, just make sure **Only Spawn in Push** and the **Objective Id** matches up to the desired objective:

![image](images/conquest-mod-setup/fde943b230.png) <!-- src: https://i.imgur.com/ceEb6ae.png -->
