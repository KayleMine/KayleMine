# :fas fa-heart-circle-xmark fa-fw: Debuff 

!> Called from unit.debuff(spell_id).FUNCTION_NAME


## down
?> down : Used to check is this debuff miss on unit.
```lua
if target.debuff(6673).down and castable(6673) then
	cast(6673, target)
	return true
end
```

## up
?> up : Used to check is this debuff exists on unit.
```lua
if target.debuff(6673).up and castable(1234) then
	cast(1234, target)
	return true
end
```

## any
?> any : Used to check is this debuff exists on unit but not account who casted it.
```lua
if target.debuff(6673).any and castable(1234) then
	cast(1234, target)
	return true
end
```

## count
?> count : Used to check count of debuff.
```lua
if target.debuff(6673).count >= 20 and castable(1234) then
	cast(1234, target)
	return true
end
```

## remains
?> remains : Used to check remains time of debuff in seconds.
```lua
if target.debuff(6673).remains <= 6 and castable(6673) then
	cast(6673, target)
	return true
end
```

## duration
?> duration : Used to return duration of this debuff.
```lua
if target.debuff(6673).remains <= (target.debuff(6673).duration * 0.3) and castable(6673) then
	cast(6673, target)
	return true
end
```
