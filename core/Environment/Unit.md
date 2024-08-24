# :fas fa-user fa-fw: unit 

!> Called from combat routine.

##  id
?> id : Used to get unit id.
```lua
if unit.id == 12345 then 
	-- do something if current unit id equal 12345
end
```

##  IsDummy
?> IsDummy : Used to check is unit training dummy.
```lua
if unit.IsDummy then
	-- do something if unit dummy
end
```

##  IsBoss
?> IsBoss : Used to check is unit boss.
```lua
if unit.IsBoss then
	-- do something if unit boss
end
```

##  alive
?> alive : Used to check is unit alive.
```lua
if unit.alive then
	-- while unit alive do stuff
end
```

##  level
?> level : Used to check is unit level.
```lua
if unit.level >= 25 then
	-- do something if unit level 25
end
```

##  dead
?> dead : Used to check is unit dead or ghost.
```lua
if unit.dead then
	-- do something if unit dead
end
```

##  enemy
?> enemy : Used to check is unit enemy.
```lua
if unit.enemy then	
	-- do something if unit enemy (not in combat with you)
end
```

##  combat
?> combat : Used to check is unit in combat.
```lua
if unit.combat then ...
```

##  friend
?> friend : Used to check is unit friend.
```lua
if unit.friend then
	-- do something if unit friendly
end
```

##  name
?> name : Used to get unit name.
```lua
if unit.name == "Sexy Elf" then
	-- do something if unit name match something.
end
```

##  exists
?> exists : Used to check is unit exists.
```lua
if unit.exists then
	-- check are this units exists?
end
```

##  guid
?> guid : Used to get unit guid.
```lua
local Uguid = unit.guid

-- identifier of unit
```

##  distance
?> distance : Used to get distance to unit.
```lua
if unit.distance <= 8 then
	-- do something if unit distance <= 8 yards
end
```

##  channeling
?> channeling : Used to check is unit channeling spell_id.
```lua
if unit.channeling(12345) then
	-- do something if unit channeling cast (spell_id)
end
```

##  castingpercent
?> castingpercent : Used to get unit casting percent.
```lua
if unit.castingpercent >= 50 then
	-- do something if unit cast percent (not channel) more or equal 50 %
end
```

##  moving
?> moving : Used to check is unit moving.
```lua
if unit.moving then
	-- do something if unit moving
end
```

##  has_stealable
?> has_stealable : Used to check is unit have stealable buff.
```lua
if unit.has_stealable then
	-- do something if unit has buff that we can steal.
end
```

##  interrupt
?> interrupt : Used to check can we interrupt cast.
?> false or spell_id to interrupt.
```lua
local intpercentlow = 10
local intpercenthigh = 90
local intpercent = math.random(intpercentlow, intpercenthigh)

if unit.interrupt(intpercent, false) then
	cast(SB.Stormbolt, unit)
	return true
end
```

##  in_range
?> in_range : Used to check is unit in range of certain spell_id.
```lua
if unit.in_range(6603) then
	-- do something if unit in range certain spell (by spell_id)
end
```

##  time_to_die
?> time_to_die : Used to get time to die of unit.
```lua
if unit.time_to_die >= 15 then
	-- if time to die more than 15 seconds do something
end
```

##  castable
?> castable : Used to check is certain spell_id castable to that unit.
```lua
if unit.castable(12345) then
	-- check can we cast at unit spell 12345
end
```
