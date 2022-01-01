# armbian-settings

This repo is a helper to configure armbian settings accordingly to different needs.

In this repo it was used an Orange Pi PC and Armbian Focal xfce desktop , with kernel 5.10.60

### Topics

#### General Settings

##### Maintaining the board updated

First of all it's important to get the latest updates:

~~~bash
sudo apt update && sudo apt upgrade
~~~

Note1: After a fresh install i have to run the commands above two times, in the first one occurs some certifications issues.

Personal Note1: In the next installation I have to remember to capture the message and open a issue on armbian project.


##### Adjusting personal settings (keyboard, timezone, locale)

###### Keyboard main configuration:
~~~bash
sudo dpkg-reconfigure keyboard-configuration
# For Brazilian Standard ABNT2 choose the option --> Portuguese (Brazil) - Portuguese (Brazil, no dead keys)
~~~

###### Keyboard keymap config:

In some cases you may adjust the keymap config. The example below is to Standard ABNT2 deal correctly with tilde (~) and accents)(´^).
~~~bash
localectl set-keymap br-abnt2
~~~

###### Timezone config (Default UTC):

~~~bash
sudo dpkg-reconfigure tzdata
~~~

###### Locale config (Default en_US.UTF-8)

I think it's ok to use the default locale but if you wanna change:
~~~bash
sudo dpkg-reconfigure locales
~~~

Note: The command above to reconfigure locale may take some time to execute.

_Finishing the adjustments above itś interesting to `reboot` the machine_

##### Setting the sound output

To check the sound outputs available:
~~~bash
pacmd list-sinks | less
~~~

To change the sound output to hdmi:
~~~bash
# Change the sound output to HDMI
pacmd set-default-sink $(pacmd list-sinks | grep 'name:' | grep -i 'hdmi' | cut -f 2 -d: | tr -d '<> ')
~~~

This change is not persistent, to make it persistent add the command above in the file /etc/rc.local


##### Disable the desktop environment

Some apps, like retroarch, don't need desktop environment. Disabling the desktop environment is great to save CPU/GPU/memory resources.

~~~bash
sudo armbian-config
# Options: System --> Desktop --> Disable Desktop
~~~

If in some moment you need the desktop environment just run `startx` from the terminal. The "logout" option close the desktop environment.

##### Setting the numlock to "ON" at start up.

Add the lines below to the file /etc/rc.local
~~~bash
# Turn Numlock on for the TTYs:
for tty in /dev/tty[1-6]; do
    /usr/bin/setleds -D +num < $tty
done
~~~

##### Dealing with 4k video resolution

At this moment (2022-01-01), the kernel of stable version of armbian does not support 4k resolution.
This may cause black screen on connect the SBC to 4k resolution devices. To deal with that you could:
1. Change the kernel to some legacy or development option, or;
2. Force the resolution to 1080p

Here we will do the second option.

Add the line below to the file /boot/armbianEnv.txt
~~~bash
extraargs=video=HDMI-A-1:1920x1080@60
~~~

Note: Despite of this config turn OS functional at 1080p some apps may try to use 4k resolution.
Retroarch is one of them, and because of it you have to change configuration in retroarch.cfg to use the 1080p resolution.

##### Basic Editing files in linux
Every time you need to edit files in linux command line you could do these steps:
1. Type "nano" followed by the filename.
2. Edit the file.
3. Use the Ctrl-o command to save.
4. Use the Ctrl-x command to exit the text editor.
