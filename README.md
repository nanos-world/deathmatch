# Deathmatch

The official nanos world Deathmatch game-mode. Fast-paced free-for-all shooting with random weapons, power-ups, kill streaks and the classic Unreal Tournament announcer.

![Deathmatch](https://user-images.githubusercontent.com/6226807/121760221-ec02a680-caff-11eb-8b2a-c0aea9168e41.jpg)


## Features

- Free-for-all matches with a full round cycle: **Warm-up → Preparing → Round → Post time**
- Players respawn with a random weapon from [Default Weapons](https://github.com/nanos-world/nanos-world-weapons)
- **Gun Game** mode: every 2 kills you level up to the next weapon, the first one to finish the list wins
- **Power-ups** spawned around the map, giving health and ammo
- **Multi kills** (Double, Triple, Multi, Mega, Ultra, Monster Kill) and **kill streaks** (Killing Spree, Rampage, Dominating, Unstoppable, Godlike)
- First Blood, countdown and winner announcements with the Unreal Tournament announcer
- Score feed, hit markers and kill feed powered by [Battlefield Kill UI](https://github.com/gtnardy/nanos-world-battlefield-kill-ui)
- Scoreboard (`Tab`), end of match ranking and Steam Leaderboard submission
- Random time of day every match


## Requirements

Loaded automatically by the game-mode:

- Package: `default-weapons`
- Package: `battlefield-kill-ui`
- Asset Pack: `unreal-tournament-announcer`

Works on any map with spawn points.


## Installation

In the server `Config.toml`:

```toml
[game]
    map =       "your-map"
    game_mode = "deathmatch"
```

Or through the command line:

```bash
./NanosWorldServer.exe --game_mode deathmatch --map your-map
```


## Configuration

Match rules are defined in `DeathmatchSettings` at the top of `Server/Index.lua`:

```lua
DeathmatchSettings = {
	warmup_time = 30,                 -- seconds of warm-up before the round
	preparing_time = 13,              -- seconds frozen before the round starts
	match_time = 300,                 -- round duration in seconds
	post_time = 15,                   -- seconds showing the results
	multikill_time = 6,               -- seconds between kills to count as a multi kill
	multikill_time_multiplier = 1,    -- extra seconds added for every multi kill in a row
	spawn_locations = Server.GetMapSpawnPoints(),
	weapons_to_use = "default",
	mode = GAME_MODE.DEATHMATCH,      -- or GAME_MODE.GUNGAME
}
```

The weapon pools (`DefaultWeapons` and `GunGameWeapons`) live in `Server/Config.lua`, so you can add or remove weapons, including your own classes:

```lua
GunGameWeapons = {
	NanosWorldWeapons.AR4,
	NanosWorldWeapons.AK47,
	NanosWorldWeapons.AWP,
	NanosWorldWeapons.DesertEagle,
	MyCustomWeapon,
}
```
