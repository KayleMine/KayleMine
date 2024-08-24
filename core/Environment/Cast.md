# :fas fa-wand-sparkles fa-fw: Cast 

!> Called from combat routine.

## cast
?> cast : Generally use to cast spell's.
```lua
if castable(12345) then
	cast(12345, target)
	return true
end
```

## hooks
!> dark_addon.environment.hooks.FUNCTION_NAME

?> Alternative: Can be called directly, if we in addon space. 

?> auto_attack : Used to start AA.
```lua
if target.distance <= 7.5 then
	auto_attack()
end
```

?> auto_shot : Used to start AS.
```lua
if target.distance <= 40 then
	auto_shot()
end
```

?> stopcast : Used to stop current cast.
```lua
if UnitCastingInfo('player') or UnitChannelInfo('player') then
	stopcast()
end
```

?> macro : Used to run macro text. [t_check can be found in support section]
```lua
local SEB_slot, _, SEB_Ready = t_check(194302) -- Storm-Eater's Boon
if SEB_Ready then
	macro('/use '.. SEB_Ready)
end
```
