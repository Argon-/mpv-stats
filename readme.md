mpv-stats
---------
Display statistics for the currently played file.

You can change the font formatting by creating a file `stats.conf` in a folder
named `lua-settings` within your mpv folder.
Please refer to the `o` table within the script for possible option names and 
consult [mpv manual](http://mpv.io/manual/master/#configuration) regarding 
configuration syntax.

Usage
-----
Place `stats.lua` in your `~/.config/mpv/scripts/` or `~/.mpv/scripts/` folder
to autoload the script.
Alternatively load it with `--script=<path>`.

The script is binding itself to `i` (however, not overriding your own bindings)
and can therefore be invoked with this key.
You can create different bindings by adding `<yourkey> script_binding stats` to
`input.conf`.
