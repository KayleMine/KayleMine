# :fas fa-address-book fa-fw: group 

!> Called from combat routine.

## removable
?> removable : Used to return unit that have debuff from dark_addon.data.removables table.
```lua
local unit = group.removable("disease", "magic", "poison", "curse", "freedom")
if unit and unit.distance <= 15 and castable(SB.Cleanse) then
	cast(SB.Cleanse, unit)
	return true
end
```

## buffable
?> buffable : Used to return unit that don't have buff.
```lua
local unit = group.buffable(12345)
if unit and unit.distance <= 15 and castable(5555) then
	cast(5555, unit)
	return true
end
```

## exists
?> exists : Used to get unit with buff from group.
```lua
local unit = group.exists(12345)
if unit and unit.distance <= 25 and castable(6666) then
	cast(6666, unit)
	return true
end
```

## dispellable
?> dispellable : Used to get unit that can be dispelled by certain spell.
```lua
local unit = group.dispellable(SB.Cleanse)
if unit and unit.distance <= 15 and castable(SB.Cleanse) then
	cast(SB.Cleanse, unit)
	return true
end

```

## under
?> under : Used to count units by health in range.
?> true or false swaps  unit.health.effective to  unit.health.percent
```lua
group.under(80, 30, false) >= 3 -- 3 units

if group.under(80, 30, false) >= 3 and castable(SB.Tranquility) then -- if 3 members in 30 yards around player, under 80 percent HP
	cast(SB.Tranquility, player)
	return true
end
```

## match
?> match : Used to filter members.
```lua
local nearest_target_for_rejuvenation = group.match(function(unit)
	return unit.alive and unit.combat and unit.distance <= 15 and unit.buff(SB.Rejuvenation).down
end)

if nearest_target_for_rejuvenation and castable(SB.Rejuvenation) then
	cast(SB.Rejuvenation, nearest_target_for_rejuvenation)
	return true
end
```

## count
?> count : Used to filter and count members.
```lua
local Without_Rejuvenation_count = group.count(function(unit)
	return unit.alive and unit.distance <= 40 and unit.debuff(SB.Rejuvenation).down
end)

if Without_Rejuvenation_count > 3 then ...
```
