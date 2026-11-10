# Economy/Money System

> Source: https://mod.io/g/pavlov/r/money-system
> Author: hawkmod | Added: 2025-10-30 | Updated: 2025-10-30 | Views: 507 | Comments: 0 | Tags: currency, money, roleplay, rp
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 3 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: this is how you can make a money/economy system for RP maps

---
### Economy / Money system

mainly for roleplay maps

 

**1. Make the money variable in your Player Info**

- Navigate to your PlayerInfo Blueprint

- In the left hand panel add a new Variable called Money and have it be either an Integer or a Float

-
![image](https://i.imgur.com/utPhR66.png)

- **(IMPORTANT)** Set the Replication of the veriable to Replicated

-
![image](https://i.imgur.com/603ifib.png)

** 2. Set the Default Money**

- Edit your Game Logic Blueprint

- **(IMPORTANT) **The following blueprint wont work if you copy it in because it needs to cast the PlayerInfo to **YOUR** player info class

- Copy the blueprint provided and put in your Cast to PlayerInfo

- https://blueprintue.com/blueprint/x4ch5kvc/

-
![image](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExZHRzNTY2M3puaGkwcGJrdG1kaHd6OW5tMWNqejZvN3B1d2duZnBnayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/IGkvSif5V0z9m76GVm/giphy.gif)

- ^^ manuscript: Cast the player info to your player info class, then set the money using that

The same player info cast can be used to get the money on both the server and the client and set the money on the server!

### ASK IN COMMENTS SO I CAN UPDATE GUIDE
