# Hold The Van Event Script

A competitive FiveM event script where players compete to hold a van for the longest time to win rewards. Created by **POSEIDON DEVELOPMENTS**.

## 📋 Overview

The Hold The Van event is a PvP-focused script that spawns a van at random locations. Players must claim and hold the van within a 50-meter radius for a specified duration to win. The script features statistics tracking, streak systems, automatic event spawning, and a modern NUI interface.

## ✨ Features

- **Dynamic Van Spawning**: Van spawns at random configured locations
- **Redzone Blip System**: Large redzone blip on map showing event location with configurable radius
- **Hold Mechanics**: Players must stay within 50m radius to maintain hold
- **Modern NUI Interface**: Beautiful centered UI showing holder name and timer
- **Timer System**: Real-time countdown showing remaining hold time
- **Statistics Tracking**: Tracks wins, longest hold times, and player streaks
- **NUI Stats Display**: View statistics in a beautiful NUI interface with `/vanstats`
- **Streak System**: Consecutive wins grant bonus rewards
- **Auto-Spawn Events**: Automatically spawns events at configured intervals
- **Pre-Event Announcements**: Countdown notifications before auto-spawn events
- **Loot Rewards**: Winners receive configurable loot items
- **Death Detection**: Automatic teleportation away from van on death
- **Team/Gang Integration**: Displays player teams and gangs (QBCore)
- **Visual Effects**: Confetti and celebration effects on win
- **Memory Leak Prevention**: Local caching and proper cleanup handlers

## 📦 Dependencies

### Required
- **ox_lib** - For UI and notifications

### Optional (for full functionality)
- **ox_inventory** - For loot rewards (required if using loot system)
- **qb-core** - For job/gang integration

## 🚀 Installation

1. Download and place the script in your `resources` folder
2. Add to your `server.cfg`:
   ```
   ensure poseidon-vanhold
   ```
3. Ensure `ox_lib` is started before this resource
4. Configure the script in `config.lua` (see Configuration section)

## 📁 File Structure

```
poseidon-vanhold/
├── client/
│   └── client.lua          # Client-side script
├── server/
│   └── server.lua          # Server-side script
├── data/
│   ├── stats.json          # Statistics data (auto-generated)
│   └── streaks.json        # Streak data (auto-generated)
├── html/
│   ├── index.html          # NUI interface
│   ├── script.js           # NUI JavaScript
│   └── style.css           # NUI styles
├── config.lua              # Configuration file
└── fxmanifest.lua          # Resource manifest
```

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

### Redzone Blip Settings
Customize the redzone blip in `Config.RedzoneBlip`:
- `sprite` - Blip sprite ID (67 = van icon)
- `color` - Blip color (1 = red)
- `scale` - Blip scale (1.2)
- `radius` - Radius of the redzone blip on map (250.0 meters)

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

## 🎮 Commands

### Admin Commands
- `/startvan` - Start a van hold event (requires `command.startvan` ACE permission)
- `/stopvan` - Stop the current event (requires admin)

### Player Commands
- `/vanstats` - View event statistics in NUI interface (shows top players by wins)

## 🎯 How It Works

1. **Event Start**: Van spawns at a random configured location with redzone blip on map
2. **Countdown**: 5-second delay, then 5-second countdown before claiming is enabled
3. **Claiming**: Players press `E` near the van (within 2m, prompt shows at 5m)
4. **Holding**: Player must stay within 50m radius of the van
5. **Timer**: NUI shows remaining hold time counting down
6. **Death**: If holder dies, timer resets and they're teleported 100m away
7. **Win Condition**: First player to hold for the required time wins
8. **Rewards**: Winner receives loot from `Config.LOOT_POOL` and streak bonuses if applicable

## 📊 Statistics

The script tracks:
- Total events held
- Total wins per player
- Longest hold time and holder
- Most wins and player
- Win streaks per player

Statistics are saved to `data/stats.json` and `data/streaks.json` and persist across server restarts.

View stats with `/vanstats` command - displays in a beautiful NUI interface showing top players by wins.

## 🎨 UI Elements

- **Center NUI**: Shows current holder name and countdown timer (e.g., "John Doe Holds The Van!" or "You Hold The Van!")
- **Location Display**: Bottom of screen shows current van location name
- **Countdown Timer**: Shows "STARTING IN: X" when event is about to start
- **Press E Prompt**: Shows "Press [E] to Claim The Van" when within 5 meters of van
- **Stats Screen**: NUI interface showing top 20 players with wins (accessible via `/vanstats`)

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
- NUI updates are cached to prevent unnecessary messages and reduce memory usage

## 🐛 Troubleshooting

**Van doesn't spawn:**
- Check that locations are configured in `Config.VAN_LOCATIONS`
- Verify coordinates are valid

**Loot not giving:**
- Ensure `ox_inventory` is installed and running
- Check item names match your inventory system
- Verify `Config.LOOT_POOL` is properly configured

**Redzone blip not showing:**
- Check `Config.RedzoneBlip` is configured correctly
- Verify event has started (blip appears when van spawns)
- Open map and zoom out to see the blip

**Team/Gang not showing:**
- Ensure QBCore is installed and running
- Check that players have jobs/gangs assigned

**NUI not displaying:**
- Ensure `ox_lib` is installed and running
- Check browser console (F8) for any JavaScript errors
- Verify `html/` folder files are correct

## 📄 Version

**Current Version:** 1.1.0

## 👨‍💻 Support

For support, issues, or feature requests, contact **POSEIDON DEVELOPMENTS**.

Or make a ticket in our discord https://discord.gg/3w8bdfZusD

---

**Enjoy the competition! May the best holder win! 🏆**
