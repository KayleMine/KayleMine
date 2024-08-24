# :fas fa-mug-hot fa-fw: power 

!>  Called from combat routine.

?>  Example: unit.power.POWER_TYPE.FUNCTION_NAME >= 50 ; 

## Power type's
```lua
	base
	mana
	rage
	focus
	energy
	combopoints
	runes
	runicpower
	soulshards
	lunarpower
	astral
	holypower
	maelstrom
	chi
	insanity
	arcanecharges
	fury
	pain
	essence
```

## actual
?>  actual : Used to return raw power value.
```lua
local power = player.power.combopoints.actual

if player.power.combopoints.actual >= 5 and castable(SB.Evisicrate) then
	cast(SB.Evisicrate)
	return true
end
```

## max
?>  max : Used to return max power value.
```lua
local power = player.power.combopoints.max

-- you can do some math, because you know your max power
```

## deficit
?>  deficit : Used to return current power deficit value.
```lua
local power = player.power.combopoints.deficit

if player.power.combopoints.deficit >= 3 then
	cast(SB.Regen_Skill)
	return true
end
```

## deficitpercent
?>  deficitpercent : Used to return current power deficitpercent value.
```lua
local power = player.power.combopoints.deficitpercent

if player.power.combopoints.deficitpercent >= 30 then -- 30%
	cast(SB.Regen_Skill)
	return true
end
```

## percent
?>  percent : Used to return current power percent value.
```lua
local power = player.power.combopoints.percent

if player.power.combopoints.percent >= 40 then -- 40%
	cast(SB.Evisicrate)
	return true
end
```

## regen
?>  regen : Used to return current power regen speed value.
```lua
local power = player.power.combopoints.regen

-- you can do some math, because you know your regen rate
```

## predict
?>  predict : Used to predict current power regen speed value.
```lua
local power = player.power.combopoints.predict

if player.power.combopoints.predict >= 5 then -- 5 raw power renegerate on next tick
	cast(SB.Evisicrate)
	return true
end
```

## predictpercent
?>  predictpercent : Used to predict percent current power regen speed value.
```lua
local power = player.power.combopoints.predictpercent

if player.power.combopoints.predictpercent >= 5 then -- 5 % power renegerate on next tick
	cast(SB.Evisicrate)
	return true
end
```

## regenpercent
?>  regenpercent : Used to get regen percent of power.
```lua
local power = player.power.combopoints.regenpercent
```

## tomax
?>  tomax : Used to get regen time to max power.
```lua
local power = player.power.combopoints.tomax

if player.power.combopoints.tomax >= 3.5 then -- if time to regen power >= 3.5 seconds
	-- do something...
end
```
