# :fas fa-bone fa-fw: Combat Routine 

!> Main routine skeleton

```lua
local  addon, dark_addon = ...
local support = dark_addon.support
local SB = {} -- just spellbook table, maybe anything or even not exist lol
local Holy = {} -- table to insert funcs inside to dark_addon space or something like tha 
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

SB.Exorcism = 12345 -- example of usage, spell table can be whatever u like
SB.Crusader = 12345 -- example of usage, spell table can be whatever u like

Holy.stuff = function() -- function in space dark_addon
end


local function combat() -- function that run's while we in fight

if target.exists and target.alive and target.enemy then

	if toggle('cooldowns', false) then	-- toggle fetch state of ui buttons, like: master_toggle , interrupts , cooldowns
		if player.buff(SB.Crusader).down and castable(SB.Crusader) then
			cast(SB.Crusader)
			return true
		end
	end

	if castable(SB.Exorcism) then 
		cast(SB.Exorcism, target)
		return true
	end

end

end

local function resting() -- function that run's while we in chilling not in fight

	if player.buff(12345).down and castable(12345) then
		cast(12345, player)
		return true
	end

end

local function interface()
  local settings = {
    key = "holypal_settings",	--- any string that represent your profile key, anything be fetchid
    title = "Holy Paladin", 	--- Profile name
    width = 350,				--- window width
    height = 950,				--- window height
    resize = true,				--- window can be resize
    show = false,				--- show window after load? (or i fucking idk lmaop jkek drink fox%dogs whiskey lfmao)
    template = {
      {type = "header", text = "Holy Paladin - Settings", align = "center"},
	  { key = 'RampUp', type = 'dropdown', text =  " RampUp Incoming Damage [NoAuto]", desc = '', default = 'Empty', list = KeyBinds },
    }
  }

  configWindow = dark_addon.interface.builder.buildGUI(settings)

  dark_addon.interface.buttons.add_toggle(
    {
      name = "settings",
      label = "Rotation Settings",
      font = "dark_addon_icon",		-- if u want use FlexIconN(id, size1, size2) in label remove font to something like: font = ""
      on = {
        label = dark_addon.interface.icon("cog"), --- Here just use FlexIconN(123, 35,35) in case of icon, or if text label = "text1\nline2"
        color = dark_addon.interface.color.pink,	--- color check dark_addon.interface.color. manual ty <3
        color2 = dark_addon.interface.color.ratio(dark_addon.interface.color.dark_pink, 0.7) --- color check dark_addon.interface.color. manual ty <3
      },
      off = {
        label = dark_addon.interface.icon("cog"), -- same above
        color = dark_addon.interface.color.red,
        color2 = dark_addon.interface.color.red
      },
      callback = function(self)
        if configWindow.parent:IsShown() then -- if window shown wee hide that, by default shown
          configWindow.parent:Hide()
        else
          configWindow.parent:Show() -- if not show window u know.
        end
      end
    }
  )
end

dark_addon.rotation.register(
  {
    spec = dark_addon.rotation.classes.paladin.holy, -- open butwhy/core/rotation/rotation.lua then check name table, you wont miss it belive.
    name = "holypal", 								 -- key name, that used to load like: /fd load holypal
    label =  FlexIconN(228, 15, 15).." Hpala ", 	 -- just text after key, in this cast "holypal '- anything you type in label'"
    gcd = GCD, 										 -- [deprecated]
    combat = combat, 								 -- says itself
    resting = resting, 								 -- says itself
    interface = interface  						     -- says itself
  }
)

for _, func in pairs(Holy) do
    setfenv(func, dark_addon.environment.env) -- we place tablke Holy in dark_addon space to allow it use special funcs.
end
```
