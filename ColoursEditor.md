## Colours Editor

The Colours pane is primarily meant for the game Palette setup, but also contains a Colour Finder control that lets you find a single-number representation of a particular color.

The Palette is very important for 8-bit games, but is not useful for others.

The Colour Finder may come useful when you need to assign a color number to a game property or in a script. Although many game properties allow to open a colour picker for this purpose, while in script it's recommended to use a [`Game.GetColorFromRGB`](Game#gamegetcolorfromrgb) command.

### Palette setup

As said above, Palette is only for *real 8-bit* games (not simulated by restricting yourself to limited colour range). If you made a decision to make a 8-bit game you first need to set game's Color Depth to 8-bit in [General Settings](GeneralSettings#basic-properties). After that the Palette control becomes actually used in your project.

Here you will see the 256-color palette
displayed in a grid. Most of the slots are marked "X" - these are the
slots reserved for the background pictures, and will be different in
each room. The other colors will be as they look here for the entire
game. These fixed colors allow things like the main character graphics,
which must be displayed on more than one screen, to work.

If you want, you can assign more or less colors to the backgrounds. To
toggle the background assignment on/off, click on the slot, then check
the "This color is room-dependent" box to swap the slot's status.

**IMPORTANT NOTE:** *You must set up the palette as you want it before
you start making your game - if you change it later, you will have to
re-import all the sprites and background scenes.*

You can select multiple color slots by clicking on the first slot, then
shift-clicking on the last slot in the range you want to select. You can
then toggle the background status of all the selected slots at once.

You can right-click in the palette grid to export the entire palette to
a .PAL or BMP file which you can then use to read back into the Editor
in a different game. If you choose to export to a bmp file, then a
screen shot of the Palette Editor will be saved as the picture. This way
you can see all the game-wide colors in the file.

The "Replace palette" option replaces the palette entries with those
entries from the PAL or BMP file you choose. It can read standard
768-byte PAL files, SCI palette resources (renamed to extension .pal)
and JASC PSP palette files.
