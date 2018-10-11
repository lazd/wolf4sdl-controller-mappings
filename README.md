# wofl4sdl-controller-mappings
A selection of controller mappings for wolf4sdl

## Instalation

First, shut down wolf4sdl so it doesn't overwrite your config.

Next, copy the file corresponding to your gamepad into the `~/.wolf4sdl/` folder, renaming it to `config.wl6`.

Restart wolf4sdl and your controller will be mapped nicely.

## Controls

All controllers are mapped as follows:

* Left stick X axis: Strafe
* Left stick Y axis: Move forward/back
* Right stick X axis: Turn
* Left stick button: Run
* Right stick button: Run
* Left bumper: Previous weapon
* Right bumper: Next weapon
* Left trigger: Use
* Right trigger: Fire
* Select: Pause
* Start: Escape

The remaining 4 buttons (A, B, X, Y) can be remapped using the UI as you see fit. Note that this changes `config.wl6`, so be sure to back up your changed file.

## How to make your own mappings

I can't make a mapping for you unless you want to send me a free controller (for keeps), so don't bother asking.

Here's how to do it yourself, assuming you're on RetroPie:

First, set up wolf4sdl to build from source:

```
cd RetroPie-Setup/
sudo ./retropie_packages.sh wolf4sdl depends
sudo ./retropie_packages.sh wolf4sdl sources
sudo ./retropie_packages.sh wolf4sdl get_opts
sudo ./retropie_packages.sh wolf4sdl get_bins
```

Run this command, then note down which of your joysticks buttons are which (use `js1` etc if your joystick is not found):

```
jstest /dev/input/js0
```

Open `wl_play.cpp` for editing:

```
sudo nano ~/RetroPie-Setup/tmp/build/wolf4sdl/wl_play.cpp
```

Change the section that looks like this so your joystick buttons are in the right order. The first entry corresponds to the action that button 0 should take, the second for button 1, and so on. Be sure to have the exact number of items you started with, and use `bu_nobutton` for any button you don't wish to map:

```
#else
    bt_attack, bt_strafe, bt_use, bt_run, bt_prevweapon, bt_nextweapon, bt_use, bt_attack,
    bt_pause, bt_esc, bt_nobutton, bt_run, bt_run, bt_nobutton, bt_nobutton, bt_nobutton,
#endif
```

Then, build/install/configure and nuke the config files:

```
cd ~/RetroPie-Setup/
sudo ./retropie_packages.sh wolf4sdl build
sudo ./retropie_packages.sh wolf4sdl install
sudo ./retropie_packages.sh wolf4sdl configure
```

Don't forget make sure wolf4sdl is shut down (or it will overwrite your config), then delete your existing `config.wl6` files:

```
rm ~/.wolf4sdl/config.wl6
```

Finally, launch wolf4sdl and test our your new controls. When you quit, a new `~/.wolf4sdl/config.wl6` file will be written.

## Backup your controller mappings

You can back up your controls by doing:

```
cp ~/.wolf4sdl/config.wl6 ~/.wolf4sdl/config.wl6.bak
```

You can restore your controls by doing:

```
cp ~/.wolf4sdl/config.wl6.bak ~/.wolf4sdl/config.wl6
```

## Thanks

Thanks to dudeleyes from the Retropie forums for the [description of how to perform remapping and build wolf4sdl from source](https://retropie.org.uk/forum/topic/8695/wolfenstein3d-wolf4sdl-remapping/).

Thanks to Anish Desai for the [tutorial on button remapping](http://dosonthepi.blogspot.com/2015/01/configure-game-controllers-for-wolf4sdl.html).
