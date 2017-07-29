# Keyboard switcher for Awesome WM with additional layouts

## Intro
Usually I use two keyboard layouts on my computer there are English and Russian layouts. But sometimes I need to write something on another language, for example: German.
But adding new keyboard layout was very annoying me. Because I have to press more than one time for changing my keyboard layout from Russian to English.
But with this widget I can configure additional layouts. When I press on buttons on keyboard only my primary layouts will be switching. But when I want to use additional layout, I just click right mouse button on keyboard widget and select one of additional layouts. You can see how it is work in the Screenshot section.

## Installing
Clone this repository to your Awesome WM configuration directory:
```
cd ~/.configs/awesome
git clone https://github.com/echuraev/keyboard_layout
```

## Usage
1. Add call of `keyboard_layout` module to your `rc.init`:
   ```
   local keyboard_layout = require("keyboard_layout")
   ```
2. Create instance of keyboard widget. You can choose between text and graphical layout label, see below. Primary layout you can set by passing it to the `tui_layout` or `gui_layout` functions. After, you can call some other functions e.g. `add_additional_layout` for setting some additional layouts. And when you add all necessary options to `kbdcfg` then you have to call `bind` functions. In this call all your settings will apply.

   2.1. Create text label:
   ```
   local kbdcfg = keyboard_layout.tui_layout({
                      layouts = {
                          {"English", "us" },
                          {"Русский", "ru" }
                      }
                  })
   kbdcfg.add_additional_layout("Deutsch",  "de")
   kbdcfg.add_additional_layout("Français", "fr")
   kbdcfg.bind()
   ```
   2.2. Create graphical label:
   ```
   local kbdcfg = keyboard_layout.gui_layout({
                      layouts = {
                          {"English", "us", beautiful.en_layout },
                          {"Русский", "ru", beautiful.ru_layout }
                      }
                  })
   kbdcfg.add_additional_layout("Deutsch", "de", beautiful.de_layout)
   kbdcfg.add_additional_layout("Français", "fr", beautiful.fr_layout)
   kbdcfg.bind()
   ```
3. Bind your mouse keys:
   ```
   -- Mouse bindings
   kbdcfg.widget:buttons(
    awful.util.table.join(awful.button({ }, 1, function () kbdcfg.switch() end),
                          awful.button({ }, 3, function () kbdcfg.menu:toggle() end))
   )
   ```
4. Bind your keyboard shortcuts:
   ```
   globalkeys = awful.util.table.join(globalkeys,
       -- Shift-Alt to change keyboard layout
       awful.key({"Shift"}, "Alt_L", function () kbdcfg.switch() end),
       -- Alt-Shift to change keyboard layout
       awful.key({"Mod1"}, "Shift_L", function () kbdcfg.switch() end)
   )
   ```

## Functions
`switch()` - this function switch one primary keyboard layout to the next primary layout.

`bind()` - this function applies all settings to the widget.
### Text label
`switch_by_name(keymap_name)` - this function mostly use for setting additional layouts. It get keymap name of layout what should be set.

`add_additional_layout(layout_name, keymap_name)` - this function adds additional layout to the widget.
### Graphical label
`switch_by_name(keymap_name, layout_image)` - this function mostly use for setting additional layouts. It get keymap name of layout what should be set.

`add_additional_layout(layout_name, keymap_name, layout_image)` - this function adds additional layout to the widget.

## Screenshots
Usage of gui_layout:
![Usage of gui_layout.gif](gui_usage.gif)

Usage of tui_layout
![Usage of tui_layout.gif](tui_usage.gif)

## Author
Egor Churaev egor.churaev@gmail.com

## Licence
MIT

## Flags icons
Icon with British flag I take from here: https://www.gosquared.com/resources/flag-icons/
