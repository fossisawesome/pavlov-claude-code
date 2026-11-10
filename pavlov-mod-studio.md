# Publish your mods in one click with Pavlov Mod Studio

> Source: https://mod.io/g/pavlov/r/pavlov-mod-studio
> Author: MasterHyp | Added: 2026-11-07 | Updated: 2026-11-09 | Views: 17 | Comments: 0 | Tags: General Guide, Mod
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 13 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A free, open source Windows app for modders. Cook and publish to PC and Quest in one click, resume failed uploads, and leave unused assets out of your builds. Unofficial community tool.
> **WARNING: THIRD-PARTY TOOL guide (not official). Review before installing or sending credentials/tokens to anything.**

---
![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/icon.png)

**Cook, publish and manage your Pavlov mods from one desktop app.**
When an upload breaks, it picks up where it stopped.

[Download for Windows](https://github.com/PavlovVR/pavlov-mod-studio/releases/latest)  |  [GitHub](https://github.com/PavlovVR/pavlov-mod-studio)  |  [User guide](https://github.com/PavlovVR/pavlov-mod-studio/blob/main/docs/guide.md)

### Read this before you install

You should know what you're installing, so here it is up front:

- **It's unofficial.** It's made by community modders, and it isn't made by or affiliated with Vankrupt or mod.io.

- **It's open source.** Anyone can read every line of the code on [GitHub](https://github.com/PavlovVR/pavlov-mod-studio), under the MIT licence, and the installer is built there from that same code.

- **It needs a mod.io token to publish for you.** You make the token yourself, choose when it expires, and can delete it on mod.io at any time. It's encrypted on your PC and only ever sent to mod.io.

- **It adds nothing to your mods.** It builds them with the same Unreal commands as the modkit, and puts no code or files of its own inside.

- **Windows may warn you.** The installer isn't code signed yet, so SmartScreen can show a warning. Choose More info, then Run anyway.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/demo.gif)

### Why use it

The modkit's Upload button works until something goes wrong. A dropped connection stops the upload and clears the queue, so you start again. Mod Studio does the same job from outside the editor, and it's built around that moment.

|
  |
Modkit Upload button |
Pavlov Mod Studio |

|
**An upload fails** |
Stops and clears the queue |
Retries that chunk, and Resume finishes the rest |

|
**Unused assets** |
Everything in the plugin ships |
Leave out what nothing uses, in an Explorer-style tree |

|
**A build breaks** |
A message box |
Names the step and the build, with Unreal's errors and the full log |

|
**Rolling back** |
The mod.io website |
One click in the Files tab |

|
**Page, media, comments** |
The mod.io website |
All in the app |

### What it does

#### Publish without babysitting it

One click bumps the version, cooks every build, packages them and uploads to mod.io. If a chunk of the upload fails, only that chunk is retried. If the whole run stops, Resume skips everything already finished and sends only what's missing.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/publish-dark.png)

#### Publish your way

Choose the version number, name the files players see on mod.io, cook now and upload later, get a warning when a build is bigger than you want, post each new version to your Discord server, and publish a mod as another of your mods with Retarget as, such as a test copy for a development server. While a build cooks, the app shows your PC's CPU and memory, and tells you when Unreal is short of memory, which is what makes a cook crawl.

#### Leave out what nothing uses

Unreal cooks every asset in a mod's plugin, used or not. The Cook tab shows them all in a tree you use like Windows Explorer, and Filter only used finds what nothing uses. Other mods in your modkit count as users, and nothing is removed from your project.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/cook-dark.png)

#### Know exactly what broke

When a build fails, you see the step, the build, Unreal's own errors and a link to the full log. Every pak is checked before it uploads, and a build stops if it contains another mod's files.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/failure-dark.png)

#### Share only what you choose

Other modders might need one struct or interface from your mod, not the whole thing. The Source tab lists every file, and only what you tick leaves your PC. It warns when those files need something you left out.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/source-dark.png)

#### See which mods use which

The References tab maps which other mods' assets your mod uses, and which mods use its assets. It flags assets that don't exist, mods you don't have, and mods mod.io doesn't list as dependencies, with every asset searchable underneath. The whole modkit fits on one map too.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/references-dark.png)

#### Run your mods from one place

The app opens on all your mods, each with its picture, the version players have, how long ago it came out and its downloads. Open one to manage it without the website.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/home-dark.png)

|

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/overview-dark.png)

**Overview**
Downloads, rating and what's live on each platform

 |

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/files-dark.png)

**Files**
Every version and build, with one-click rollback

 |

|

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/size-dark.png)

**Size**
See what takes up the space in each build

 |

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/page-dark.png)

**Page**
Edit your mod's listing without the website

 |

### Set up

You need Windows 10 or 11, the Pavlov modkit, Unreal Engine 5.1 and a mod.io account.

- Download the installer from the [latest release](https://github.com/PavlovVR/pavlov-mod-studio/releases/latest) and run it.

- Open Settings, choose your modkit folder, and select Save settings.

- Read and accept Pavlov's EULA, which the app shows from your modkit. Nothing works until you do.

- Select Open mod.io, then Generate token. Tick All my mods, User actions, Read and Write, and set Expiry to 1 Year.

- Paste the token into the app and select Connect.

The first time the app opens, a short tour shows you around with sample mods. Nothing you do in it touches your own mods.

![image](https://raw.githubusercontent.com/PavlovVR/pavlov-mod-studio/main/docs/media/connect-dark.png)

### Publish a mod

- Open your mod from the grid, then open the Publish tab.

- Choose PC, Quest or Both.

- Write a change note.

- Select Publish.

The panel at the bottom shows each step, with progress for every build.

### Questions

**Does it replace the modkit?**
No. You still build your mod in Unreal. Mod Studio drives the modkit from outside the editor, and replaces its Upload button.

**Do I need to close Unreal to publish?**
No. If Unreal is open, the app has it save the new version. If you have unsaved work, it asks you to save first so it isn't left out of the build.

**Are updates safe?**
Every update is signed, and the app refuses anything that doesn't match. Releases can't be changed once they're published. Updating by itself waits until a version has been out for a day, so a bad release can be pulled before it reaches anyone, and it shows you what's new before it installs. It never updates during a publish.

**Can I try new features early?**
Yes. In Settings, under Updates, choose Beta. Betas come before everyone else gets them and can have bugs. You can switch back to Stable, or go back to an older version, any time.

**Why does my Quest server show as Mac on mod.io?**
That's how Pavlov's builds are published. Windows is the PC client, Linux is the PC server, Oculus is the Quest client and Mac is the Quest server.

### Help

The [user guide](https://github.com/PavlovVR/pavlov-mod-studio/blob/main/docs/guide.md) covers every tab and the problems you're most likely to hit. If something breaks, comment here or [open an issue](https://github.com/PavlovVR/pavlov-mod-studio/issues).
