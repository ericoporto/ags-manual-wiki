## Global functions (Palette Operations)

### `CyclePalette`

```ags
CyclePalette (int start, int end)
```

This is used for special effects, like the flowing colors on the Space
Quest 4 title screen, and the Sierra logo of the later Sierra games. The
palette indexes from START to END are cycled around one slot. Using this
call in a repeatedly_execute function gives the effect of animation.

By default, the colors rotate leftwards through the palette. If you
pass the arguments the other way round (i.e. START being larger than END)
then the colors will rotate in the opposite direction.

**NOTE:** This command only works in 256-color games.

Example:

```ags
CyclePalette(10,200);
```

will cause the palette indexes from 10 to 200 cycle around one slot and
give a color effect.

*See also:* [`FadeIn`](Globalfunctions_Screen#fadein), [`FadeOut`](Globalfunctions_Screen#fadeout),
[`SetPalRGB`](Globalfunctions_Palette#setpalrgb)

---

### `SetPalRGB`

```ags
SetPalRGB (int slot, int red, int green, int blue)
```

Changes the RGB components of one of the palette slots. The palette is
initially set up in the Palette Editor, but you can override it during
the game using this function for special effects. The RED, GREEN and
BLUE parameters each range from 0 to 63 (as used in the Palette Editor).

If SLOT is a background slot, then this function's effect will last
until the player changes screen, when the palette is changed to the new
room's palette. If SLOT is not a background slot, the effect of this
function is permanent.

NOTE: This function will allow you to change the colors which are
"locked" in the AGS Editor. However, you should not normally do this as
it can cause strange colors in the game.

Example:

```ags
SetPalRGB(10,63,63,21);
```

will change palette slot number 10 from light green to yellow

*See also:* [`CyclePalette`](Globalfunctions_Palette#cyclepalette),
[`FadeIn`](Globalfunctions_Screen#fadein), [`FadeOut`](Globalfunctions_Screen#fadeout),
[`UpdatePalette`](Globalfunctions_Palette#updatepalette)

---

### `UpdatePalette`

```ags
UpdatePalette()
```

Commits the changes you made to the game palette. The script global
variable `palette[]` stores the state of all the colors of the palette.
You can access the red, green and blue components with .r, .g and .b.
The values range from 0 to 63.

Example:

```ags
palette[16].r = 60;
UpdatePalette();
```

will make the black color turn bright red. When you actually change the
variable, nothing happens. Call this function to update the screen.

*See also:* [`SetPalRGB`](Globalfunctions_Palette#setpalrgb)
