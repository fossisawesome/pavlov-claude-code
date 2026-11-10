# Disable Radio (in your custom map)

> Source: https://mod.io/g/pavlov/r/disable-radio
> Author: Gary_Pavlov | Added: 2025-07-30 | Updated: 2025-07-30 | Views: 291 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 6 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: What to put in your player info to delete squeakers

---
### This is a guide on effectively disabling the radio in your custom maps.

---------------------------------

#### •Version One:

1. The first thing you need to do is go into your map's PlayerInfo

![image](https://image.modcdn.io/members/9692/12941038/profile/screenshot2025-07-29235127.png)

2. The next thing you want to do is paste these nodes into the PlayerInfo's event graph (open link below)

[Link to the copy paste right here](https://blueprintue.com/blueprint/fi3olph9/)

![image](https://image.modcdn.io/members/9692/12941038/profile/screenshot2025-07-29235608.png)

3. next you want to connect the **Set Radio Channel** to **Event Begin Play **as so:

![image](https://image.modcdn.io/members/9692/12941038/profile/screenshot2025-07-30000004.png)

#### •Version Two (admin channel):

If you want to put admins or police on a certain radio, you can follow this guide

1. Copy the code from the link below and paste the variable into your player info, and fill the array with your staff's usernames.

[Code To Copy Paste](https://pastes.io/pavlov-staff-names-array)

![image](https://image.modcdn.io/members/9692/12941038/profile/screenshot2025-07-30000814.png)

2. Like the first version, paste these nodes into your PlayerInfo:

[Code To Copy Paste](https://blueprintue.com/blueprint/cf5sggu6/)

![image](https://image.modcdn.io/members/9692/12941038/profile/screenshot2025-07-30001306.png)

3. And again, attach it to **Event Begin Play**

![image](https://image.modcdn.io/members/9692/12941038/profile/screenshot2025-07-30001420.png)

And that is the end of the guide, radio channel 2 is also excluded from the random integer in range node so you can use it for Police if you so desire.
