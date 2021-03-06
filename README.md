<div align='center'>
    <h1>squash</h1><br>
</div>

`squash` is a dead simple theme manager for unix systems.
Themes are defined in pure shell scripts, allowing for squash to be both flexible and increadibly simple.
`squash` takes theme information, applies it to active applications,
and writes files in various formats to be used by other programs.

Predefined themes are available in the `themes` directory.
Add your own themes using the `template` file.
When you are ready, change themes with:

```
squash <THEME>
```

Squash currently supports the following window managers:

* 2bwm
* bspwm
* windowchef

## Theory

Managing themes on unix systems can often be difficult.
Nearly every program stores their theme files in different locations
and in different formats.
Squash aims to consolidate theme information into a single location.
These files can then be used to quickly apply themes to the entire system.

## Installation

Installing and setting up squash should be fairly simple. Follow these steps:

1) Clone the repository:
    ```bash
    git clone https://github.com/JLErvin/squash
    ```

2) Create the theme directory and move themes there
    ```bash
    cd squash
    mkdir ~/.config/squash
    cp themes/* ~/.config/squash/
    ```

3) Set the defaults. Change the values in the `defaults` file

4) Source `squash` files for xorg. Add the following to the top of your `.Xresources`
    ```xdefaults
    #include ".cache/squash/x_colors"
    ```

5) Switch to your first theme!
    ```bash
    squash designr
    ```

## Configuration

### .Xresources

For colors to persist on new terminals, and for the colors to be used by `x` applications,
add the following to your `$HOME/.Xresources`

```xdefaults
#include ".cache/squash/x_colors"
```

### BSPWM

For bspwm to use variables define by squash, add the following to your `bspwmrc`

```bash
source "${HOME}/.cache/squash/colors"
bspc config normal_border_color "${BSPWM_NORMAL}"
bspc config focused_border_color "${BSPWM_FOCUSED}"
```

### Windowchef

Windowchef configuration is almost identical to bspwm configuration,
simply add the following to `windowchefrc`

```bash
source "${HOME}/.cache/squash/colors"

waitron wm_config internal_border_width 5
waitron wm_config internal_color_focused "${TWOBWM_FOCUS:1:7}"
waitron wm_config internal_color_unfocused "${TWOBWM_UNFOCUS:1:7}"

waitron wm_config border_width 10
waitron wm_config color_focused "${BG:1:7}"
waitron wm_config color_unfocused "${BG:1:7}"
```

This gives a double border look much like 2bwm.
Notice that in `windowchefrc` you must use hex colors
without the #, hence shortening the hex code.

### i3wm
Configuration for i3 requires you to have lines in your configuration file that
squash can find and modify. If you don't have lines like these already, add them
to your configuration file.
```
client.focused #ffffff #ffffff #ffffff #ffffff
client.focused_inactive #ffffff #ffffff #ffffff #ffffff
client.unfocused #ffffff #ffffff #ffffff #ffffff
client.urgent #ffffff #ffffff #ffffff #ffffff
bar {
    colors {
            statusline #ffffff
            separator #ffffff
            focused_workspace #ffffff #ffffff #ffffff
            active_workspace #ffffff #ffffff #ffffff
            inactive_workspace #ffffff #ffffff #ffffff
            urgent_workspace #ffffff #ffffff #ffffff
    }
}
```
