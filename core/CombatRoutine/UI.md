# :fas fa-box fa-fw: Combat Routine - UI

!> UI - How to?
 
## Base for interface
```lua

local function interface()

   local settings = {
        key = 'bruho_meho',			-- profile key (PK), we fetch setting with PK+Settings_Key
        title = 'Especial name',	-- Window title text
        width = 300,				-- Window width
        height = 720,				-- Window height
        resize = true,				-- Window can be resized? (Click and drag)
        show = false,				-- Window shown on load? (/reload too)
        template = {
			-- here we go mario	
		},
	}
	
	configWindow = dark_addon.interface.builder.buildGUI(settings) -- build template
	
    dark_addon.interface.buttons.add_toggle({					   -- Button to open settings 
        name = 'settings',
        label = 'Rotation Settings',
        font = 'dark_addon_icon',
        on = {
            label = dark_addon.interface.icon('cog'),
            color = dark_addon.interface.color.green,
            color2 = dark_addon.interface.color.green
        },
        off = {
            label = dark_addon.interface.icon('cog'),
            color = dark_addon.interface.color.red,
            color2 = dark_addon.interface.color.red
        },
        callback = function(self)
            if configWindow.parent:IsShown() then
                configWindow.parent:Hide()
            else
                configWindow.parent:Show()
            end
        end
    })

end
```


## Button for interface
```lua
	dark_addon.interface.buttons.add_toggle(
		{
			name = "battleres",                                -- unique key to fetch is it enaled, via: toggle('battleres', false)
			label = "Use battleres on FOCUS",				   -- label text, explain what is that shit on hover
			on = {
				label = "BR\nON", -- shown while toggle'd on.
				color = dark_addon.interface.color.orange,
				color2 = dark_addon.interface.color.orange
			},
			off = {
				label = "BR\nOFF", -- shown while not toggle'd.
				color = dark_addon.interface.color.red,
				color2 = dark_addon.interface.color.ratio(dark_addon.interface.color.dark_grey, 0.5)
			}
		}
	)
```


## checkspin
?>  how to fetch?: 
```lua
-- P.S without []
local C_Check               = dark_addon.settings.fetch("[YOUR_PROFILE_KEY]_[ITEM_KEY].check", false) -- false mean default check state.
local C_CPercent             = dark_addon.settings.fetch("[YOUR_PROFILE_KEY]_[ITEM_KEY].spin", 55) -- 55 mean default value in spinner.
```
?>   what do we place in template?:
```lua
{ key = "[ITEM_KEY]", type = "checkspin", text = " MP%", desc = "", default_check = false, default_spin = 55, min = 5, max = 100, step = 1 },
-- key is key we fetch, type represent what do we use here, text anything, desc anything, default_check false or true, default_spin aka value anything, max suggest from 0 to 100 but you can from -1000 to 9999 ofc, set per m3 slide up\down we move to 1 value.
```


## spinner
?>  how to fetch?: 
```lua
-- P.S without []
local DPSCSSwitch = dark_addon.settings.fetch('[YOUR_PROFILE_KEY]_[ITEM_KEY]', 90 )-- value 90 mean default spinner value.
```

?>  what do we place in template?:
```lua
{ key = "[ITEM_KEY]", type = "spinner", text = " Auto-Switch", default = "90", desc = "", min = 10, max = 100, step = 5 },
-- key is key we fetch, type represent what do we use here, text anything, desc anything, default_check value is what it set to, max suggest from 0 to 100 but you can from -1000 to 9999 ofc, set per m3 slide up\down we move to 1 value.
```


## checkbox
?>  how to fetch?: 
```lua
-- P.S without []
dark_addon.settings.fetch("'[YOUR_PROFILE_KEY]_[ITEM_KEY]'", false) -- false mean default check state.
```
?>  what do we place in template?:
```lua
{ key = "trinket_use1", type = "checkbox", text = "Use 1 on cd", desc = "", default_check = false},
-- key is key we fetch, type represent what do we use here, text anything, desc anything. default_check value is what it set to.
```


## dropdown Key's example
```lua
local KeyBinds = {
    { key = 'Empty', text = 'Unbound' },
    { key = 'control', text = 'Any:CTRL' },
    { key = 'lcontrol', text = 'Left CTRL' },
    { key = 'rcontrol', text = 'Right CTRL' },
    { key = 'alt', text = 'Any:ALT' },
    { key = 'lalt', text = 'Left ALT' },
    { key = 'ralt', text = 'Right ALT' },
    { key = 'shift', text = 'Any:SHIFT' },
    { key = 'lshift', text = 'Left SHIFT' },
    { key = 'rshift', text = 'Right SHIFT' },
	{ key = 'auto', text = 'Auto' },
}
```


## dropdown
?>  how to fetch?: 
```lua
-- P.S without []
local _RampUp = dark_addon.settings.fetch("[YOUR_PROFILE_KEY]_[ITEM_KEY]")
if _RampUp == 'Empty' then ....
```
?>  what do we place in template?:
```lua
{ key = 'RampUp', type = 'dropdown', text =  " RampUp Incoming Damage [NoAuto]", desc = '', default = 'Empty', list = KeyBinds }, -- to short, list are outside.
-- key is key we fetch, type represent what do we use here, text anything, desc anything, default value is what it set to, list table with key's (value).
```

## ruler
?>  straight line in where u placed it
```lua
{ type = "rule" },
```

## spacer
?>  paragraph or smthng like that?
```lua
{ type = "spacer", size = 2 }, -- 2 pixels. or idl lfmao
```

## text
?>  text section
```lua
{ type = "text", text = "my pretty text" },
```

## Header text
?>  just Header text section (bigger than text)
```lua
{ type = "header", text = "my pretty text" },
```

## input
?>  input, you can fetch whatever typed here
```lua
{type = "input", key = "inputkey", text = "test", width = 145.0},
-- fetch:
local input_string = dark_addon.settings.fetch([YOUR_PROFILE_KEY]_[ITEM_KEY], nil) -- nil default text value
```

## FlexIcon ; FlexIconN
?>  Place icon in any text [todo: make sing func...]
```lua
{ type = "text", text = FlexIcon(12345, 25,25) }, -- will insert icon with spell name
{ type = "text", text = FlexIconN(12345, 25,25) }, -- will insert icon without spell name
```
