## Getting Started with AGS - Part 6

### Using your own graphics

When you were choosing the graphics for the object earlier in this
tutorial, you probably noticed that the images available didn't look up
to much. This is no problem, because you can import your own graphics
using the Sprite Manager.

Double-click *"Sprites"* near the top of the project tree. This opens up
the Sprite Manager, where you can see the complete sprite set for the
game.

AGS uses these sprites for all game graphics, except room backgrounds.
The Sprite Manager is the central place where you do all your graphics
importing. Whenever you want to use images in the game (for mouse
cursors, views, objects, etc), you select an image to use from here.

There are two ways to import your graphics - either overwrite an
existing sprite with your graphic, or create a new slot for it. To
overwrite an existing sprite, right-click the sprite and select
*"Replace sprite from file"*. To import a new slot, right-click on the
background of the window and choose *"Import new sprite from file"*. If
your game is hi-color, you'll also have options to paste from the
clipboard.

Note that the sprite graphics you import shouldn't exceed the maximum
number of colors that the game supports - i.e. if you have a 256-color
game, you must import 256-color sprites.

![Right-clicking to replace existing sprite](images/intro6_1.jpg)

So, let's replace the default key image with something of our own.
Right-click on it and choose "*Replace sprite from file*". Select the
file that you want in the dialog, and then you'll be presented with
this:

![The "Import Sprite" window](images/intro6_2.png)

This is the Import Sprite window. You'll see the image from the file
that you chose, along with various options. The Zoom slider on the left
allows you to zoom in on the image (very useful for low resolution
graphics), and the "Transparent color" option allows you to choose how
AGS decides which color is the image's transparent color.

Now, you have two choices. If you want to import the whole image, just
click the "Import Whole Image" button, and you're done. If on the other
hand you only want to import a portion of the image, then you need to
right-drag the mouse within the image to select the area that you want
to import. Once you've got it right, left-click to confirm and the
selected area of the image will be imported.

**NOTE:** For character graphics, make sure you import graphics that are
a suitable size for the game backgrounds. For example, don't import a
320x200-sized image for your character if your game resolution is 320x200.
A good size for games with this size of screen resolution would be about
20x50 pixels.

![](images/icon_info.gif)

NOTE (256-color only): You may well find that the colors on your graphic
look slightly strange once you've imported the image. This is because by
default only the first 41 of the palette colors are allocated to sprites,
so your graphic will be remapped to this much smaller palette. If you find
that many of your imported sprites look strange, you can increase the
number of colors assigned to sprites, at the expense of background colors
(see the earlier part of the tutorial for palette setup).

#### Tiled sprite import

This feature allows you to import a grid of sprites into separate slots
- for example, if you have several frames of a character animation side
by side in the source bitmap. To do this, simply check the "Tiled sprite
import" box, and align your rectangle on the top left sprite. When you
click the left mouse button, you will get an extra step which allows you
to size the grid:

Click the left button again once you are happy with the grid. Each of
the cells will be imported as a separate sprite.

![](images/icon_info.gif)

NOTE: Tiled sprite import only works if you selected "Import new sprite
from file". If you used the "Replace sprite" option, only the first tile
will be imported.

Go to part 7: [Animations](acintro7)
