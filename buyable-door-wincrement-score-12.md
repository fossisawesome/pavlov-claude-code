# Buyable Door W/Increment Score

> Source: https://mod.io/g/pavlov/r/buyable-door-wincrement-score-12
> Author: Smallbogdan | Added: 2026-07-18 | Updated: 2026-07-18 | Views: 139 | Comments: 0 | Tags: dumb, Map Making, Upgrade
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 11 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This is for people who like slop RPs. GPPS = Get Pavlov Player Status

---
##### If you see any problems with them in game, please DM Smallbogdan on Discord for assistance.Step 1Add an new interactive box with text saying Buy and the value. After that, add 2 More Texts of the user/owner (should say none), and name the upper text at the very top Unowned.
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-17_165856872.png)
Should look like this!Make sure they are attached below your door mesh!
![image](https://image.modcdn.io/members/8147/35513005/profile/screenshot2026-07-17165932.png)
Step 2Create your important variables!Cost - integer - Will determine how much the door will costOwningPlayerstate- Player state (object reference) - Game determines if bought by player. SET TO REP-NOTIFYStep 3Go into your Owningplayerstate functionShould be StraightforwardStep 4Create the name/own system Copy this image right here to replicate yours
![image](https://image.modcdn.io/members/8147/35513005/profile/screenshot2026-07-17173003.png)
Connect the on rep into A branch, then add "Is valid (the one with a boolean)."Add your Playerstate variable to its object pin.Step 5Drag off the True branch, and get "set text"; the target is your "owned-unowned" text component.Drag off the value from Set Text, and get "Make literal Text", and name the empty space "Owned"Drag off the other exec pin from Set Text (Own) and place down Set Text (User/Username text component), whatever you named your text render.Your target should already be tickedFor Value, pull it and get To Text (String)In string - Get Player nameFor target get Owningplayerstate VariableShould look like this
![image](https://image.modcdn.io/members/8147/35513005/profile/screenshot2026-07-17183613.png)
Step 6Drag off the false Branch, and get "set text" the target is your "owned-unowned" text component.Drag off the value from Set Text, and get "Make literal Text", and name the empty space "Unowned"Drag off the other exec pin from Set Text, and get "Set Text (User text component again)."Drag off the value from Set Text, and get "Make literal Text", and name the empty space "None"
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_111116995.png)

##### The whole thing should look like this.WHEN FINISH COMPILE AND SAVE, AND RETURN TO EVENT GRAPH._______________________________________________________________________________Step 7Copy this exact image (too lazy to guide through)
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_111637244.png)
Do not put Owning playerstate into Get player Proxy (Just if the wires look confusing)ONCE FINISHED COMPILE AND SAVE!Step 8Right click on your purchase interact in your left outliner, and add both Client and server 
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_111930043.png)

![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_113526665.png)
Connect Your Server and client like this!Step 9 Drag off is not valid, and get Pavlov player status!Then connect Player State to Player State.
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_113628453.png)
Step 10Pull out the exec pin for GPPS and get Branch.Plug its condition into Succeeded Below GPPS.Drag off Player status score, and get Greater EqualGet your price variable (make sure you already have a price set)Place it into Greater equal to And drag off the variable and get multiplyPut -1 in the spare box
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_114405498.png)
Should look like this!Step 11Drag off true Branch and get branch again, connect its condition to the Boolean return value of Greater equal.Drag off true from the second branch, and get "Increment Player Score"The target for "Increment Player Score" will be Get game logic.Connect the player state to player status player state from GPPS.The score will go straight into the top-right return value of multiply.Step 12 (Final step)Drag off the other Exec Pin from Increment score, and Set OwningPlayerstate (Variable)Connect the Owning player state return pin into Player status player state. DO NOT PLUG THE VARIABLE IN JUST ITS RETURNGet the Set Owningplayerstate pin and get 'Change Door State"
![image](https://image.modcdn.io/members/8147/35513005/profile/image_2026-07-18_115523519.png)

##### PUT A CHECK IN THE STATECongrats your done.THIS IS A TEST DO NOT EXPECT MUCHCOMPILE AND SAVE
