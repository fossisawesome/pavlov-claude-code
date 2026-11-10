# Modkit version upgrade best practices (Post 5.1.1)

> Source: https://mod.io/g/pavlov/r/modkit-version-upgrade-best-practices-post-511
> Author: Juntistik99 | Added: 2023-02-22 | Updated: 2024-05-14 | Views: 1614 | Comments: 0 | Tags: General Guide, Upgrade
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 0 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Best way to update a project already in 5.1.1

---
This guide is for folks who are **already using the Unreal 5.1.1 **version of the modkit and need to update their project with the latest changes and fixes with future releases. [If you are trying to upgrade your modkit from Unreal 4.21, please use this guide instead.](https://mod.io/g/pavlov/r/421-to-511-upgrade-guide)

 

#### Mark Dey EZPZ Method™

- Extract the new modkit.

- Go to your old modkits Plugin folder. **Delete the Saved folders inside your UGCXXXX folders' **

- Copy the UGCXXXX folders AFTER you have deleted your Saved folder inside it.

- paste them in your **new** extracted modkit plugin folder

 

#### I'm grumpy and set in my old ways method™

If you want to do hard mode. You can copy the modkit update over the top of your existing folder directory like you may have previously done in the old modkit, but there are extra steps involved with this method. **its not as recommended anymore**, but if you do choose this path, DELETE the folder YOURPROJECT/Intermediate/ScriptModules

Other potential unforseeen issues may arise so it is definitely recommended to use the Mark Dey EZPZ Method™ (patent pending), however if you know what you are doing you can use this way to save time because you will not have to recook or repackage.
