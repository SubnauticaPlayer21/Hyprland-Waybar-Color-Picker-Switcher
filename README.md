# Hyprland-Waybar-Color-Picker-Switcher
Lets you change the color of your hyprland borders and waybar using a color picker. For Arch




# make your hyprland.conf look sorta like this:
   bind = SUPER CTRL, F9, exec, ~/Scripts/accent.sh pick
   windowrule = float, title:^Accent color$
   windowrule = size 420 480, title:^Accent color$
   windowrule = center, title:^Accent color$:


Yeah and uhhh its cool and stuff. Keybind is super + ctrl + f9 More detailed setup below:

## Setup

### 1. Install

```bash
sudo pacman -S zenity libnotify
mkdir -p ~/Scripts
cp accent.sh ~/Scripts/
chmod +x ~/Scripts/accent.sh
```

### 2. Hyprland

The script writes the color to `~/.config/hypr/accent.lua`. Load it in `hyprland.lua` and use it for borders:

```lua
local accent = dofile(os.getenv("HOME") .. "/.config/hypr/accent.lua")
-- e.g. col.active_border = accent
```

Add the keybinds and window rule:

```lua
bind(mainMod .. " + F9", hl.dsp.exec_cmd("~/Scripts/accent.sh"), "Cycle accent")
bind(mainMod .. " + CTRL + F9", hl.dsp.exec_cmd("~/Scripts/accent.sh pick"), "Pick accent")

hl.window_rule({
  name = "accent-picker",
  match = { title = "^Accent color$" },
  float = true,
  size = "420 480",
  center = true,
})
```

### 3. Waybar

Add to the top of `~/.config/waybar/style.css`:

```css
@import "accent.css";
```

Use `@accent` wherever you want the color:

```css
#workspaces button.active { color: @accent; }
```

### 4. Usage

```bash
accent.sh            # cycle presets
accent.sh pick       # open color wheel
accent.sh ff4081     # set a hex color
accent.sh orange     # set a preset
```
