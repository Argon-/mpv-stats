Note
====
This script is now part of mpv and, therefore, **not updated in this repo as of Nov 2018.** 
For an up to date version please visit: https://github.com/mpv-player/mpv/blob/master/player/lua/stats.lua

*You do not need to download it here* unless you want a specific version, e.g. 
because you are using an old version of mpv (you shouldn't).  
In such a case, start mpv with `--load-stats-overlay=no` in order to disable the 
internal version and place your desired script version at the locations mentioned below.

[There's also some documentation available](https://mpv.io/manual/master/#stats).


mpv-stats
=========
Display statistics for the currently played file in mpv.

![Default](https://cloud.githubusercontent.com/assets/540920/16775632/85da9aa6-489c-11e6-8333-176755e64892.jpg)
(screenshot is outdated)

Requirements
============

mpv 0.28.0 **is not sufficient**. You need a more recent version of mpv. 
For older mpv versions please go to [Releases](https://github.com/Argon-/mpv-stats/releases).
The oldest supported version of mpv is 0.9.3.

By default *Source Sans Pro* is used as font.
[You can download it here](https://github.com/adobe-fonts/source-sans-pro).  
If you want to use your own, please make sure your alternative choice supports
as many font weights and monospaced digits, for an optimal visual experience.


Usage
=====
Place `stats.lua` in your `~/.config/mpv/scripts/` or `~/.mpv/scripts/` folder
to autoload the script.

The script is binding itself to `i` and `I` (however, not overriding your own
bindings) and can therefore be invoked by pressing these keys.
`i` will show the stats once while `I` will toggle them.

While the stats are visible on screen, you can use numeric keys (1, 2, 3, ...)
to switch between "pages" of stats. So far, the following pages are defined:

1. stats (as usual)
2. frame timings

There will be more pages in the future.
Also, expect some layout changes of current pages in the near future.

You can set different bindings either by [customizing](#customization) this script
or by using the `script_binding` input command (in `input.conf`), e.g.:

    e script-binding stats/display-stats
    E script-binding stats/display-stats-toggle


F.A.Q.
======

### How to get graphs?

Graphs are enabled by default.
Due to their size, graphs for `Frame Timings` can only be shown on their dedicated page (2).
For `VSync Ratio` and `VSync Jitter` they are only shown when stats are toggled (page 1)
because they need to be recorded.
Please note that only the `opengl` VO is exposing frame timing data.

Turn graphs off with `plot_perfdata=no`, `plot_vsync_ratio=no` and `plot_vsync_jitter=no` (see [Customization](#customization)).


### The graph's position is jumping

Please use a font with monospaced digits.
The default font does meet this requirement. Either download it (see [Usage](#usage))
or set your own with `font_mono` (see [Customization](#customization)).  
Note that `font` does not need to be a monospaced font.


Customization
=============
You can configure various settings by creating a file called `stats.conf` in a folder
named `lua-settings` within your mpv config folder (where your `mpv.conf` is in).
Please refer to the `o` table within the script for possible option names and
consult [mpv manual](http://mpv.io/manual/master/#config-syntax) regarding
configuration syntax.

To change e.g. the text display duration your `stats.conf` may look like:

    duration=5

A more sophisticated example:

    key_oneshot=e
    key_toggle=E
    font_size=8
    plot_perfdata=no
    font=Arial
    font_mono=Monospaced
    font_color=262626
    border_size=0.5

Note: colors are given as hexadecimal values and use
[ASS tag](http://docs.aegisub.org/3.2/ASS_Tags/#\c) order: BBGGRR (blue green red).
