# PDEVvanhold
POSEIDON VAN HOLD SCRIPT - custom van hold script for your Fivem server

# Hold The Van Event Script

A competitive FiveM event script where players compete to hold a van for the longest time to win rewards. Created by **POSEIDON DEVELOPMENTS**.

## 📋 Overview

The Hold The Van event is a PvP-focused script that spawns a van at random locations. Players must claim and hold the van within a 50-meter radius for a specified duration to win. The script features statistics tracking, leaderboards, streak systems, and automatic event spawning.

## ✨ Features

- **Dynamic Van Spawning**: Van spawns at random configured locations
- **Hold Mechanics**: Players must stay within 50m radius to maintain hold
- **Timer System**: Real-time countdown showing hold progress
- **Statistics Tracking**: Tracks wins, longest hold times, and player streaks
- **Leaderboard System**: View top players with `/vanleaderboard`
- **Streak System**: Consecutive wins grant bonus rewards
- **Auto-Spawn Events**: Automatically spawns events at configured intervals
- **Pre-Event Announcements**: Countdown notifications before auto-spawn events
- **Loot Rewards**: Winners receive configurable loot items
- **Kill Feed**: Notifications when van holders are killed
- **Death Detection**: Automatic teleportation away from van on death
- **Team/Gang Integration**: Displays player teams and gangs (QBCore)
- **Visual Effects**: Confetti and celebration effects on win

## 📦 Dependencies

### Required
- **ox_lib** - For UI and notifications

### Optional (for full functionality)
- **ox_inventory** - For loot rewards (required if using loot system)
- **qb-core** - For job/gang integration
- **Ambulance System** (one of the following):
  - `wasabi_ambulance`
  - `qb-ambulancejob`
  - `qb-core` (basic respawn)

## 🚀 Installation

1. Download and place the script in your `resources` folder
2. Add to your `server.cfg`:
   ```
   ensure poseidon-vanhold
   ```
3. Ensure `ox_lib` is started before this resource
4. Configure the script in `config.lua` (see Configuration section)

## ⚙️ Configuration

All configuration is done in `config.lua`. Key settings include:

### Van Locations
Add spawn locations in `Config.VAN_LOCATIONS`:
```lua
{
    name = "Location Name",
    coords = vector3(x, y, z),
    heading = 0.0,
    holdTime = 60  -- Optional: custom hold time for this location
}
```

### Hold Time
- `Config.DEFAULT_HOLD_TIME` - Default time required to hold (in seconds)
- Each location can have its own `holdTime` override

### Blip Settings
Customize map blips in `Config.BLIP_SETTINGS`:
- Van blip sprite, color, and scale
- Zone radius blip color, alpha, and scale

### Loot Pool
Configure rewards in `Config.LOOT_POOL`:
```lua
{
    item = "item_name",
    minCount = 1,
    maxCount = 10,
    chance = 100,  -- 0-100 percentage
    minItems = 1,  -- Minimum times this item can be selected
    maxItems = 3   -- Maximum times this item can be selected
}
```

### Streak System
Enable/disable and configure streak rewards:
- `Config.STREAK_ENABLED` - Enable/disable streak system
- `Config.STREAK_BONUS_LOOT` - Bonus items for consecutive wins

### Auto-Spawn
- `Config.AUTO_SPAWN_ENABLED` - Enable automatic event spawning
- `Config.AUTO_SPAWN_INTERVAL` - Minutes between auto-spawns
- `Config.PRE_EVENT_ANNOUNCEMENT` - Show countdown notifications
- `Config.ANNOUNCEMENT_TIME` - Minutes before event to start announcements

### Ambulance System
- `Config.AMBULANCE_SYSTEM` - Set to "auto", "wasabi", "qb-ambulancejob", "qb-core", or "none"
- `Config.RESPAWN_AFTER_TELEPORT` - Respawn player after death teleportation

## 🎮 Commands

### Admin Commands
- `/startvan` - Start a van hold event (requires `command.startvan` ACE permission)
- `/stopvan` - Stop the current event (requires admin)

### Player Commands
- `/vanstats` - View event statistics
- `/vanleaderboard` - Display the leaderboard (top 20 players)

## 🎯 How It Works

1. **Event Start**: Van spawns at a random configured location
2. **Countdown**: 5-second delay, then 5-second countdown before claiming is enabled
3. **Claiming**: Players press `E` near the van (within 2m) to claim it
4. **Holding**: Player must stay within 50m radius of the van
5. **Timer**: Hold time counts up while player maintains hold
6. **Death**: If holder dies, timer resets and they're teleported away
7. **Win Condition**: First player to hold for the required time wins
8. **Rewards**: Winner receives loot from `Config.LOOT_POOL` and streak bonuses if applicable

## 📊 Statistics

The script tracks:
- Total events held
- Total wins per player
- Longest hold time and holder
- Most wins and player
- Win streaks per player

Statistics are saved to `stats.json` and `streaks.json` and persist across server restarts.

## 🎨 UI Elements

- **Top-Left HUD**: Shows current holder, team/gang, and hold timer
- **Center Screen**: "YOU ARE HOLDING THE VAN" indicator for holder
- **Countdown Timer**: Shows countdown before event starts
- **Location Display**: Shows current van location name
- **Leaderboard**: Overlay showing top 20 players (press ESC to close)
- **Kill Feed**: Notifications when van holders are killed

## 🔧 Permissions

Add to your `server.cfg` or permissions system:
```
add_ace group.admin command.startvan allow
add_ace group.admin command.stopvan allow
```

## 📝 Notes

- The van is invincible and cannot be damaged
- Players are teleported 100m away from the van on death
- Events timeout after 20 minutes if no one claims the van
- Streaks reset for all players when someone else wins
- Statistics are cached and saved periodically (every 30 seconds) or on critical events

## 🐛 Troubleshooting

**Van doesn't spawn:**
- Check that locations are configured in `Config.VAN_LOCATIONS`
- Verify coordinates are valid

**Loot not giving:**
- Ensure `ox_inventory` is installed and running
- Check item names match your inventory system
- Verify `Config.LOOT_POOL` is properly configured

**Respawn not working:**
- Set `Config.AMBULANCE_SYSTEM` to match your ambulance script
- Or set to "none" if you don't use an ambulance system

**Team/Gang not showing:**
- Ensure QBCore is installed and running
- Check that players have jobs/gangs assigned

## 📄 Version

**Current Version:** 1.1.0

## 👨‍💻 Support

For support, issues, or feature requests, contact **POSEIDON DEVELOPMENTS**.

Or make a ticket in our discord https://discord.gg/3w8bdfZusD

---

**Enjoy the competition! May the best holder win! 🏆**


