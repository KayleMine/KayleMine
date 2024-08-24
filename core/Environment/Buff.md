# :fas fa-heart-circle-plus fa-fw: Buff 

!> Called from unit.buff(spell_id).FUNCTION_NAME


## down
?> down : Used to check is this buff miss on unit.
```lua
if player.buff(6673).down and castable(6673) then
	cast(6673, player)
	return true
end
```

## up
?> up : Used to check is this buff exists on unit.
```lua
if player.buff(6673).up and castable(1234) then
	cast(1234, target)
	return true
end
```

## any
?> any : Used to check is this buff exists on unit but not account who casted it.
```lua
if player.buff(6673).any and castable(1234) then
	cast(1234, target)
	return true
end
```

## count
?> count : Used to check count of buff.
```lua
if player.buff(6673).count >= 20 and castable(1234) then
	cast(1234, target)
	return true
end
```

## remains
?> remains : Used to check remains time of buff in seconds.
```lua
if player.buff(6673).remains <= 6 and castable(6673) then
	cast(6673, player)
	return true
end
```

## duration
?> duration : Used to return duration of this buff.
```lua
if player.buff(6673).remains <= (player.buff(6673).duration * 0.3) and castable(6673) then
	cast(6673, player)
	return true
end
```

## stealable
?> stealable : Used to check can we steal it.
```lua
if target.buff(6673).stealable and castable(SB.SpellSteal) then
	cast(SB.SpellSteal, target)
	return true
end
```
