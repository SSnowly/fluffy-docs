---
sidebar_position: 1
title: Configuration
description: Our Configuration file
---

```lua
Config = {}

Config.Framework = 'autodetect' -- 'autodetect', 'esx', 'qbcore', or 'qbox'
Config.FrameworkDetection = function()
    if Config.Framework == 'autodetect' then
        if GetResourceState('es_extended') == 'started' then
            Config.Framework = 'esx'
        elseif GetResourceState('qb-core') == 'started' then
            Config.Framework = 'qbcore'
        elseif GetResourceState('qbx_core') == 'started' then
            Config.Framework = 'qbox'
        else
            error('No framework found')
        end
    end
end

-- Framework specific settings
Config.FrameworkUpdateInterval = 500 -- ms

Config.enableDeathScreen = true -- if enabled the player will see a death screen when they die.
Config.enableMinimap = true -- if enabled the hud will "shift" to the right to make space for the minimap
Config.onlyVehicleMap = true -- if enabled the minimap will only show when in a vehicle
-- Speedometer settings
Config.useKMH = true -- Set to false to use MPH 
Config.fuelSystem = "gta"  -- "gta" or "ox_fuel" or "custom"
Config.fuelDetection = function(vehicle)
    if GetResourceState('ox_fuel') == 'started' then
        Config.fuelSystem = "ox_fuel"
    elseif GetResourceState('TAM_Fuel') == 'started' then
        Config.fuelSystem = "tam"
    else
        Config.fuelSystem = "gta"
    end
end
Config.customFuel = function(vehicle)
    local fuel = GetVehicleFuelLevel(vehicle)
    return fuel
end
-- Death settings
Config.deathTimer = 30 -- Time in seconds before respawn is available

--- lang
Config.Lang = {
    rpm = "RPM",
    fuel = "Fuel",
    speed = "Speed",
    gear = "Gear",
    health = "Health",
    stamina = "Stamina",
    oxygen = "Oxygen",
    armor = "Armor",
    thirst = "Thirst",
    hunger = "Hunger",
    stress = "Stress",

    -- Death messages
    youDied = "YOU DIED",
    respawnIn = "You can respawn in %s seconds",
    pressToRespawn = "Press %s to respawn",

    -- Seatbelt
    seatbelt = "Toggle Seatbelt",
    seatbeltOn = "Seatbelt On",
    seatbeltOff = "Seatbelt Off",
}

Config.displayOnChange = false -- true = should display "health", "armor", "thirst" and "hunger" only when the value changes. Stamina, Oxygen and Stress are always only visible on change.

-- anything below these values will be displayed forever if displayOnChange is true
Config.ThresholdValues = {
    health = 70,
    armor = false,
    thirst = 40,
    hunger = 40
}

-- Vehicle HUD update rate (updates per second)
-- Higher values will make the vehicle HUD smoother but increase resource usage
Config.vehicleUpdateRate = 30 -- Updates per second

-- Notification system
Config.NotifySystem = "ox" -- "esx", "qb", "ox", "custom", or "auto" (will detect based on framework)
Config.CustomNotify = function(title, description, type, length)
    -- Example: exports['your-notify']:ShowNotification(title, description, type, length)
end

Config.useCustomSeatbelt = true -- enables our seatbelt system
Config.SeatbeltGetter = function()
    -- Example: return exports['your-resource']:hasSeatbeltOn()
    return false -- default to false if not using custom
end
Config.EnableStress = true -- enables the stress system
Config.StressFunction = function(player)
    --local stress = exports['example_Export']:GetPlayerStress(player)
    return 30 -- number between 0 and 100, 0 = no stress, 100 = max stress
end

-- only enable if Config.EnableRespawn is true
Config.RespawnFunction = function()
    TriggerEvent('esx_ambulancejob:revive')
end

return Config
```