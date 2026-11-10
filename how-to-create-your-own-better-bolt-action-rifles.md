# How to create your own better bolt action rifles

> Source: https://mod.io/g/pavlov/r/how-to-create-your-own-better-bolt-action-rifles
> Author: BritishColonist | Added: 2026-08-09 | Updated: 2026-08-10 | Views: 109 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 18 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Title already sums it up

---
### This guide is for creating your own better bolt action rifles using my base provided in [this mod.](https://mod.io/g/pavlov/m/source-better-bolt-action-rifles#description)

#### This is not a beginners guide. I will be assuming you already know how to set up a custom gun and have a rigged mesh.

[Guide for creating custom guns](https://www.youtube.com/watch?v=nxw2cP2fICQ&t=1665s)

[Guide for rigging custom gun meshes](https://www.youtube.com/watch?v=J5u3qoJXzD0&t=499s)

 

### Mesh:

You can set up your mesh same you would with a normal bolt action rifle. I advise stealing the skeleton from the kar98 example and rigging to that. 

 

### Adding the plugin:

Before adding the source plugin, make sure your project has the pav examples in their normal location. if some stuff is missing, dependencies may break.

![image](images/how-to-create-your-own-better-bolt-action-rifles/5e31ea6efb.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09225706.png -->

 

 

Assuming your pav examples are all there, you can import the plugin by going to the workshop tab > download source plugin > and searching for "bolt"

![image](images/how-to-create-your-own-better-bolt-action-rifles/a94775ef4d.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09225636.png -->

You should now see the UGC with these inside. You can either leave the code where it is and set this mod as a dependency on your mod, or move the code into your own UGC

![image](images/how-to-create-your-own-better-bolt-action-rifles/c99f77c525.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09225940.png -->

 

 

 

### Creating your own:

####

#### Invisible Grip:

The better bolt actions use an invisible grip to change the two hand grip when holding the bullets down. its important you create your own ID for your mods invisible grip. 

Open up the base (Gun_BetterBoltActions_Base) and find the bit of code shown in the screenshot below. Edit the ID in the array to your own one.

![image](images/how-to-create-your-own-better-bolt-action-rifles/118e71f36f.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09230342.png -->

Then in your mod initialiser, add the invisible grip to the list and give it the same ID you referenced in the base

![image](images/how-to-create-your-own-better-bolt-action-rifles/73fcfb44ca.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09230804.png -->

####

#### Gun BPs:

You will need to create a child BP of the base, as well as a child of the single mag and full mag. 
Clip ejected base can be duplicated, as it doesnt need to be a child BP.

![image](images/how-to-create-your-own-better-bolt-action-rifles/ec0ab1d6c5.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/image.png -->

![image](images/how-to-create-your-own-better-bolt-action-rifles/2819ebdec1.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09231841.png -->

 

#### Ammo Stuff

The better bolt action rifles use two seperate magazines. one for full stripper and one for a single bullet. For the most part you can set these up the same you would normally. swap out the meshes for your own and set the right ammo count. 

 

Full stripper clip magazine:

![image](images/how-to-create-your-own-better-bolt-action-rifles/30cab38b1d.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09233003.png -->

![image](images/how-to-create-your-own-better-bolt-action-rifles/1831d7cd54.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09233028.png -->

 

Single bullet mag magazine:

![image](images/how-to-create-your-own-better-bolt-action-rifles/33f88b20dc.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-10161923.png -->

![image](images/how-to-create-your-own-better-bolt-action-rifles/b3765f92d5.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-10161950.png -->

make sure you swap out the mesh in the rifle clip ejected BP: 

![image](images/how-to-create-your-own-better-bolt-action-rifles/f36f4a5acc.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09233323.png -->

![image](images/how-to-create-your-own-better-bolt-action-rifles/a5e064da79.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09233336.png -->

 

 

#### Main Gun BP:

Set your class defaults as you would normally for a custom gun. If you are new to custom guns, [I have a tutorial here.](https://www.youtube.com/watch?v=nxw2cP2fICQ&t=1665s)

The only variables unique to the better bolt actions base which need editing are in the screenshot below. The other variables in this base don't need to be edited in your child BP. 

Most of these should be self explanatory. You need to make sure you set sounds and the bullet meshes here as well as in the normal place for custom guns. This is because they are referenced in the normal Kar98 example, which this base is a modified version of. I decided to turn them into variables so its easier to edit them in child BPs.

![image](images/how-to-create-your-own-better-bolt-action-rifles/c312881ed4.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-09234724.png -->

**Mad minute** - if ticked, you can pull trigger with A button if bolt is gripped by right hand.

**rifle uses striper clips **- If unticked, will disable the stripper clip interactions added - no clip will become visible after inserting a full mag.  

If you don want your rifle to alternative between two magazines, you can set both variables to the same magazine BP. This can be useful for guns that have an En bloc style clip.

Make sure to align your stripper clip with the gun mesh in the viewport:

![image](images/how-to-create-your-own-better-bolt-action-rifles/c2d1da5050.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-10163146.png -->

 

 

### Additional information:

I have included some additional code for rifles with an En bloc style clip. you can use this code in child BPs. 
If you are creating an en bloc style rifle, make sure the VRMagazineSlot has "allow refill" unticked, and "cock enabled" ticked
Also make sure "manual mag release" is ticked in class defaults.

![image](images/how-to-create-your-own-better-bolt-action-rifles/8c3d4622a6.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-10164458.png -->

![image](images/how-to-create-your-own-better-bolt-action-rifles/6d1c8ca20e.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-10164518.png -->

**Inputs:**
If you are unhappy with the current inputs, you can feel free to edit which buttons trigger which events:

![image](images/how-to-create-your-own-better-bolt-action-rifles/ecfcb6c57d.png) <!-- src: https://image.modcdn.io/members/a0d0/9271223/profile/screenshot2026-08-10165222.png -->

 

 

#### If you need additional support, feel free to leave a comment or ask me directly on [my discord server](https://discord.gg/96yUaXH8sv).
