# Archery Modkit Guide

> Source: https://mod.io/g/pavlov/r/archery-modkit-guide
> Author: KodaTheProto | Added: 2024-09-24 | Updated: 2025-03-03 | Views: 505 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 3 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Learn How To Create Custom Bows, Arrows, And Quivers Using The Archery Modkit

---
### Initial Setup

#### You can skip this step if you know how to create a new mod, install a source plugin, and set a mod dependency.

First step is to create a new mod. Go into the editor and click "Window > Pavlov Workshop > Create Mod" then select "Mod", give it a name and a summary, then press create mod.

After creating your mod, go to the "Download Source Plugin" tab and find the "Archery Modkit" plugin and press "Add To Project" then restart the editor.

With that, you should have your own UGC folder and the modkit.

Now open your UGC folder and right click in the content browser, create a new blueprint and set the class to "Pavlov_ModInitializer".

After you create your mod initializer, open your definition and set your initializer.

Open your mod initializer and navigate to the event graph. Right click and search for "Event On Mod Initialized" and place it. Drag off of "Global Info" and search for "**?** Is Valid" and place it in, then connect the execute pins. Now click compile, then save it.

Finally, go to mod.io, click "My Content" and find the mod you just made, then click "Manage". Click "Dependencies" and search for "Archery Modkit", click it and press save.

### Creating A Custom Bow

Right click in the content browser, create a new blueprint and set the class to "VRI_BowBase", then name it whatever you want, and open it.

#### Changing The Bow Model

Go to the veiwport and click "Bow" in the components list. On the right side, find "Static Mesh" and set it to your new model.

Now in the components list, find "Top String Root" and "Bottom String Root" and adjust them to match the new model's string position

After adjusting the string root's position, in the components list, click "Resting Pos" and set its X and Y position to match the string root's position, then line its Z position to match the height where your arrow should go.

Finally, get the Z position of the "Resting Pos" component and add 5.5 to it then multiply that by -1, then under "Class Defaults" at the top, set the "Bow Pivot Offset"'s Z value to the result.

Remember to click compile and to save your blueprint after changing it.

#### Changing The Bow Properties

At the top, click "Class Defaults" then on the right, find "Bow Settings".

You will see a list of properties you can edit to change the bow's behavior.

**Quiver Class:
**This allows you to set the bow's default quiver when purchased.

**Max Arrow Speed:
**This affects the maximum velocity an arrow can leave the bow when fired.

**Power Requirement:
**This sets the minimum draw distance required to fire an arrow from your bow.

**Draw Length:
**This changes how far the string can be pulled back.

**String Interp Speed:
**This affects how fast the string moves to your hand's position, simulating tension.

**Bow Pivot Offset:
**This changes where the bow's rotation pivot will be when pulling the string.

**String Controller Offset:
**This changes where the string will rest relative to the player's hand when pulling it back.

**SFX:
**This is where you can change your bow's sound effects when doing certain actions.

Remember to click compile and to save your blueprint after changing it.

#### Adding The Bow To The Game

Navigate to your UGC and open your mod initializer.

In the event graph, drag off of your previous node and search for "Add Bow To List" and place it.

Connect the global info pin to "Event On Mod Initialized", then right click the "Bow Details" pin and select "Split Struct Pin".

Here you can define your bow's details.

**Bow Name:
**Set this to what you want your bow's item name to be, this is used for spawning it in.

**Bow Class:
**Set this to the bow class you just made.

**Purchasable:
**Set weather you want your bow to be purchasable in the buy menu or not.

**Team Id:
**Set which team you want to be able to purchase your bow.

**Cost:
**Set how much you want your bow to be purchased for.

**Buy Menu Image:
**Set this to the icon you want to display in the buy menu.

Finally, click compile and save your initializer.

#### Extras

If you want to add custom logic to your bow, here are a few events and variables you can use.

![image](images/archery-modkit-guide/f6fd301777.png) <!-- src: https://image.modcdn.io/members/0cde/25627877/profile/image.png -->

The events are all called on the server, so replication should be easy.

Remember to click compile and to save your blueprint after changing it.

### Creating A Custom Arrow

First we need to create a damage type, right click the content browser then create a new blueprint and set its class to "DamageType_Pavlov" then open it.

At the top click "Class Defaults" then on the right you will see some properties you can change. Set "Icon Lookup" to the name you want your arrow to be when spawning it in, then add "-gun" to the end of it.

When you are done tweaking your damage type's settings, click compile and save it. You can close this blueprint now.

Now right click in the content browser, create a new blueprint and set its class to "VRI_ArrowBase" then name it whatever you want. This will be the item, used when handling the arrow.

Create another blueprint and set its class to "BP_ArrowProjectileBase", name it whatever you want and open them both. This will be the projectile, used when loaded in the bow and fired.

#### Setting Up The Arrow Item

In the arrow item, click "Class Defaults" and look on the right under "Item Settings". Here you will see a few settings you can change. Set "Projectile Class" to your arrow projectile you just created.

After linking the projectile class to your arrow item, you can also set your arrow model here if you have a custom one, and set a custom icon.

If you changed the model of your arrow, navigate to the viewport and make sure the arrow's nock is at the back the box, otherwise you will need to adjust your model.

Now you can click compile and save your item blueprint, and navigate to your projectile blueprint.

#### Setting Up The Arrow Projectile

If you changed the model of your arrow item, navigate to the viewport and under the components list, click "Arrow" then on the right side, change your arrow's model to the one you set in your item.

Now at the top, click "Class Defaults" and look on the right side under "Arrow Settings". Here you will see a list of properties you can edit to change your arrows behavior.

**Damage Type:
**Set this to the damage type you created.

**Damage Amount
**This is how much damage the arrow will do when traveling at its maximum possible speed.

**Speed Scaling:
**This affects the maximum speed your arrow can travel when fired from a bow.

**Peircable Surfaces:
**This is a list of what surfaces your arrow can peirce, how fast your arrow needs to go to peirce it, and how deep the arrow will go when peirced.

**SFX:
**Here you can change your arrow's sound effects when it deflects off of a surface or peirces it.

Now you can click compile and save your blueprint.

#### Adding The Arrow To The Game

Navigate to your UGC and open your mod initializer.

In the event graph, drag off of your previous node and search for "Add Arrow To List" and place it.

Connect the global info pin to "Event On Mod Initialized", then right click the "Arrow Details" pin and select "Split Struct Pin".

Here you can define your arrow's details.

**Arrow Name:
**Set this to what you set "Icon Lookup" in your damage type minus the "-gun" part.

**Arrow Item Class:
**Set this to the arrow item you created.

**Arrow Kill Bonus:
**Set this to the amount of money the player gets on kill.

Finally, click compile and save your initializer.

#### Extras

If you want to add custom logic to your arrow, in the arrow item blueprint there is an event and variable you can use.

![image](images/archery-modkit-guide/21540e96e0.png) <!-- src: https://image.modcdn.io/members/0cde/25627877/profile/arrowitemdelegates.png -->

The event is called on the server, so replication should be easy.

Remember to click compile and to save your blueprint after changing it.

### Creating A Custom Quiver

Right click in the content browser then create a new blueprint and set its class to "VRI_QuiverBasic" then open it.

#### Changing The Quiver Model

Navigate to the viewport, then under the components list, click "Quiver". On the right side, find "Static Mesh" and change it to your new quiver model.

Now adjust the arrow meshes to make them fit in your quiver. You can add or remove as many arrows as you need.

After adjusting the arrows, make sure that your quiver is comfortably inside the "Pick Collision" and adjust it if needed. This is to make sure that you can grab an arrow from your quiver.

Remember to click compile and to save your blueprint after changing it.

#### Changing The Quiver Properties

At the top, click "Class Defaults" then on the right, find "Quiver Settings".

You will see a list of properties you can edit to change your quiver's behavior.

**Quiver Arrows:
**This is where you set the type of arrows and how many arrows are in your quiver.

**SFX:
**Here you can set the sound effect when someone takes an arrow from your quiver

#### Adding The Quiver To The Game

Navigate to your UGC and open your mod initializer.

In the event graph, drag off of your previous node and search for "Add Quiver To List" and place it.

Connect the global info pin to "Event On Mod Initialized", then right click the "Quiver Details" pin and select "Split Struct Pin".

Here you can define your quivers's details.

**Quiver Name:
**Set this to what you want your quiver's item name to be, this is used for spawning it in.

**Quiver Class:
**Set this to the quiver class you just made.

**Purchasable:
**Set weather you want your quiver to be purchasable in the buy menu or not.

**Team Id:
**Set which team you want to be able to purchase your quiver.

**Cost:
**Set how much you want your quiver to be purchased for.

**Buy Menu Image:
**Set this to the icon you want to display in the buy menu.

Finally, click compile and save your initializer.

#### Extras

If you want to add custom logic to your quiver, here are a few events and variables you can use.

![image](images/archery-modkit-guide/b4b57b802c.png) <!-- src: https://image.modcdn.io/members/0cde/25627877/profile/quiverdelegates.png -->

The events are called on the server, so replication should be easy.

Remember to click compile and to save your blueprint after changing it.

### Uploading Your Mod

#### You can skip this step if you already know how to upload a pavlov mod.

Navigate to "Window > Pavlov Workshop > Upload Mod" and select the mod you created, check windows and android, then press "Upload Mod" and wait for it to complete.

Congratulations! You have successfully created your own archery mod using the archery modkit.
