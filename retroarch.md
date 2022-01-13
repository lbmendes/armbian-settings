# Retroarch

Guide to use retroarch.

Based in an a setup with a SBC Orange Pi PC (H3) with armbian (kernel 5.10.60)

## Install

1. Add the libretro repository:
~~~bash
sudo add-apt-repository ppa:libretro/stable
~~~

2. Update your repo:
~~~
sudo apt update
~~~

3. Install retroarch
~~~bash
sudo apt install retroarch
~~~


## Config

1. Open retroarch to load the initial settings, and then quit.
~~~bash
retroarch
~~~

2. OPTIONAL: Change the file `~/.config/retroarch/retroarch.cfg` to set 1080p resolution. This will prevent to load 4k resolution. Edit these lines:
~~~
custom_viewport_height = "1080"
custom_viewport_width = "1920"
video_fullscreen = "true"
video_fullscreen_x = "1920"
video_fullscreen_y = "1080"
video_window_auto_height_max = "1080"
video_window_auto_width_max = "1920"
~~~

3. OPTIONAL: Copy your .bin BIOS files to the retroarch system folder:
```bash
cp -v ~/retrogames/BIOS/*.bin ~/.config/retroarch/system/
```

4. Open retroarch again and update all things in the settings menu. After that you are ready to install cores and play games.


## Core specifics:


### pcsx_rearmed (PSONE)

The version of core pcsx_rearmed installed by retroarch is not the correct version for arm32bits architecture. This causes crashes and low speed.

To install this core manually, do these steps:

1. Clone the core repository:
~~~bash
mkdir -p ~/retrogames/git
cd ~/retrogames/git
git clone https://github.com/libretro/pcsx_rearmed.git
cd pcsx_rearmed/
~~~

2. Build the core:
~~~bash
make -f Makefile.libretro platform='armv-cortexa7-neon' clean
make -f Makefile.libretro platform='armv-cortexa7-neon'
~~~

3. Copy the .so file to the retroarch cores folder:
~~~bash
cp pcsx_rearmed_libretro.so ~/.config/retroarch/cores/
~~~
