# :fas fa-radio fa-fw: Listener 

!> Called from addon space.

### Listener:Add
?> Listener:Add : Used to create listner for event.
```lua

local function combatLogHandler(event, ...)
    local timestamp, subevent, _, sourceGUID, sourceName, sourceFlags, sourceRaidFlags, destGUID, destName, destFlags, destRaidFlags = ... -- unpack event COMBAT_LOG_EVENT_UNFILTERED

    if subevent == "SPELL_CAST_SUCCESS" and sourceGUID == UnitGUID("player") then -- we casted
        local spellId, spellName, spellSchool = select(12, ...) -- unpack event SPELL_CAST_SUCCESS
        print(sourceName, ' :: Casted :: ', FlexIcon(spellId, 25,25), ' :: at :: ', destName)
    end

    if subevent == "SPELL_CAST_SUCCESS" and destGUID == UnitGUID("player") then -- casted on me
        local spellId, spellName, spellSchool = select(12, ...) -- unpack event SPELL_CAST_SUCCESS
        print(sourceName, ' :: Casted :: ', FlexIcon(spellId, 25,25), ' :: at :: ', destName)
        if spellId == 1126 then -- my buff
            cast(61336, player) -- feral save just to test
        end
    end

end
setfenv(combatLogHandler, dark_addon.environment.env)

dark_addon.Listener:Add("CombatLogHandler", "COMBAT_LOG_EVENT_UNFILTERED", function(...)
    combatLogHandler("COMBAT_LOG_EVENT_UNFILTERED", CombatLogGetCurrentEventInfo())
end)
```

### Listener:Remove
?> Listener:Remove : Used to Remove listner.
```lua

dark_addon.Listener:Remove("CombatLogHandler", "COMBAT_LOG_EVENT_UNFILTERED")
```

### Listener:Trigger
?> Listener:Trigger : Used to listen event.
```lua
dark_addon.Listener:Trigger("COMBAT_LOG_EVENT_UNFILTERED", function() end)
```
