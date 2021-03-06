## Run-time engine setup

The engine Setup program allows the player to customize certain game
settings.

**NOTE:** currently a setup program is only available for Windows.

The options in the setup program are divided into two parts: _common_ and _advanced_.
The advanced options can be accessed by clicking the "Advanced" button.

### Graphics settings

**Driver**

Lets the player choose a graphics driver. Currently supported are Software
renderer (the old and slower option, but the only driver that fully supports 8-bit
games), Direct3D 9 and OpenGL (newer and faster drivers with hardware
acceleration, but without proper palette-based effects support).

**Start in a windowed mode**

If checked, the game will be run in windowed mode, as opposed to
fullscreen.

**Mode**

Lets the player choose a fullscreen display mode (otherwise shows the approximate
size of window the game will be running in). The list of modes depends
on the graphic card and the system's capabilities.

**Fullscreen scale**
**Windowed scale**

These two options determine the way the game will be scaled (when required)
in fullscreen and windowed modes respectively:

**None**. The game will be shown in its native resolution. Note that
low-resolution games will be running in a tiny window on modern
monitors, so this choice is more suitable for high-resolution games.

**Max round multiplier**. The game will be scaled up using a maximal
round integer (2, 3, 4, etc) multiplier with which it still fits inside
the screen.

**Stretch to fit screen**. The game will be stretched to fill the whole
screen. Note that if the game's native aspect ratio is different from the
screen's aspect ratio, the game graphics will appear deformed and indeed stretched.

**Stretch to fit screen (preserve aspect ratio)**. The game will be
stretched to screen borders while respecting the game's native aspect ratio
(width/height proportions). This ensures that the game graphics will always
look correct, but the option can lead to black borders at the left & right or
top & bottom sides of the screen.

**Scaling method**

Here the player can choose a game scaling algorithm (nearest-neighbor is
the simplest one). Some of the methods (notably Hqx) are restricted to
which scaling multiplier the player selected; if the multiplier is not enough to resize the
game on its own, the nearest-neighbor method will be applied
additionally. The list of available filters depend on graphics driver
selection.

### Gameplay settings

**Game language**

Here the player selects one of the available game translations.

### Advanced graphics options

**Vertical sync**

This option enables vertical synchronization mode, which reduces the
"tearing" effect on the game graphics, but the option may decrease the game running speed.

**Use 85 Hz display**

This option sets the monitor refresh rate to 85 Hz to run the game,
which eliminates flickering. However, this does not work on all monitors,
and not at all on flat panel displays, which is why it is disabled by
default.

**Smooth scaled sprites**

This option will apply anti-aliasing to scaled characters, in order to
give them a smoother look after the resizing. This can slow down the game
though, so it is off by default.

**Render sprites at screen resolution**

When enabled, characters and objects are scaled in screen pixels rather
than game pixels. What this means is that when a low-resolution game is
run in a larger window, the sprites will take advantage of this higher
resolution and look less pixelated when scaled down. This option may be
locked to a certain state by the game itself (according to author's
choice), in which case the player will not be able to change it.

### Sound options

**Digital sound**

Here the player may choose the digital audio driver, or disable digital
sound completely.

**MIDI music**

Here the player may choose the MIDI music playback method, or disable MIDI
music completely.

**Enable threaded audio**

When enabled, the engine will process audio on a separate thread. This results in a much smoother playback, but may potentially break the game's synchronization with the music (if it had one).

**Use voice pack if available**

When checked, this option enables voice speech in game (where
available).

### Mouse options

**Auto lock to window**

If this option is enabled, the mouse will be locked inside game window
whenever the player clicks on it or switches into game. The locked mouse
cannot leave the game window, making it impossible to accidentally jump out of the
game by mistake (by clicking on the desktop, for example). Naturally, this
option is only important if the game is run in windowed mode; when the game runs in
fullscreen mode, the mouse is always locked.

**Mouse speed**

This slider allows the player to set up the mouse cursor speed in game. It
should be noted that this parameter is only applied if the game is run
in fullscreen mode.

### Other advanced settings

**Sprite cache max size**

This option limits the maximum amount of memory that the game will use
for its sprite cache. The sprite cache is used to keep a partition of all
the game sprites loaded to the memory, thus reducing loading times
between rooms and preventing slowdowns during game play. Of course,
higher values make the game use more memory. Usually only
high-resolution games with long animations need to have this value
increased.

**Custom game saves path**

When unchecked, the game will store its saved games in the default Windows folder:
`C:/Users/<Username>/Saved Games/<Game Title>`.
Players may enable this option and define their own location to store
game saves.

**Custom game shared data path**

When unchecked, the game will store its shared files - custom
runtime data shared among all the users of this computer - in the default Windows folder:
`C:/Program Data/Adventure Game Studio/<Game Title>`.
Players may enable this option and define their own location to store
these game files.

*See also:* [Default setup (Editor Pane)](DefaultSetup), [Location of the configuration file on the system and options](RuntimeEngine) 
