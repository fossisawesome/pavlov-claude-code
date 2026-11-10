# How to create a ban function within your custom Pavlov menu!

> Source: https://mod.io/g/pavlov/r/how-to-create-a-ban-function-within-your-custom-pavlov-menu
> Author: RPMaker | Added: 2025-10-01 | Updated: 2025-10-07 | Views: 557 | Comments: 0 | Tags: Ban
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 5 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: This Guide will include how to make a ban system within your Pavlov custom menu!

---
**Guide : **

 

**Prerequisites Include :**

- A already made custom menu 

- Custom player info

 

***Widget Setup : ***

**1st : **Create a widget name it something like ban and kick.

**2nd : **Inside of the widget place your a border and resize it to your liking (Border not required for setup).

**3rd : **Inside of the same widget make 1 button and add text to the button and set the text to "**Ban**" after rename the button to fit its purpose and once those steps are done search in the widget search bar Combo box string now there are 2 types of combo boxes 
![image](https://image.modcdn.io/members/ef03/32634888/profile/screenshot2025-10-01030412.png)
 but make sure you put this one in widget. **THE 2 BUTTONS AND COMBO BOX STRING SHOULD BE VARIABLES.**

 

***Player Info Setup : ***

**1st : **Make a custom event and make it run on server and add a input to it and name it "PawnToBan" and make the variable type pawn. Once you have that it should look like this.

![image](https://image.modcdn.io/members/ef03/32634888/profile/screenshot2025-10-01030957.png)

**2nd : **Make a variable named Non-Bannable make it a string and change its type to array and put your oculus username in the array this will be able to prevent you from getting banned from the menu. I will now display what you need to add onto your custom event below.

![image](https://image.modcdn.io/members/ef03/32634888/profile/screenshot2025-10-01031354.png)

**3rd : **Because this is ban you want to make sure you have the **ban boolean on the kick player node checked** if not it will only kick the player and they will be able to join back.

 

***Widget Setup Part 2 :***** **

**1st : **Go back to the widget you made earlier in the guide.

**2nd : **Now you will need to click on your combo box string and scroll down in the** details panel** until you see** events** and click on **opening combo box string and **this will take you to the widgets blueprint and off the execution pin of the on opening of the combo box string you will want to add the code I have displayed below.

![image](https://image.modcdn.io/members/ef03/32634888/profile/screenshot2025-10-01033548.png)

This is what adds the players names and clears it.

**3rd :** Now go to the ban button and in the details panel scroll down until you see events and use either on click or pressed its users preference and choose one like before this will bring you to the widgets blueprint. I will display what you need below

![image](https://image.modcdn.io/members/ef03/32634888/profile/screenshot2025-10-01033809.png)

At the end the Ban player admin menu is just **calling your custom event from earlier**.

 

**That is all you are done!!**

 

***Thank you guys for following along my guide this is my first one I hope you enjoy!!***

 

PS. Leave a comment if there is anything you would like to see next!
