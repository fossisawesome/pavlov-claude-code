# Wardrobe for push mode

> Source: https://mod.io/g/pavlov/r/wardrobe-for-push-mode
> Author: shadowmanxr | Added: 2023-09-20 | Updated: 2023-10-30 | Views: 341 | Comments: 8 | Tags: mod, push, skin
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 2 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A method is shown on how to make sure that when you select a specific locker, a specific skin is given. ModKit 2.0

---
Work PC and Shack version

UE 5.1.1

ModKit 2.0

##### Link to blueprint:

https://drive.google.com/file/d/13Q61WkiA4Fi5PAmHL5ugefsoQKzdcaux/view?usp=drive_link

#### How to use?

1. Copy the blueprint to your project folder.
2. In the game logic, specify this proxy player or copy this logic into your script.
3. Everything is ready

### Inside the script

This logic should be located in the Player Proxy blueprint

1. Checking whether the player has chosen a locker

![image](https://image.modcdn.io/members/af45/26066947/profilewardrobe/screenshot2023-09-21000218.png)

2. We install the skin according to the label installed on the locker. The mark is the amount of armor that is given to the player

![image](https://image.modcdn.io/members/af45/26066947/profilewardrobe/screenshot2023-09-21000334.png)

3. In the loadout object, set the amount of armor accordingly.


---

## Comments (mod.io API, 8)

- **BritishColonist** (2023-11-06): previously i had done it by getting the id of the class, then setting a skin to any class with that name. tho this was back in ue4 and was done in the push loadout proxy.  only downside is i couldnt have classes on both team with the same name, so one red team i may have "sniper", but blue team "sniper." this is what kenithh showed me, not sure if hes changed his method.
- **shadowmanxr** (2023-11-06): Yes, I haven’t found any other way to install a skin for a class. Do you have another way?
- **BritishColonist** (2023-11-06): i dont understand, are you saying i have to set the armour value to the same as the class i want this skin to apply to?? this seems like a odd way of doing this
- **shadowmanxr** (2023-11-06): In the blueprint itself, you need to change the armor value and the name of the skin. Not very comfortable)
- **BritishColonist** (2023-11-05): im confused on how to actually use this, like where do i put the id of the class to assign the skins to?
- **BritishColonist** (2023-09-27): aaaah ok
- **shadowmanxr** (2023-09-22): So that after selecting a locker with weapons, in push mode, a certain skin is installed. For example, for a Sturmikov there is a regular skin, for a medic it’s already different, for a commander it’s even different.
- **BritishColonist** (2023-09-21): what is meant for? the BP that is
