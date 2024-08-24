# :fas fa-life-ring fa-fw: Support 

!> Called from **dark_addon**.support.FUNCTION_NAME

## W_Enchant
> W_Enchant : Used to check do we had enchant on our weapon by id.
```lua
local Earth_Weapon = W_Enchant(6498)
if Earth_Weapon then ... end
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.W_Enchant = function(enchantId)
    local hasEnchant = false
    local _, _, _, mainEnchantId, _, _, _, offEnchantId = GetWeaponEnchantInfo()
    if mainEnchantId == enchantId or offEnchantId == enchantId then
        hasEnchant = true
    end
    return hasEnchant
end
```
</details>


## t_check
> t_check : Used to check trinket state by id.
```lua
local SEB_slot, _, SEB_Ready = t_check(194302) -- Storm-Eater's Boon
if SEB_Ready then
	macro('/use '.. SEB_Ready)
end
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.t_check = function(itemID)
    for i = 13, 14 do -- iterate over trinket slots
        local itemLink = GetInventoryItemLink("player", i)
        if itemLink and tonumber(string.match(itemLink, "item:(%d+)")) == itemID then
            local startTime, duration, isEnabled = GetItemCooldown(itemLink)
            if duration > 0 then
                local remainingTime = duration - (GetTime() - startTime)
                return i, remainingTime, false -- return slot number, remaining cooldown time, and false (on cooldown)
            else
                return i, 0, true -- return slot number, 0 (no cooldown), and true (ready to use)
            end
        end
    end
    return nil, nil, nil -- return nil if trinket is not equipped
end
```
</details>



## GroupType
> GroupType : Used to get current group type.
```lua
local GroupType = support.GroupType
if GroupType=="raid" then ...
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.GroupType = function()
  return IsInRaid() and "raid" or IsInGroup() and "party" or "solo"
end
```
</details>




## getTanks
> getTanks : Used to get current tanks in party.
```lua
local tank1, tank2 = support.getTanks
if not tank1.alive and tank2.alive then ....
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.getTanks = function()
  local tank1 = nil
  local tank2 = nil

  local group_type = support.GroupType()
  local members = GetNumGroupMembers()
  for i = 1, (members - 1) do
    local unit = group_type .. i
    if (UnitGroupRolesAssigned(unit) == "TANK") and not UnitCanAttack("player", unit) and not UnitIsDeadOrGhost(unit) then
      if tank1 == nil then
        tank1 = unit
      elseif tank2 == nil then
        tank2 = unit
        break
      end
    end
  end
  --print("The two tanks are: " .. tank1.name .. ", " .. tank2.name)
  if tank1 ~= nil then
    tank1 = dark_addon.environment.conditions.unit(tank1)
  end
  if tank2 ~= nil then
    tank2 = dark_addon.environment.conditions.unit(tank2)
  end
  return tank1, tank2
end
```
</details>




## castGroupBuff
> castGroupBuff : Used to count buff if min_value < desired_value, return true.
```lua
local Power_Word_Fortitude = support.castGroupBuff(21562, 5)
if not Power_Word_Fortitude then ...
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.castGroupBuff = function(buff, min)
  local count = 0
  local group_type = support.GroupType()
  local members = GetNumGroupMembers()
  if group_type == "solo" then
    return min == 1 and not hasBuff("player", buff)
  end
  for i = 1, (members - 1) do
    if not hasBuff(group_type .. i, buff) then
      count = count + 1
      if (count >= min) then
        return true
      end
    end
  end
  return false
end
```
</details>





## iknow
> iknow : Used to check do we know spell or talent, by spell_id.
```lua
local Power_Word_Fortitude = support.iknow(21562)
if Power_Word_Fortitude then ...
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.iknow = function(spellID)
isKnown = IsPlayerSpell(spellID, isPetSpell)
	if isKnown == true then
		return true 
			else 
		return false 
	end
end
```
</details>






## name
> name : Used to get spell_name, by spell_id.
```lua
local Power_Word_Fortitude = support.name(21562)
print(Power_Word_Fortitude)
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.name = function(spell)
spell = select(1, C_Spell.GetSpellInfo(spell).name)
	return spell
end
```
</details>







## GetMovementDuration
> GetMovementDuration : Used to display how long we move.
```lua
local move_for = support.GetMovementDuration()
if move_for > 2.5 then ...
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.GetMovementDuration = function()
 if player.moving then
        if not moving then
            moving = true
            moveTime = GetTime()
        end
        duration = math.floor((GetTime() - moveTime) * 10) / 10 -- duration in seconds, rounded to 1 decimal place
    else
        if moving then
            moving = false
            local result = duration
            duration = 0
            return result
        end
    end
    return duration
end
```
</details>








## lowest_target
!> Possible be removed cause its garbage.
> lowest_target : Used to get alive lowest unitID.
```lua
local AliveLowest_unitID = support.lowest_target()
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.lowest_target = function()
if lowest.alive then
	return lowest.unitID
end
end
```
</details>









## buffable_table
> buffable_table : Used to get table of units without certain buff.
```lua
local Regrowth_table = support.buffable_table(SB.Regrowth)

for _, unit in ipairs(Regrowth_table) do
	if not UnitIsDeadOrGhost(unit.unitID) and UnitIsConnected(unit.unitID) and unit.castable(SB.Regrowth) and unit.distance <= 25 then
		cast(SB.Regrowth, unit)
		return true
	end
end
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
local function collect_buffable_units(spell)
  local units = {}
  for unit in dark_addon.environment.iterator() do
    if unit and unit.alive and unit.buff(spell).down then 
      table.insert(units, unit)
    end
  end
  return units
end

function group:buffable_units(spell)
  return collect_buffable_units(spell)
end

support.buffable_table = function(spell)
	return group:buffable_units(spell)
end
```
</details>










## buffed_table
> buffed_table : Used to get table of units with certain buff.
```lua
local WildGrowth_table = support.buffed_table(SB.WildGrowth)
	for _, unit in ipairs(WildGrowth_table) do
		if not UnitIsDeadOrGhost(unit.unitID) and UnitIsConnected(unit.unitID) and unit.castable(SB.Swiftmend) and unit.distance <= 25  and unit.health.percent <= 90 then
			cast(SB.Swiftmend, unit)
			return true
		end
	end
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
local function collect_buffed_units(spell)
  local units = {}
  for unit in dark_addon.environment.iterator() do
    if unit and unit.alive and unit.buff(spell).up then 
      table.insert(units, unit)
    end
  end
  return units
end

function group:buffed_units(spell)
  return collect_buffed_units(spell)
end

support.buffed_table = function(spell)
  return group:buffed_units(spell)
end
```
</details>











## CreateMacro
> CreateMacro : Used to create macros on character.
```lua
	CreateMacroIfNotExist("DISP", "/fd toggle dispel")
```

<details>
<summary>Function code. (Click to expand)</summary>

 
```lua
support.CreateMacro = function(macroName, macroCommand)
    if GetMacroIndexByName(macroName) == 0 then
        CreateMacro(macroName, "INV_MISC_QUESTIONMARK", macroCommand, 1)
    end
end
```
</details>

