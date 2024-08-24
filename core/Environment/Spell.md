# :fas fa-newspaper fa-fw: spell 

!> Called from -spell(spell_id).FUNCTION_NAME

?> Some api can be called like: unit.spell(spell_id).FUNCTION_NAME

##  cooldown
?> cooldown : Used to return spell cooldown.
```lua
local Rampage = -spell(184367).cooldown

if -spell(184367).cooldown >= 3.5 and castable(SB.SomethingElse) then
	cast(SB.SomethingElse)
	return true
end
```

##  cooldown_duration
?> cooldown_duration : Used to return how long spell will be on cooldown.
```lua
local Rampage = -spell(184367).cooldown_duration
print(Rampage)

-- you can do some math knowing cooldown duration of spell
```

##  exists
?> exists : Used to return is spell exists. [Not used anymore]
```lua
local Rampage = -spell(184367).exists
if Rampage then ... end
```

##  casting_remains
?> casting_remains : Used to return remains cast time.
```lua
local FrostBolt = -spell(116).casting_remains
if FrostBolt < 1.5 then 
-- do stuff if our FrostBolt cast end's after 1.5 seconds
end
```

##  castingtime
?> castingtime : Used to return how long cast would be.
```lua
local FrostBolt = -spell(116).castingtime
if FrostBolt > 2.25 then ... end

-- you can do some math knowing casting time of certain spell
```

##  charges
?> charges : Used to return spell actual charges.
```lua
local RagingBlow = -spell(85288).charges

if -spell(85288).charges >= 2 and castable(85288) then  -- we cast 85288 two times here, then it will have one charge reserved.
	cast(85288, target)
	return true
end
```

##  fractionalcharges
?> fractionalcharges : Used to return spell fractional charges.
```lua
local RagingBlow = -spell(85288).fractionalcharges
if RagingBlow > 1.75 then ... end


if -spell(85288).fractionalcharges >= 1.75 and castable(85288) then -- if current fractional charge of 85288 == 1.75 (almost regenerated other charge) we cast it.
	cast(85288, target)
	return true
end
```

##  recharge
?> recharge : Used to return how long spell will be recharged.
```lua
local RagingBlow = -spell(85288).recharge
if RagingBlow < 0.85 then ... end
```

##  recharge_duration
?> recharge_duration : Used to return spell recharge duration.
```lua
local RagingBlow = -spell(85288).recharge_duration
print(RagingBlow)
```

##  full_recharge_time
?> full_recharge_time : Used to return spell recharge time to full charges.
```lua
local RagingBlow = -spell(85288).full_recharge_time
if RagingBlow > 3 then ... end
```

##  lastcast
?> lastcast : Used to check is this spell lastcast'ed.
```lua
local RagingBlow = -spell(85288).lastcast

if not -spell(85288).lastcast and castable(85288) then 
	cast(85288, target)
	return true
end
```

##  castable
?> castable : Used to check is this spell can be casted atm.
```lua
local RagingBlow = castable(85288)

if castable(85288) then
	cast(85288, target)
	return true
end
```

##  current
?> current : Used to check current spell cast.
```lua
local FrostBolt = -spell(116).current
if -spell(116).current then 
	-- do something if our current spell 116, or if called like target.spell(116).current we check other unit.
end
```
