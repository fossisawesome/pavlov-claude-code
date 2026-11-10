# Money System: Achievement System

> Source: https://mod.io/g/pavlov/r/money-system-achievement-system
> Author: papercutpavv | Added: 2026-07-08 | Updated: 2026-07-08 | Views: 118 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 4 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This achievement is only when the player has a certain amount of money, when they can claim the achievement to get more money

---
#### Optional: This is to make it so the background of the button changes color when the player has reached the required money for the achievement
![image](https://image.modcdn.io/members/126c/39023825/profile/screenshot2026-07-08152247.png)

#### Step 1: Custom Events Player Info 
![image](https://image.modcdn.io/members/126c/39023825/profile/screenshot2026-07-08153120.png)
You need to create a custom event by right clicking in the graph and searching up custom event. You will see Add Custom Event...1. Make it run on server2. Add two inputs, one being player state and another being an integer3. Drag off of yoru custom event and do " Set Player Cash "4. Plug player state into player state and amount into cash amount5. Target of set player cash is " get game logic "

#### Once step 1 is done, you may go back to yoru userwidget/menu and follow these steps.
![image](https://image.modcdn.io/members/126c/39023825/profile/screenshot2026-07-08153530.png)
(On Pressed (moneybags) is your userwidget button you made in designer)This part is only to make sure the players money is equal to 30k or has more than 30k

#### ![image](https://image.modcdn.io/members/126c/39023825/profile/screenshot2026-07-08153734.png)
You will be casting to your player info/whatever you named it and then dragging off and searching up you custom event that you made in yoru player info.

#### If you followed all the steps correctly, you have finished.
