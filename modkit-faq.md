# Modkit FAQ

> Source: https://mod.io/g/pavlov/r/modkit-faq
> Author: Juntistik99 | Added: 2023-02-19 | Updated: 2023-09-08 | Views: 2688 | Comments: 4 | Tags: FAQ, General Guide, upgrade
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 3 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Some of the questions from the modding community answered.

---
#### Does this work for Shack?

Yes!

 

#### How does versioning work?

Versioning is automatic when updating content to Mod.Io Pavlov client will update the mod when a new version is seen.

 

#### Will we be able to make full custom skins directly (like hands, the vest,... are not supported in the current modkit)

You can set custom hands in the player proxy. You will use function override. The vest you cannot change at this time. 

 

#### Can you rig custom character eyes for PS5 eye tracking.

Not at this time.

 

#### Is there a way to drop items with a direct reference?

Yes you can, you can use the slot index to determine which gun it is you're dropping.

#### Is there a way to get the references for the pavlov main menu to modify it? (like to change the color of the buttons,...)

This is not something we want to encourage as we want core functionality of Pavlov to remain consistent, such as leaving a map or accessing settings.

 

#### Will there be a way to modify/replace original pav stuff with mods (for example making a slightly customised ak and replace the original with it)

Yes, in modkit 3.0 (very soon)

 

#### Will skins rigged for current UE4 Pavlov continue to work on UE5?

Yes

 

#### Would it be possible to store text data on clients (like the modsave folder on server) with that you could make single player stuff that could save progress or some other cool stuff

You can store it on a community server, but not the player client. Will not work for lobbies as the server is destroyed after the match.

 

#### Can you add custom voice lines to push?

This is fixed in Modkit 3.0 (very soon)

 

#### What should I do about fake references or reflections in my mod?

Remove all the old fake references, and use the references we have supplied.

 

#### Does Lumen or Nanite work?

They are not supported. Lumen and Ninite are currently only for deferred rendering. Pavlov uses forward rendering.

 

#### The sky sphere looked bugged out after building light.

This is a UE 5 bug we’re currently trying to resolve. You can click "refresh material" to bring it back in the skysphere settings to address this in the meantime.

 

#### Are custom c++ plugins enabled?

No. Likely never will be.

 

#### My cook is taking a really long time, what gives?

Shaders are cooking for the first time. It will be much faster after the first cook.

 

#### Objects like spent shells and grenades are falling through my map floor and walls!if you are using complex as simple with single sided geo, it’s highly recommended to make custom collision for the object. Otherwise chaos physics will let things pass through it on occasion.

 

#### How can I reference other mods, gamemodes, or custom guns?

Modkit 3.0 will have this ability (Very soon) 

Separate custom weapons and game modes that are not tied down to map files will come in the future. When you click Create Mod tab see how it has that Map option, that will eventually have Map/GameMode/Mod (Maps are legacy or just a map, Gamemode is just gamelogic + things it references, and Mod is a content pack youll get a list of actors that will spawn when it starts to set it up yourself)

 

#### Is there a way to drop items with a direct reference?

Currently you only can use the item IDs to drop an item of a certain type but you can't choose what item exactly Yes you can, you can use the slot index to determine which gun it is you're dropping.

 

#### My builds are failing! How can I troubleshoot?

Check your logs in the output log in the editor or in yourproject/saved/logs directory of windows file system. The easiest way to check for errors is go to the end of the log, find "error" then search up. If you start at the top and search down you will have to wade through irrelevant errors. 

 

#### Can we customize the buy menu?

Not at this time, but will come in Modkit 3.0

 

#### Is there a way to preview a custom hand pose?

A guide has been written for this: [Custom Hand Sequence Guide](https://mod.io/g/pavlov/r/custom-hand-sequence-guide)

 

#### What is the best way to optimize glass or windows?

We discourage making glass windows with masked materials, for a couple of reasons:

1. It leverages the alpha to coverage feature of the forward renderer, which relies on MSAA being turned on. We allow for different settings of anti-aliasing, which will break the effect for some players who choose to turn the anti aliasing off.
 

2. The occlusion/visibility issues- seems like this behaviour has changed in between UE 4 and 5, masked transparent windows will still act as occluders. the translucent windows could still cause sorting issues.
 
3. It is best to use a translucent material for glass, if you're worried about the shading quality we recommend setting the lighting mode to Surface Forward Shading.

![image](images/modkit-faq/626daf7dd5.png) <!-- src: https://i.imgur.com/oHPu9x5.png -->

 
You should also not merge too many glass sheets into one object, to help with sorting against some effects like smoke or blood.  Ideally you could use instanced meshes for your windows
 

####

#### How do only cook the assets used in the map instead of all the assets in the plugin folder?

ProjectSettings -> Packaging -> Advanced dropdown -> DirectoriesToNeverCook. Add your directories  you don't want included.
 
 

#### My mods are uploading slowly, how can I address this?

Go to Edit->EditorPreferences->Performance set UseLess CPU when in Background to false

![image](images/modkit-faq/f5d1ee11a4.png) <!-- src: https://i.imgur.com/7Fe2c97.png -->

 

#### My viewport looks blurry in editor what gives?

go to same location as above, adjust the Overrides to manual and set the editor viewport screen percentage to 100.

 

 
![image](images/modkit-faq/c12a04de2c.png) <!-- src: https://i.imgur.com/BWa5DiL.png -->


---

## Comments (mod.io API, 4)

- **idwin** (2024-06-25): it loads up in note pad
- **Franzi57** (2023-11-10): WARNING: When using assets, do not name a folder "windows" ( or change the name ) because UE 5.1.1 of the modkit is a packaging error ! ATTENTION : Quand vous utilisez des assets, ne pas nommer un dossier "windows" ( ou changez le nom ) car UE 5.1.1 du modkit est une erreur  pour le packaging !
- **Franzi57** (2023-10-08): Hello! I have a problem uploading a map, which tells me: "failed for Linux Server"! ? what's the problem? i don't have this problem with other maps! Thanks in advance for your answers.
- **-nukester-** (2023-09-25): youre making me blush
