# 09 - Reference: IDs, Game Modes, Maps, RCON

Source: pavlovwiki `ItemIDs`, `Setting_up_a_dedicated_server`, `Rcon_Overview_and_Commands`, `Vehicles`, mod.io "All Pavlov ids". [V] Item IDs are the **PC/base-game set**; Shack availability of each item may differ [?]. Use RCON `ItemList` on a live Shack server for the authoritative list.

## Game mode IDs (Game.ini `GameMode=` / RCON SwitchMap)
DM, KOTH, GUN (gun game), OITC, SND, TANKTDM (WW2 TDM), TDM, TTT, TTTclassic, WW2GUN, ZWV (zombie wave), HIDE (The Hidden), INFECTION, PUSH, PH (prop hunt). Custom: `UGC<id>` of a Gamemode UGC. Custom-mode maps override the mode.

## Default map IDs
datacenter, sand, bridge, containeryard, siberia (Prison Break), hospital (Zombies), killhouse, range, tutorial, santorini, station, industry; **Shack only**: ogcontainers, haguenau, foundation; PC only: stalingrad(+_night), santorini_night, sand_night, station_night, industry_night, bunker.

## Item IDs
- **Pistols**: 1911, 57, cet9, de, goldengun, luger, m9, revolver, silentcet9, sock, tokarev, webley
- **SMGs**: ak, ar9, detectivesmg, kross, mp40, mp5, p90, ppsh, skorpion, smg, sten, thompson, uzi
- **Shotguns**: autoshotgun, drumshotgun, sawedoff, shotgun, trenchgun
- **Rifles**: ak12, ak47, akshorty, ar, aug, autosniper, g43, galul, m16, m1garand, sks, stg44, svt40, vanas
- **LMGs**: bar, bren, dp27, lmga, mg42, pkm, tankmg
- **Snipers**: antitank, awp, hunting, kar98, leeenfield, mosin, scur, springfield, vzz
- **Launchers**: rl_m1a1, rl_panzer, rl_piat, rl_rpg, tankturret
- **Knives**: knife, tttknife, ww2knife; **Other weapons**: flaregun, newtonlauncher, taser, tranqgun
- **Attachments**: acog, bayonet_{kar98,leeenfield,m1garand,mosin,springfield,trenchgun}, canted_reddot, flashlight_rifle, grip_angled, grip_vertical, holo, laser_pistol, laser_rifle, reddot, reddot_pistol, scope, scope_{kar98,leeenfield,mosin,springfield}, supp_pistol, supp_rifle
- **Meds**: adrenaline, bandage, medkit, painkillers, syringe, ww2bandage, ww2medkit, ww2painkillers, ww2syringe
- **Grenades**: flash, flash_aurora, flash_ru, grenade, grenade_{aurora,dis,ger,ru,svt,us}, smoke, smoke_{ger,ru,svt,us}
- **Mines**: antipersonnelmine, antitankmine, tripalarm
- **Ammo**: ammo_pistol, ammo_rifle, ammo_shotgun, ammo_smg, ammo_sniper, ammo_special, ammocrate
- **Misc**: armour, ballisticsshield, boltcutters, cloakdisrupter, crowbar, dnascanner, handcuffs, healthstation, kevlarhelmet, keycard, lockpick, monocular, pickaxe, pipe, pliers, pushBomb, repairtool, skinhelmet_{ger,svt,us}, snowball, teleporter, tttc4
- **Skins**: aurora, clown, cop, farmer, german, kevin, naked, nato, nato1-4, prisoner, russian, russian1-4, soviet, us
- **Vehicles (health)**: atv 400, kubel 750, motorcycle 400, panzer 1000, sherman 1000, t34 1000, tiger 1500, truck 750, willys 750, willys_svt 750
- **TTT roles (case sensitive)**: Innocent, Traitor, Detective, Mercenary, Glitch, Assassin, Jester, Survivalist, Sheriff, Tank, LoneWolf, Zombie, Hypnotist, Soulmate, Psychopath

## Attachment prices (wiki `Attachments`)
Angled/vertical grip $300, pistol sight/red dot/holo/canted/rifle suppressor/rifle laser/flashlight $500, ACOG/8x $400, pistol suppressor $250, pistol laser $400.

## RCON
- TCP, default port 9100 (Docker guide forwards 9100, 8177, 7777). Server sends a password request; client replies with **lowercase hex MD5 of the password**, no newline; reply `Authenticated=1` or `0`. Replies are JSON `{"Command","Comment","Successful", ...}`. Placeholders: [UniqueID] = SteamID64 (PC) / **Oculus username (Shack)**; [TeamID] 0 blue, 1 red. Use open-source RCON tools only (some hosted tools steal passwords).
- Commands: Help, AddMapRotation, RemoveMapRotation, MapList, SwitchMap, RotateMap, AddMod, RemoveMod, ModeratorList (admin list), UGCAddMod/UGCRemoveMod/UGCClearModList/UGCModList, Ban, Unban, Banlist, Kick, Kill, Slap, Gag, Teleport, SwitchTeam, GiveItem, GiveAll, GiveCash, GiveTeamCash, SetCash, SetPlayerSkin, ItemList, InspectAll/InspectPlayer/InspectTeam, ServerInfo, SetMaxPlayers, SetPin, SetTimeLimit, UpdateServerName, SetLimitedAmmoType, SetBalanceTableURL, SetBotsEnabled, ShowNametags, EnableCompMode, EnableVerboseLogging, EnableWhitelist, PauseMatch, ResetSND, ClearEmptyVehicles, RefreshList, ShutdownServer, Disconnect, TTT*: TTTAlwaysEnableSkinMenu, TTTEndRound, TTTFlushKarma, TTTGiveCredits, TTTPauseTimer, TTTSetKarma, TTTSetRole. Parameter details: wiki page `Rcon_Overview_and_Commands`.

## Pavlov TV API
Custom OBS/stream overlays: wiki page `Pavlov_TV_API` (PC spectate/PAV TV); not Shack-specific [not read in depth].
