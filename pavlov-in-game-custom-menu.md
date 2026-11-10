# Pavlov In-Game Custom Menu (Updated)

> Source: https://mod.io/g/pavlov/r/pavlov-in-game-custom-menu
> Author: MasterHyp | Added: 2024-10-13 | Updated: 2025-02-16 | Views: 2049 | Comments: 0 | Tags: Custom Menu
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 0 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Pavlov In Game Custom Menu, Using PlayerInfo, Optimized

---
**How to Install the Menu:**

1. Download the RAR file containing the menu's blueprints: [PavlovVR_InGameCustomMenuV2.rar](https://github.com/masterhyp/PavlovVR/raw/refs/heads/main/PavlovVR_InGameCustomMenuV2.rar)
2. Close Unreal Engine.
3. Open the downloaded RAR file.
4. Open your Modkit folder.
5. Drag the *Content* folder from the RAR file into your Modkit folder.

*You have now successfully installed the menu into your Modkit.*

**Where to Find It, and How to Move It to Your UGC Plugin:**

1. Open your Unreal Engine Modkit project.
2. In the **All/Content** directory, locate *PavlovVR_InGameCustomMenu*.
3. Open each Blueprint and Widget, then click **Compile** and **Save** to ensure they work properly.
4. Drag the *PavlovVR_InGameCustomMenu* folder into your *UGCXXXXXXX* folder under **Plugins**, and choose **Move Files** (not Copy).
5. Right-click the moved folder in your UGC plugin and select **Fix Redirectors**.
6. Repeat step 3 after moving the files to your UGC plugin folder.

*You have now successfully moved the menu content into your UGC folder.*

**Placing the Custom GameLogic:**

- You do not need to use the level included in the menu files.
- In your level, place a single *Custom GameLogic* actor (only one per level).
- Select the *GameLogic* actor to set up your definition.
- Drag the *PlayerInfo* (included with the menu files) below your definition where it says *Pavlov Player Info*.

**Additional Resources:**
1. Wiki: [Replacing the Scoreboard](https://pavlovwiki.com/index.php/Replacing_the_scoreboard)
2. Video Tutorial: https://www.youtube.com/watch?v=WT68dJPoR4E

If you need additional help, mention **@010** in Pavlov's main Discord server.
