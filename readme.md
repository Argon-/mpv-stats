mpv-stats
=========
Display statistics for the currently played file in mpv.

![Default](https://cloud.githubusercontent.com/assets/540920/16775632/85da9aa6-489c-11e6-8333-176755e64892.jpg)

Requirements
============

The latest version of this script requires mpv version **0.26.0** or above (or at least [newer than this 0.25 commit](https://github.com/mpv-player/mpv/commit/6a12b1fdc3c5c70fed15734c02f65005db2835cd)).  
For older mpv versions please go to [Releases](https://github.com/Argon-/mpv-stats/releases).
The oldest supported version of mpv is 0.9.3.


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

By default *Source Sans Pro* is used as font.
[You can download it here](https://github.com/adobe-fonts/source-sans-pro).


F.A.Q.
======

### How to get graphs?

Graphs are enabled by default.
Due to their size, graphs for `Frame Timings` can only be shown on their dedicated page (2).
For `VSync Ratio` and `VSync Jitter` they are only shown when stats are toggled (page 1)
because they need to be recorded.
Please note that only the `opengl` VO is exposing frame timing data.

Turn graphs off with `plot_perfdata=no`, `plot_vsync_ratio=no` and `plot_vsync_jitter=no` (see [Customization](#customization)).

### Why are my frame timing values colored?

**Red**: your hardware needs more time to render/present/upload a frame than available.  
**Yellow**: your hardware needs more than 85% of the available time.
This is merely a warning.

When using
[display-resample](https://mpv.io/manual/stable/#options-video-sync) and/or
[interpolation](https://mpv.io/manual/stable/#video-output-drivers-interpolation)
mpv has to show (render/present/upload) one frame every `1/display-fps` seconds.
In case of a 60Hz display this means there's `1/60 = 0.016666` sec (`16666` μs) time
per frame available.  
Given [display-resample](https://mpv.io/manual/stable/#options-video-sync)
is not used the video's FPS will be used for these calculations.
Note that there are further parameters and coherences
(depending on user configuration) influencing fluent playback and this is
just a very general indicator.

Turn it off by setting `timing_warning=no` (see [Customization](#customization)).  
Use `timing_warning_th=0.85` to set a factor determining when to warn (yellow).

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
    print_perfdata_total=yes
    font=Arial
    font_mono=Monospaced
    font_color=262626
    border_size=0.5

Note: colors are given as hexadecimal values and use
[ASS tag](http://docs.aegisub.org/3.2/ASS_Tags/#\c) order: BBGGRR (blue green red).
