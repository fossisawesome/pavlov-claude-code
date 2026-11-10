# How To make money saving

> Source: https://mod.io/g/pavlov/r/how-to-make-money-saving
> Author: su-sukana | Added: 2025-09-22 | Updated: 2025-10-02 | Views: 321 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 0 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Made this guide for dum people

---
(FOR MONEY SAVING YOU WILL NEED A COMMUNITY SERVER)
And you need basic logic bout ue5

First Open up your game logic (if you dont have one watch a tutorial from majerati)

Second Look on the left and hover functions and click override, then click on player joined server

Then Drag Off Players status and do break pavlov player status

Then off the player state do get player name

The drag off the arrow of the joined server and do load string from file

and then connect the file name to the get player name from earlier

then off that arrow make a branch and connect the condition to the return value of the load string

And then off the true pin to a set player cash and connect the integer pin to the string from load string from file and the player state from the break pavlov player status

off the false pin do set player cash and set that to the amount you want the player to start with.

Now right click anywhere you want and search up event on player left server

Off the player status pin do break pavlov player status and off the player state do get player name and off the cash pin drag off of it and do save string to file and connect the player name to the file name and allow overwrite
