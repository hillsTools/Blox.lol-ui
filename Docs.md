## Core Library Structure

### Initialization
```lua
local library = loadstring(game:HttpGet("YOUR_SCRIPT_URL"))()
```

### Window Creation
```lua
local window = library:new({
    name = "UI Name",               -- Title of the window
    textsize = 12,                  -- Base text size
    font = "RobotoMono",            -- Font family
    color = Color3.fromRGB(225,58,81), -- Accent color
    size = UDim2.new(0, 500, 0, 606) -- Window dimensions
})
```

## Page System

### Creating Pages
```lua
local page = window:page({
    name = "Page Name",
    pointer = "optional_reference_name" -- For saving/loading
})
```

### Multi-Sections
```lua
local multisection = page:multisection({
    name = "Multi-Section Name",
    side = "left",                  -- "left" or "right"
    size = 200,                     -- Height in pixels
    pointer = "optional_reference_name"
})
```

## Section Elements

### Basic Section
```lua
local section = page:section({
    name = "Section Name",
    side = "left",                  -- "left" or "right"
    size = 200,                     -- Height in pixels
    pointer = "optional_reference_name"
})
```

## UI Components

### 1. Toggle
```lua
local toggle = section:toggle({
    name = "Toggle Name",
    def = false,                    -- Default state
    callback = function(state) 
        print("Toggle:", state) 
    end,
    pointer = "toggle_reference"
})
```

**Methods:**
```lua
toggle:set(true) -- Programmatically set state
```

### 2. Button
```lua
local button = section:button({
    name = "Button Text",
    callback = function()
        print("Button pressed!")
    end
})
```

### 3. Slider
```lua
local slider = section:slider({
    name = "Slider Name",
    def = 50,                       -- Default value
    min = 0,                        -- Minimum value
    max = 100,                      -- Maximum value
    rounding = false,               -- Round to integers
    ticking = false,                -- Snap to integer values
    measurement = "%",              -- Unit suffix
    callback = function(value)
        print("Slider value:", value)
    end,
    pointer = "slider_reference"
})
```

**Methods:**
```lua
slider:set(75) -- Set slider value
```

### 4. Dropdown
```lua
local dropdown = section:dropdown({
    name = "Dropdown Name",
    def = "Option1",                -- Default selection
    max = 4,                        -- Max visible options
    options = {"Option1", "Option2", "Option3"},
    callback = function(selected)
        print("Selected:", selected)
    end,
    pointer = "dropdown_reference"
})
```

**Methods:**
```lua
dropdown:set("Option2") -- Set selection
```

### 5. Multibox
```lua
local multibox = section:multibox({
    name = "Multibox Name",
    def = {"Option1"},              -- Default selections
    max = 4,                        -- Max visible options
    options = {"Option1", "Option2", "Option3"},
    callback = function(selected)
        print("Selected:", table.concat(selected, ", "))
    end,
    pointer = "multibox_reference"
})
```

**Methods:**
```lua
multibox:set({"Option1", "Option3"}) -- Set multiple selections
```

### 6. Buttonbox
```lua
local buttonbox = section:buttonbox({
    name = "Buttonbox Name",
    def = "Option1",                -- Default selection
    max = 4,                        -- Max visible options
    options = {"Option1", "Option2", "Option3"},
    callback = function(selected)
        print("Selected:", selected)
    end,
    pointer = "buttonbox_reference"
})
```

**Methods:**
```lua
buttonbox:set("Option3") -- Set selection
```

### 7. Textbox
```lua
local textbox = section:textbox({
    name = "Textbox Label",
    def = "",                       -- Default text
    placeholder = "Enter text...",  -- Placeholder text
    callback = function(text)
        print("Text entered:", text)
    end,
    pointer = "textbox_reference"
})
```

**Methods:**
```lua
textbox:set("New text") -- Set textbox content
```

### 8. Keybind
```lua
local keybind = section:keybind({
    name = "Keybind Name",
    def = Enum.KeyCode.RightShift,  -- Default key
    allowed = 1,                    -- 1=allow mouse buttons, 0=keyboard only
    callback = function(key)
        print("Key pressed:", key)
    end,
    pointer = "keybind_reference"
})
```

**Methods:**
```lua
keybind:set(Enum.KeyCode.F) -- Change keybind
```

### 9. Color Picker
```lua
local colorpicker = section:colorpicker({
    name = "Color Picker",
    cpname = "Color Options",       -- Picker title
    def = Color3.fromRGB(255,0,0),  -- Default color
    callback = function(color)
        print("Selected color:", color)
    end,
    pointer = "color_reference"
})
```

**Methods:**
```lua
colorpicker:set(Color3.fromRGB(0,255,0)) -- Set color
colorpicker:set({255,0,0}) -- Alternative RGB format
```

### 10. Config Loader
```lua
local configloader = section:configloader({
    folder = "MyConfigs/"           -- Folder path for configs
})
```

## Utility Components

### Watermark
```lua
local watermark = window:watermark()

-- Update watermark content
watermark:update({
    FPS = "60",
    Ping = "25ms",
    User = "Player1"
})

-- Change position
watermark:updateside("topright") -- "topright", "topleft", "bottomright", "bottomleft"

-- Toggle visibility
watermark:toggle(true)
```

### Loader Screen
```lua
local loader = library:loader({
    name = "Script Loader",
    scriptname = "Universal",
    closecallback = function()
        print("Loader closed")
    end,
    logincallback = function()
        print("Login successful")
    end
})

loader:toggle() -- Show loader
```

## Configuration Management

### Saving Config
```lua
local config = window:saveconfig()
writefile("config.cfg", config)
```

### Loading Config
```lua
window:loadconfig("config.cfg")
```

## Complete Example

```lua
local library = loadstring(game:HttpGet("YOUR_SCRIPT_URL"))()

-- Create window
local window = library:new({
    name = "Advanced Script Hub",
    textsize = 13,
    font = "RobotoMono",
    color = Color3.fromRGB(225, 58, 81),
    size = UDim2.new(0, 550, 0, 650)
})

-- Main page
local mainPage = window:page({name = "Main", pointer = "mainpage"})

-- Combat section
local combatSection = mainPage:section({
    name = "Combat",
    side = "left",
    size = 250,
    pointer = "combat_section"
})

-- Combat toggles
combatSection:toggle({
    name = "Kill Aura",
    def = false,
    callback = function(state)
        print("Kill Aura:", state)
    end,
    pointer = "killaura"
})

combatSection:slider({
    name = "Hit Distance",
    def = 10,
    min = 5,
    max = 25,
    rounding = true,
    callback = function(value)
        print("Distance:", value)
    end,
    pointer = "hitdistance"
})

-- Visuals page
local visualsPage = window:page({name = "Visuals"})

-- ESP section
local espSection = visualsPage:section({
    name = "ESP",
    side = "left",
    size = 300
})

espSection:colorpicker({
    name = "ESP Color",
    def = Color3.fromRGB(255, 0, 0),
    callback = function(color)
        print("ESP Color:", color)
    end,
    pointer = "espcolor"
})

espSection:dropdown({
    name = "ESP Type",
    def = "Box",
    options = {"Box", "Name", "Health", "Both"},
    callback = function(selected)
        print("ESP Type:", selected)
    end
})

-- Settings page
local settingsPage = window:page({name = "Settings"})

-- Keybinds section
local keybindsSection = settingsPage:section({
    name = "Keybinds",
    side = "left"
})

keybindsSection:keybind({
    name = "Menu Toggle",
    def = Enum.KeyCode.RightShift,
    callback = function(key)
        print("Menu key:", key)
    end
})

-- Config section
local configSection = settingsPage:section({
    name = "Configuration",
    side = "right",
    size = 200
})

configSection:configloader({
    folder = "MyScriptConfigs/"
})

-- Add watermark
local watermark = window:watermark()
watermark:update({
    FPS = "60",
    Ping = "25ms",
    User = game.Players.LocalPlayer.Name
})
watermark:updateside("topright")
```
