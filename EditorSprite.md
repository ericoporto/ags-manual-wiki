## Sprite Manager

The sprite manager is where you can import sprites and organize them into
folders. Each sprite that is imported will be assigned a sprite number which is
used as its unique identifier.

![](images/EditorSprite_1.png)

The sprite manager has two panes, on the left are the sprite folders. Right
click here to create a subfolder, rename an existing subfolder, or delete a
subfolder (losing all of its contents).

![](images/EditorSprite_2.png)

The pane on the right, is where imported sprites are displayed. Right clicking
on an empty area will give you the possibility to "import new sprite(s) from
files...". This allows you to import one or more compatible image files into
your game project.

**NOTE:** Unlike other game development tools, once a sprite is imported using
AGS it is added to the sprite data inside your game project's directory and the
source file isn't read again unless you choose to re-import it. This is done by
right clicking a sprite and choosing the "Replace sprite(s) from source..."
option.

**NOTE:** You can quickly select all files in a folder by selecting the first
file and then pressing Shift+End.

### Import Sprite

Once a file or files are selected, AGS will bring up the Import Sprite window.

![](images/EditorSprite_3.png)

In this window, AGS will offer you controls which determine exactly how the
images files will be used. The most crucial choice is usually to choose how
transparency will be determined for the imported sprite, as well as whether to
import the entire sprite or use a tiled selection.

If multiple files are being imported they can be processed individually by
using the 'Import' button, or all in one go by using the 'Import All' button.
The combobox near the bottom left corner of the screen will allow you to change
which source image file is currently being displayed.

**NOTE:** if using the 'Import All' button all remaining images will be imported
using the currently selected import options

**NOTE:** animated GIF frames are treated as separate images, so a 5 frame GIF
imported as 2 tiles will result in 10 new sprites being created.


### Tiled sprite import

You may have noticed a checkbox called "Tiled sprite import". Some
people find this a useful way of importing many frames of a character's
animation at once.

In order for this to work, you need to have all your sprites lined up on
your source bitmap at even intervals. Then, use the "Import from file"
option and import it as usual. Check the "Tiled sprite import" box, and
select the upper-left frame.

When you click the left mouse button, the selection rectangle will
become un-filled and now you can drag the mouse to define how many
frames to import - they'll all be enclosed by selection rectangles. Once
you have the correct number, click the left button again and they will
all be imported.

### Alpha blended sprites

AGS supports alpha blended sprites if your game is 32-bit color. In
this case, you need to import a PNG image with an alpha channel (you
cannot paste alpha-blended images from the clipboard).

When you do so, AGS will prompt you asking whether you want to use the
image's alpha channel or not. If you select Yes, then the sprite will be
drawn alpha blended in the game if it is used for a character, object,
mouse cursor or GUI.

Note that if you use alpha blending, any overall transparency that you
set (such as Character.Transparency, Object.Transparency,
GUI.Transparency) will be ignored.

NOTE: Currently, alpha blended sprites cannot be antialiased, so if
you have the Anti Alias Sprites option turned on in Setup, it will not
be applied to alpha-blended characters.

### Sprite Storage

AGS sprite storage can be configured through **Enable sprite storage optimization** and **Sprite file compression** in [General Settings, in Compiler category](GeneralSettings#compiler).

- **Enable sprite storage optimization**, stores sprites in a format that requires less space.
- **Sprite file compression**, can be configured to no compression, RLE or LZW.

When a sprite is imported, it gets and index number which can be used to refer to it through your game. This information, along with import settings for each sprite, are saved in your AGS game project. It will additionally, incrementally as you import sprites, add the file to your project sprite file, named `acsprset.spr`. You can at any time in your project switch your sprite file compression and storage settings and AGS will update it accordingly, so don't worry if you just realize you need compression at a later time in your project.

It's recommended that all the graphic files you are importing in your project are placed in a directory inside of your AGS Game Project. By maintaining all files there, if you wish to not backup your `acsprset.spr` file, you can recreate it at any time by using the **File** `->` **Restore all sprites from sources** menu. 