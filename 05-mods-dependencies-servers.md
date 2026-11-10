# 05 - Content Mods, Dependencies, Community Servers

## Creating and sharing UGC [V: mod.io Modkit 3.0 FAQ]
**Content Mod**: Create Mod (select Mod) -> add `Pavlov_ModInitializer` -> set in definition -> add content -> upload.
**Gamemode**: Create UGC (select Gamemode) -> `Pavlov_GameLogic` (definition blank) with own proxy/global info -> assign in UGC definition -> upload. Cannot be loaded on a map with Custom enabled.
**Share assets between UGCs**: make mod UGC, drop asset pack in; make map UGC; place mod assets into map level; upload mod; upload map; set mod public; set dependency on map's mod.io page; make map public. Benefit: map re-uploads are small.
**Platform match**: PC+Linux tags = PC; **Oculus + Mac = Shack** (Oculus = client headset, Mac = Shack dedicated server).

## Community server config (Game.ini) [V wiki]
Path (Linux): `/home/steam/pavlovserver/Pavlov/Saved/Config/LinuxServer/Game.ini`. **Linux only; no Windows server binaries.** Section `[/Script/Pavlov.DedicatedServer]`.

```
bEnabled=true
ServerName="..."          ; ~35 chars, profanity filter may hide server
MaxPlayers=10             ; Shack: <=10 recommended, hard max 24
bSecured=true             ; VAC
bCustomServer=true        ; needed for modding save/http funcs and writing blacklist
bEnableBots=false
bCompetitive=false        ; SND only
bWhitelist=false
RefreshListTime=120
LimitedAmmoType=0
TickRate=90               ; do not touch
TimeLimit=60
AFKTimeLimit=300
Password=0000
BalanceTableURL="vankruptgames/BalancingTable/main"
MapRotation=(MapId="UGC1758245796", GameMode="GUN")
MapRotation=(MapId="datacenter", GameMode="SND")
MapRotation=(MapId="UGC3249319", GameMode="UGC3262731")   ; custom gamemode UGC (Modkit 3.0)
AdditionalMods=UGC3462586                                  ; mod loaded on every map
```
- Map/mod id = mod.io resource id prefixed `UGC` (e.g. 2773760 -> `UGC2773760`). Gamemodes **cannot** be AdditionalMods.
- An ApiKey from the Pavlov "Getting your API Key" section is required to register with the master server.
- Shack maps: create `Saved/maps`; rotate to the map (RCON/Game.ini) and the server auto-downloads. Also `mods.txt`, `blacklist.txt`, `whitelist.txt` in `Saved/Config`. Mod must be published for the Mac/Oculus platforms.
- Docker option (community guide): https://github.com/XavierSJC/pavlov-vr-server; ports 9100 (RCON), 8177, 7777 default. Hosted options named by wiki: Arctic VR, Horde (Shack).
- Multiple servers on one host, competitive mode (`-COMPETITIVE=1`), systemd supervision, auto-update scripts: see wiki page `Setting_up_a_dedicated_server`.

## RCON for modders [V]
`UGCAddMod UGC<id>`, `UGCRemoveMod`, `UGCClearModList`, `UGCModList` (map must rotate to apply); `SwitchMap <map> <mode>` e.g. `SwitchMap UGC3247570 UGC3267976` (map + custom gamemode); `ItemList`; `GiveItem`; `SetPlayerSkin`. Full list in [09](09-reference-ids-rcon-gamemodes.md).

## Security note [V mod.io, July 2026]
A popular "[MOD] Tools" mod by TsWizzard contained a paid backdoor (ban/kick/fly for non-staff); the author mods were privated 24 July 2026. If a map used it, remove it (can cause the "Datacenter bug"). A "Tools Blocker" mod existed as a dependency-based mitigation. Lesson: audit dependencies; a dependency runs code on your server.
