# i3wm

## Install and Config

To configure the i3wm to use in an Armbian Desktop (with XFCE)

1. Install the necessary packages

~~~bash
# i3: main package
sudo apt install i3

# i3status: status bar of i3wm
sudo apt install i3status

# suckless-tools: tools for wm that includes dmenu
sudo apt install suckless-tools
~~~

2. Disable Desktop Environment with `armbian-config`

3. Create in you user home a file `~/.xinitrc` with this line:

`exec i3`

4. Now, when you run `startx` the i3wm will be initiated


## Quick usage:

 - win + enter: Open the terminal emulator

 - win + d: Dmenu prompt to open an installed app with autocomplete

 - win + shift + q: Close the window

 - win + shift + e: Exit i3wm (will prompt to confirm exit)

For more information run `man i3`
