# :fas fa-brands fa-sketch fa-fw: Misc 

!> Called from addon space.

## settings.store
?> settings.store : Used to save settings.
```lua
dark_addon.settings.store(key, value)
```

## settings.fetch
?> settings.fetch : Used to get settings.
```lua
dark_addon.settings.fetch(key, default)
```

## Example: <!-- {docsify-ignore} -->

```lua
-------------- Example -------------------
state = 0
dark_addon.settings.store('ssc', state)
------------------------------------------
stateval = dark_addon.settings.fetch('ssc') 
if stateval == 2 then ...
------------------------------------------
```

## setfenv
?> setfenv : Default Lua function.

?> Here we just change 'test' function env to addon env, so now we can use addon function in there.
```lua
local function test()
	if player.buff(1234).up then 
		return true 
	end
	return false
end
setfenv(test, dark_addon.environment.env)
```