# 4.21 to 5.1.1 Upgrade Guide

> Source: https://mod.io/g/pavlov/r/421-to-511-upgrade-guide
> Author: Juntistik99 | Added: 2023-02-19 | Updated: 2023-02-19 | Views: 3341 | Comments: 13 | Tags: DNU_PINNED, General Guide, Porting, Upgrade
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 9 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: How to move your previous map to Unreal Engine 5.1.1

---
1.Download unreal engine 5.1.1 (4.21 is not required to be installed to update old projects)

 

2.Unzip Modkit to a new folder

 

3.Copy your old 4.21 **content folder** over the new 5.1.1 **content folder** (using windows file explorer). Ignore all other folders.

![image](images/421-to-511-upgrade-guide/1d8cd811a2.png) <!-- src: https://i.imgur.com/aFMnDrf.png -->

4.Launch the project, Go to Window->Pavlov Workshop Login to mod.io on the “Account” Tab of the Pavlov Workshop window with your email address and press “send”.

![image](images/421-to-511-upgrade-guide/730dd47116.png) <!-- src: https://i.imgur.com/lAiHzJY.png -->

![image](images/421-to-511-upgrade-guide/618f27310d.png) <!-- src: https://i.imgur.com/2NlZAxV.png -->

5.Paste the auth code from your email into the Auth code field, and Login

![image](images/421-to-511-upgrade-guide/8e006e94f0.png) <!-- src: https://i.imgur.com/YQGqWZr.png -->

6.Click the “Create Mod” tab and name your mod/map, and include a summary. If you want to add a custom image check the image requirements on the tooltip.

7.Click “Create Mod”

8.Take your UGC folder and “move” it into the “Plugins/UGCXXXXX Content” folder.

![image](images/421-to-511-upgrade-guide/e33b0508d4.png) <!-- src: https://i.imgur.com/S0EXLIU.png -->

9.Right click the custom maps folder and fix up redirectors

![image](images/421-to-511-upgrade-guide/023467a6ab.png) <!-- src: https://i.imgur.com/nzV7U2X.png -->

10.Set all of your settings in the newly created definition file that was created in the “Plugins/UGCXXXXX Content” Folder. Link the desired map, name it and set your game modes.

 

11.Change the name of your old UGC folder to something else. Nested UGC folders is bad practice and might technically work but will likely cause issues due to path length.

 

12.Check your lightmass settings,it is recommended to select “Build all Levels” to rebuild using unreal 5.1.

![image](images/421-to-511-upgrade-guide/0487645367.png) <!-- src: https://i.imgur.com/aEKsLNq.png -->

13. REPLACE OLD DEFINITION FILE. You can delete your original and select to replace with the new one, or manually replace it in every instance in your project and pavlov logic in the scene.

![image](images/421-to-511-upgrade-guide/1813d1d152.png) <!-- src: https://i.imgur.com/9LTmK8r.png -->

14.  Select the appropriate tags for game modes. They will matter now, and be filtered in-game if not properly selected. Do not select game modes that if your map is not set up for it them such as Prop Hunt or Push.

![image](images/421-to-511-upgrade-guide/497aeccc81.png) <!-- src: https://i.imgur.com/uUhA3Ja.png -->

15.Fix up redirectors in your content folder for your new Mod.io UGC folder

16.Stage or upload to mod.io - Under the Pavlov Workshop window, select the “Upload Mod” tab and select the UGC number from the dropdown. Set your change notes, and select windows for PC and android for Shack.

17.Click stage to stage or upload to upload.


---

## Comments (mod.io API, 13)

- **Hushey** (2023-06-26): gaming
- **orionplays77** (2023-06-21): where is the modkit and how do I download it?
- **SoggyMicrowaveNugget** (2023-06-21): I'm sure all of the Workshop users will love going through all 17 of these steps for each of their mods to make their map playable to the ¹³ ʸᵉᵃʳ ᵒˡᵈ Player-base you've invited in to the community. I see no downside to abandoning workshop, won't harm the ᵖˡᵃʸˢᵗᵃᵗᶦᵒⁿ⁵ community at all.
- **MacAndMayo** (2023-06-16): Could you provide a guide that tells users how to install mods from mod.io?
- **Ernest326** (2023-06-16): ong
- **Zetch_** (2023-02-23): There's totally nothing that can go wrong. right... Right?
- **VoidVibrato** (2023-02-21): Very nice, I am looking forward to playing mods on the latest version of this Virtual Reality Computer Game known as Pavlov VR.
- **Ernest326** (2023-06-16): fake
- **no-** (2023-02-20): real
- **MichelCats** (2023-02-20): Was the virus scanner. So if anyone els got the same problem, that’s it
- **MichelCats** (2023-02-19): Stuck in step 4: When I press 'Sent" after typing my email address nothing happens. Got a mod.io account with the same email as what I typed in the mod kit for an authentic code.  (also tried my other email address but still the same) Any tips on why this happens and am I the only one with this problem?
- **inactive9948** (2023-02-19): fr
- **Skeedard** (2023-02-19): Truly quite unbelievable
