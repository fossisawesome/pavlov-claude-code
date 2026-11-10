# How to make a basic menu for beginners!!! NOT FINISHED I TRIED HIDING

> Source: https://mod.io/g/pavlov/r/how-to-make-a-basic-menu-for-beginners
> Author: senba | Added: 2025-09-16 | Updated: 2025-09-17 | Views: 948 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 19 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: How to make a basic menu for beginners because masterhyps is outdated

---
### STARTING THINGS, YOU WILL NEED FOR SUCCESS!!!

***THE TINIEST BIT OF COMMON SENSE AND GOOD EYES! :)
***

READ BELOW TO START MAKING YOUR SUPER COOL MENU!
                                           VVV

-Starting off you this is what you will need;
-A folder, name it whatever you want i would recommend putting menu/widget doesn't matter.
-After organizing, right click in the empty area and go down to user interface, Widget Blueprint.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-15235830.png)

-Once you click Widget Blueprint a pop up will show, all you need to do is click **User Widget.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16000546.png)

**

### The start of MAKING YOUR MENU!

-With your widget in your editor, you can start customizing.
-Open your widget and place down a canvas panel. *(This is a key step or your widget will not show in game)*
-Do NOT change the size of the canvas panel, make sure to keep it at what it was when you placed it.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16001609.png)

***THIS IS WHAT YOUR WIDGET SHOULD LOOK LIKE, IF IT DOESN'T YOU MESSED SOMETHING UP!!***

-If you have this, then your ready for designing your widget.
-Place an image in your canvas panel and set the anchor to the middle one.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16002601.png)

-After setting the anchor, copy these settings.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16002538.png)

-If you have this in your widget

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16002826.png)

-You have everything correct.
-In *"Tint" *you can select the color I would recommend a grayish blackish color for best results, in game.

### CUSTOMIZING THE MENU

#### Rounded Edges

-If you want rounded edges in your widget (Such as the thumbnail)
-Here's what you need to do!
-Under the brush tab, drop down *Draw As *and select **Rounded Box.**
-You might notice your "Box" might look a little ovaly, sort of like a circle.
-How ever their is an easy fix for this, under *"Outline Settings"* you should see a little drop down that says ***Rounding Typ**e**, ***drop that down and select ***Fixed Radius.***
-Once you have that done, you will see that "That did nothing" thats where your wrong under ***O******u******tline Settings ***you can change the corner radius.
-You can change your corner radius to whatever and experiment what ever looks good for what your going for.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16144746.png)

If you have done everything right so far, this is what your menu should look like!

-If you want your menus edges to have colors here's what you need to do.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16145141.png)

-Set the **Use Brush Transparency **to ✅ and but the width to what ever you want I would recommend 20 or 30.
-You can change the color by clicking **Outline** and changing the color.

### Coding the menu :)

-If you take a glance at the thumbnail you realize it says your name, your health, your ping, and your money. (THE MONEY PART IS IF YOU USE A SCORE BASED MONEY SYSTEM NOT PLAYER INFO) this part of the menu is pretty easy as I will be copy and pasting things for u to copy and paste in to your code but in order to do this i will need you to do a couple of things.
- 1. Place 4 ***"Text"*** and place them were you think would look good, if done correctly, it should look like this.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16160032.png)

-I just quickly made this, but the things that selected in green are the 4 I was talking about, i just made my menu fancy because I want it to look good if you want to copy what i did, i don't care copy it.
-With the 4 text that u placed down, for me the things i highlighted in green are my 4 text and you wanna make sure "Is Variable" is ✅

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16162214.png)

Make sure "Is Variable" is checked for ALL 4 text for this to work, also you should probably name your text 

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16163146.png)

#### The actual coding part which is easy!https://blueprintue.com/blueprint/3ia4p684/Go to this link and copy this code into your graph
![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16164149.png)
It will give you compile errors because you don't have the variables I used, but if you followed it correctly
![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16164724.png)
You should have these and connect them to the proper target
![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16165030.png)
Connect the target to the proper variable, this is why i made you name them earlier.
![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16165112.png)

### Making the actor

-Make an actor inside of your folder name it "Menu" or whatever works for you.
-Inside the event graph in the actor
https://blueprintue.com/blueprint/3qcrb0s1/
-Copy and paste this code in to the actors event graph (DONT CHANGE ANYTHING)
-After doing this head over to the viewport, in your components tab **"+Add" *Widget 

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16175229.png)

***-Once you place this down, click the widget in your viewport and head over to the details tab.
-In your details tab copy and paste this into your transform
Location: (X=32.103262,Y=-2.999999,Z=15.636062)
Rotation: (Pitch=50.000000,Yaw=180.000000,Roll=0.000000)
Scale: (X=0.040000,Y=0.040000,Z=0.040000)

-In the widget class you want to put the name of your widget into the widget in the actor (For example my widget is called WB_MenuForGuide so in the widget class I would put WB_MenuForGuide)
![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16181053.png)

-In the **User Interface **tab set the draw size to (1920,1080)
if everything is right. your only half way done with the guide and it should look like this.

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16181450.png)

(OPTIONAL) if you want the menu to curve in game

![image](https://image.modcdn.io/members/8cf6/39108360/profile/screenshot2025-09-16181627.png)

Change the Geometry Mode to Cylinder and you can mess with the Arc depends on what you like its your menu!

### Making Buttons! (OPTIONAL)

-Head over to your widget not your widget actor but your actual widget.
-And add a button to your widget just how you would add an image or the canvas panel.
-Customize the button how ever you would like, what ever fits your theme of your menu.

to be continued!

### The interactor for your buttons (OPTIONAL)

 

### Player proxy and Game logic for this to actually show up on your hands.

**This is a very tricky part so if you need help ping i_am_point in the Pavlov Discord #ue5-help**
-You will be copying code from a link but, theres a lot of variables
