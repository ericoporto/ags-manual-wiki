## Sprite Manager

The sprite manager is where you can import sprites and organize them into
folders.
Each sprite is assigned an unique positive integer number as identifier.

![](images/EditorSprite_1.png)

The sprite manager has two panels, at left are the folders, which you can use
the right click button to create a subfolder, rename an already created
subfolder or deleting a subfolder (losing all it's contents).

![](images/EditorSprite_2.png)

The panel at right, is where imported sprites at the selected folder are shown.
Right clicking on an empty area will give you the possibility to "import new
sprite(s) from files...", which will allow you to select a number of compatible
image files in your computer directories to import into your game project.

**Note:** it's interesting that the images you use on your project are
themselves placed on the own AGS game project directory, this is because ags will
in this case store the path relatively, which will allow to later on in the game
development process, if you update a game graphic, you can select and right
click the desired sprites in the sprite manager and tell AGS to update them with
"Replace sprite(s) from source..." option.

You can select all files in a folder by selecting the first file in the folder
and then pressing Shift+End.

### Import Sprite

Once a file or files are selected, AGS will bring up the Import Sprite window.

![](images/EditorSprite_3.png)

On the Import Sprite window, AGS will offer you controls so you can change how
the transparency is defined for the imported sprite, and a selection in case
you don't want to import the whole area of the sprite or you want a tiled sprite
import.

Above Close, Import and Import All buttons, a combobox will allow you to navigate
the image files you selected before. If you click Import All, the chosen options
will be applied to all images you are importing.

At the end of the import process, the sprites will be inserted in the folder
that was active at the Sprite manager tab.
