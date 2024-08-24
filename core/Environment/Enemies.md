# :fas fa-bolt fa-fw: enemies 

!> Called from combat routine.

## around
> around : Used to return enemies around us.
```lua
local enemyCount = enemies.around(8) -- 8 yards around player
if enemyCount == 0 then enemyCount = 1 end
```

## match
> match : Used to filter enemies.
```lua
local nearest_target = enemies.match(function(unit)
	return unit.name, unit.alive and unit.combat and unit.distance <= 5
end)
local NTname, NTbool = nearest_target;
if (not target.exists or target.distance > 5) and NTbool and NTname then
	TargetUnit(NTname)
end
```

## count
> count : Used to filter and count enemies.
```lua
local without_12345 = enemies.count(function(unit)
	return unit.alive and unit.distance <= 40 and unit.debuff(12345).down
end)
if without_12345 > 5 then ...
```
