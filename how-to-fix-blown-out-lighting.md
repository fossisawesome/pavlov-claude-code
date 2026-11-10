# How to fix blown out lighting / phantom lights

> Source: https://mod.io/g/pavlov/r/how-to-fix-blown-out-lighting
> Author: Juntistik99 | Added: 2024-04-14 | Updated: 2024-04-14 | Views: 402 | Comments: 0 | Tags: fix
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 5 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Strange lighting artifacts that can't be explained? Try to see if you're missing a UV channel!

---
When upgrading from an older version of the modkit you may find your lighting all blown out and nearly pure white. This may be related to a missing UV channel. You can check this by looking at the UV editor for your mesh.

 

Locate your mesh in the content browser, right click on it and select UV Editor

![image](https://cdn.discordapp.com/attachments/1141025829418180689/1229137135148208229/image.png?ex=662e9629&is=661c2129&hm=add52c7387dcf1726e510ac5f5cf98c1a088af020273aee2fde226e69021f349&)

Once you are in the UV editor, check the drop down labeled channels. Notice in this example UV channel 1 is missing.

![image](images/how-to-fix-blown-out-lighting/ac1bf82762.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/screenshot2024-04-14134533.png -->

 

Click on the channels button then add a channel, hit apply. 

![image](images/how-to-fix-blown-out-lighting/f82c4d2f42.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/screenshot2024-04-14134734.png -->

 

Check your UV channel drop down again, make sure there is now a Channel 1 and it's selected. 

![image](images/how-to-fix-blown-out-lighting/7ded14e861.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/screenshot2024-04-14134857.png -->

 

Use the AutoUV button to generate new UVs, for the method select XAtlas. 

![image](images/how-to-fix-blown-out-lighting/2479cc7dba.png) <!-- src: https://image.modcdn.io/members/5389/21041384/profile/screenshot2024-04-14135429.png -->

 

Hit Accept at the bottom.
