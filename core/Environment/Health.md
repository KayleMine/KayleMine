# :fas fa-heart fa-fw: health 

!> Called from combat routine.

##  percent
> percent : Used to return health percent.
```lua
if unit.health.percent <= 80 then ...

if lowest.health.percent <= 80 and castable(SB.HealingSpell) then
	cast(SB.HealingSpell, lowest)
	return true
end
```

##  actual
> actual : Used to return actual raw health.
```lua
if unit.health.actual <= 80000 then ...

if lowest.health.actual <= 80000 and castable(SB.HealingSpell) then
	cast(SB.HealingSpell, lowest)
	return true
end
```

##  effective
> effective : Used to return effective health.
```lua
if unit.health.effective <= 80 then ...

if lowest.health.effective >= 30 and castable(SB.HealingSpell) then
	cast(SB.HealingSpell, lowest)
	return true
end
```

##  incoming
> incoming : Used to return incoming healing to health.
```lua
if unit.health.incoming >= 50000 then ...

if lowest.health.incoming >= 50000 and castable(SB.LessHealingSpell) then
	cast(SB.LessHealingSpell, lowest)
	return true
end
```

##  missing
> missing : Used to return missing health.
```lua
if unit.health.missing >= 55 then ...

if lowest.health.missing >= 55 and castable(SB.EmergencyHeal) then
	cast(SB.EmergencyHeal, lowest)
	return true
end
```
