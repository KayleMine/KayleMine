# :fas fa-keyboard fa-fw: modifiers 

!> Called from combat routine.

## modifiers type's
?> Any:
```lua
shift
control
alt
```
?> Certain:
```lua
lshift
lcontrol
lalt
rshift
rcontrol
ralt
```

## modifier
?> modifier : Used to check are we holding key atm.
```lua
if modifier.control then ...

local ElysianDecrees = dark_addon.settings.fetch("dh_settings_ElysianDecree") -- dh_settings are profile key ; ElysianDecree settings key

if (ElysianDecrees == "shift" and modifier.shift) or (ElysianDecrees == "control" and modifier.control) or (ElysianDecrees == "alt" and modifier.alt) then
	-- do stuff, while selected key holded.
end
```
