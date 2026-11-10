# How to make basic custom money system!

> Source: https://mod.io/g/pavlov/r/how-to-make-basic-custom-money-system
> Author: Fishy! | Added: 2024-09-10 | Updated: 2024-09-25 | Views: 940 | Comments: 1 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 6 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: --THIS DOES NOT TEACH HOW TO CODE-- Will teach the basic on how to create a custom money system for whatever you want. I will also show how to change the money you have!

---
So first, I want you to create or use a custom Player Info in your UGC. Add this Player Info into your Game logic.

![image](https://image.modcdn.io/members/2660/8392937/profile/screenshot2024-09-09204729.png)

In your Player Info, then add a variable.

![image](https://image.modcdn.io/members/2660/8392937/profile/screenshot2024-09-09204749.png)

Set the variable to integer.

To get the variable and edit it inside a Blueprint, get the player's Player State.

![image](https://image.modcdn.io/members/2660/8392937/profile/screenshot2024-09-09205030.png)

Off the player state, use the "Get Player Info".

![image](https://image.modcdn.io/members/2660/8392937/profile/screenshot2024-09-09205139.png)

Off Get Player Info, add a cast to your Player Info and use the Get Player Info as the
![image](https://image.modcdn.io/members/2660/8392937/profile/screenshot2024-09-09205232.png)
.

Off the target in the cast, you can get/set the money your player has.

Example;

![image](https://image.modcdn.io/members/2660/8392937/profile/screenshot2024-09-09205452.png)

Hope this was helpful, if I am missing anything or have any feedback/questions, please leave a comment!
Remember that you can also use Player Info variables for other things! This is just for a money system, but that doesn't mean you can't make anything else!


---

## Comments (mod.io API, 1)

- **CHICK-FiI-A** (2024-09-10): sigma
