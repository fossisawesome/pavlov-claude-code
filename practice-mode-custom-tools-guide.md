# Practice Mode Custom Tools

> Source: https://mod.io/g/pavlov/r/practice-mode-custom-tools-guide
> Author: Stevie257 | Added: 2025-07-21 | Updated: 2025-07-22 | Views: 276 | Comments: 0 | Tags: Game Mode, Mod
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 15 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A guide on how to create custom tools for practice mode

---
This short guide will teach you how to create your own custom tools for [practice mode](https://mod.io/g/pavlov/m/practice-mode), a mod designed to help players sharpen their Pavlov skills.

 

### Before you begin

#### Make sure you have the [custom content source mod](https://mod.io/g/pavlov/m/practice-mode-custom-content) added to your project

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/customcontentadded.png)

 

### Step 1: Creating your mod

The custom tools in practice mode are handled via content mods. To add your custom tool(s) to a lobby you'll need to set up a Pavlov mod with the proper mod initializer.

##### Start by creating a Pavlov mod like normal

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/createmod.png)

 

##### Create a mod initializer as a child of the Practice_CustomBaseInit class

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/child.png)

Your mod initializer **must** be a child of the **`Practice_CustomBaseInit` **class for it to be properly recognized by the gamemode.

|

#### Important

It's important that you do not edit the `Practice_CustomBaseInit` class. Your changes will not be uploaded with your mod and will end up breaking your mod or potentially crashing players' games. The same is true for any other assets in the custom content mod's plugin folder. ( UGC5103039 )

You can, however, freely edit any children you make of the class.

 |

Once you've created your mod initializer you'll have to add it to your mod's definition.

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/definition.png)

We'll come back to your mod initializer later.

 

### Step 2: Creating a tool

All of your tools will be read from a Data Table referenced in your mod initializer. 

##### Creating a table

A premade data table exists in the custom content plugin folder that you can copy to your mod's folder. You can also create a data table yourself with the following steps.

You can create a data table from the **Miscellaneous **tab when creating a new asset. 

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/createtable.png)

The data table will need to use the **`CustomWindowData` **struct found within the custom content mod's plugin folder

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/tablestruct.png)

 

##### Adding tools to the table

Once you've created or copied your data table, you'll have to add a new row to the table for each tool you want to make.

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/createrow.png)

After adding a new row you should see something like this:

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/newrow2.png)

This is where you'll define all of the parameters of your tool and it's window.

Here's a brief explanation of each parameter. All of the parameters have tooltips as well that you can read to see the same information.

|

**WidgetClass** - The widget that will be displayed in your tool's window. Cannot be left empty

**AppTitle** - The text that will appear in your tool's button and title bar. Cannot be left empty and cannot exceed 32 characters

**AppIcon** - An icon image for the button in the tools page. Can be left empty to have no icon

**WindowSize** - The size your window will be. Must be 1080x1080 or less and 400x400 or more. **Note:** the widget displayed within the window will be smaller than the window's total size

**WindowID** - The unique ID for your tool. Cannot use an existing ID of another tool, custom or vanilla

**LogicComponent** - An actor component that will be added to the practice UI actor when your tool is opened. Will also be removed when your window is closed. Client-side only. Can be left empty if your tool doesn't need it

**ShowPinButton** - Whether or not to show the pin button in the title bar. Pinned tools will remain visible when the practice UI is closed

**BackgroundImage** - An image that will be displayed in the background of the tool's window. Will use BackgroundColor if left empty

**BackgroundColor** - The background color for the tool's window. Will be used if BackgroundImage is empty or invalid

 |

 

##### Fill out your tool's info

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/filledout.png)

To avoid confusion and potential bugs, I would recommend also changing your row's name to your WindowID

 

##### Tool icon best practices

The way the mod renders tool icons results in them being tinted different colors based on whether the tool is hovered over with the cursor or not. **If your icon has color it will end up looking strange**, so I highly recommend using a completely white icon (with a transparent background) or at the very least a grayscale image. Tool icons should ideally be square (1:1 aspect ratio) as well to avoid stretching. The image included with the custom content mod is an example of what an icon should ideally look like.

 

You're almost finished, all that's left is a widget for your tool

 

### Step 3: Creating a widget

You'll create the actual UI for your tool using widgets.

You can create a new widget under the **User Interface** tab when creating a new asset.

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/createwidget.png)

 

Choose **User Widget** when creating the widget

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/userwidget.png)

 

I wont be covering how to create widgets in this guide as plenty of tutorials can be found online

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/toolwidget.png)

 

##### Once you've created your widget, specify it in your data table

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/customwidgetadded.png)

 

### Step 4: Adding logic

After you've created your widget you can run logic when buttons are pressed or when checkboxes are checked, etc.

It's important to note that the practice UI and any tool windows created by it are entirely **client-sided**, so you won't be able to run functions directly from your widget that require server authority such as spawning items.

 

### Final steps

The final step is to reference your data table in your mod initializer. You can set the table in the class defaults tab in your mod initializer.

![image](https://image.modcdn.io/members/0492/29223580/profilepracguid/tableref.png)

 

##### You can upload your mod when you're ready!

Once you've uploaded your mod, simply add it as a content mod to your lobby after choosing practice mode as your gamemode. If you've set everything up correctly your tool(s) should appear in the CUSTOM tab in the practice UI.

![image](https://github.com/Stevie257/images/blob/530b6082b7d84976b8a10a2e7639ab3507d38814/toolgif.gif?raw=true)

 

### Final words

Something important to note is that if your mod does not have the [custom content mod](https://mod.io/g/pavlov/m/practice-mode-custom-content) added as a dependency it may crash people's games if they try to load your mod in a lobby that isn't running practice mode. While this may be an unusual circumstance, it might be best to add the mod as dependency just in case.

The custom content mod can be found here:
https://mod.io/g/pavlov/m/practice-mode-custom-content

The example tool shown in this guide can also be downloaded as a source mod for reference
https://mod.io/g/pavlov/m/custom-tool-example

 

Thank you for reading to the end! I'm curious what people might make for practice mode, so please leave a comment on this guide or send me a message on Discord (username Stevie257) with your mod.
