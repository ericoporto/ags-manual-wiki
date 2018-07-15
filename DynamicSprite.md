DynamicSprite functions and properties
--------------------------------------

[Create (dynamic sprite)](#DynamicSprite.Create)\
[CreateFromBackground](#DynamicSprite.CreateFromBackground)\
[CreateFromDrawingSurface](#DynamicSprite.CreateFromDrawingSurface)\
[CreateFromExistingSprite](#DynamicSprite.CreateFromExistingSprite)\
[CreateFromFile](#DynamicSprite.CreateFromFile)\
[CreateFromSaveGame](#DynamicSprite.CreateFromSaveGame)\
[CreateFromScreenShot](#DynamicSprite.CreateFromScreenShot)\
[ChangeCanvasSize](#DynamicSprite.ChangeCanvasSize)\
[CopyTransparencyMask](#DynamicSprite.CopyTransparencyMask)\
[Crop (dynamic sprite)](#DynamicSprite.Crop)\
[Delete (dynamic sprite)](#DynamicSprite.Delete)\
[Flip (dynamic sprite)](#DynamicSprite.Flip)\
[GetDrawingSurface (dynamic sprite)](#DynamicSprite.GetDrawingSurface)\
[Resize (dynamic sprite)](#DynamicSprite.Resize)\
[Rotate (dynamic sprite)](#DynamicSprite.Rotate)\
[SaveToFile (dynamic sprite)](#DynamicSprite.SaveToFile)\
[Tint (dynamic sprite)](#DynamicSprite.Tint)\
[ColorDepth property (dynamic sprite)](#DynamicSprite.ColorDepth)\
[Graphic property (dynamic sprite)](#DynamicSprite.Graphic)\
[Height property (dynamic sprite)](#DynamicSprite.Height)\
[Width property (dynamic sprite)](#DynamicSprite.Width)

---

### Create (dynamic sprite)

    static DynamicSprite* DynamicSprite.Create(int width, int height,
                                               optional bool hasAlphaChannel)

Creates a new blank dynamic sprite of the specified size. It will
initially be fully transparent, and can optionally have an alpha
channel. This command is useful if you just want to create a new sprite
and then use the DrawingSurface commands to draw onto it.

If the game colour depth is lower than 32-bit, then the
*hasAlphaChannel* parameter will be ignored.

Use the [Graphic](ags52#DynamicSprite.Graphic) property of the
DynamicSprite to interface with other commands and to use the new sprite
in the game.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    DynamicSprite* sprite = DynamicSprite.Create(50, 30);
    DrawingSurface *surface = sprite.GetDrawingSurface();
    surface.DrawingColor = 14;
    surface.DrawPixel(25, 15);
    surface.Release();
    sprite.Delete();

creates a 50x30 sprite, draws a white dot in the middle, then deletes
the sprite.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete),
[DynamicSprite.Graphic](ags52#DynamicSprite.Graphic),
[DynamicSprite.GetDrawingSurface](ags52#DynamicSprite.GetDrawingSurface)

---

### CreateFromBackground

    static DynamicSprite* DynamicSprite.CreateFromBackground
                          (optional int frame, optional int x, optional int y,
                           optional int width, optional int height)

Creates a new dynamic sprite containing a copy of the specified room
background.

The most basic use of this function is to supply no parameters, in which
case the sprite will contain an exact copy of the current room
background.

If you want, you can supply the *frame* only, in which case you will get
a complete copy of that background frame number from the current room.

Optionally, you can specify a portion of the background to grab. You
must either supply all or none of the x, y, width and height parameters;
if you do supply them, this allows you to just get a small portion of
the background image into the new sprite. All co-ordinates are in
320x200-resolution room co-ordinates.

Use the [Graphic](ags52#DynamicSprite.Graphic) property of the
DynamicSprite to interface with other commands and to use the new sprite
in the game.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromBackground(GetBackgroundFrame(), 130, 70, 60, 60);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(0, 0, sprite.Graphic);
    surface.Release();
    sprite.Delete();

creates a copy of the centre 60x60 area on the background, and draws it
onto the top left corner of the background image.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete)

---

### CreateFromDrawingSurface

    static DynamicSprite* DynamicSprite.CreateFromDrawingSurface(
                            DrawingSurface* surface, int x, int y,
                            int width, int height)

Creates a new dynamic sprite containing a copy of the specified portion
of the drawing surface. This allows you to easily create new sprites
from portions of other sprites.

**NOTE:** The *x*, *y*, *width* and *height* parameters respect the
DrawingSurface's
[UseHighResCoordinates](ags51#DrawingSurface.UseHighResCoordinates)
setting, so make sure that the type of co-ordinates that you are using
match up with what the drawing surface expects.

Use the [Graphic](ags52#DynamicSprite.Graphic) property of the
DynamicSprite to interface with other commands and to use the new sprite
in the game.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromExistingSprite(object[0].Graphic);
    DrawingSurface *surface = sprite.GetDrawingSurface();
    DynamicSprite *newSprite = DynamicSprite.CreateFromDrawingSurface(surface, 0, 0, 10, 10);
    surface.Release();
    sprite.Delete();
    object[0].Graphic = newSprite.Graphic;

changes object 0's image to be just the top-left corner of what it
previously was.

*Compatibility:* Supported by **AGS 3.0.2** and later versions.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete)

---

### CreateFromExistingSprite

    static DynamicSprite* DynamicSprite.CreateFromExistingSprite(
                            int slot, optional bool preserveAlphaChannel)

Creates a new dynamic sprite containing a copy of the specified sprite
*slot*.

Returns the DynamicSprite instance representing the new sprite. This
function is useful as it effectively allows you to apply transformations
such as resizing to any sprite in the game.

Use the [Graphic](ags52#DynamicSprite.Graphic) property of the
DynamicSprite to interface with other commands and to use the new sprite
in the game.

*preserveAlphaChannel* determines whether the sprite's alpha channel
will also be copied across. It is false by default for backwards
compatibility reasons, and is useful because it allows you to strip the
alpha channel in order to do whole image transparency. This parameter
has no effect with sprites that do not have an alpha channel.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromExistingSprite(object[0].Graphic);
    sprite.Resize(20, 20);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 80, sprite.Graphic);
    surface.Release();
    sprite.Delete();

creates a copy of object 0's current sprite, resizes it down to 20x20,
and then draws the result onto the background.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete),
[DynamicSprite.Resize](ags52#DynamicSprite.Resize)

---

### CreateFromFile

*(Formerly known as LoadImageFile, which is now obsolete)*

    static DynamicSprite* DynamicSprite.CreateFromFile(string filename)

Loads an external image FILENAME into memory as a sprite.

Returns the DynamicSprite instance representing the sprite, or *null* if
the image could not be loaded (file not found or unsupported format).

Only BMP and PCX files can be loaded with this command.

Use the [Graphic](ags52#DynamicSprite.Graphic) property of the
DynamicSprite to interface with other commands and to use the new sprite
in the game.

**NOTE:** Since AGS 3.4.1 you can use location tokens in filename, like
with [File.Open](ags53#File.Open) and similar commands.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    if (sprite != null) {
      DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
      surface.DrawImage(100, 80, sprite.Graphic);
      surface.Release();
      sprite.Delete();
    }

will load the file "CustomAvatar.bmp" and if successful draw the image
near the middle of the screen.

Once the image is finished with, Delete should be called on it.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete),
[DynamicSprite.CreateFromSaveGame](ags52#DynamicSprite.CreateFromSaveGame)

---

### CreateFromSaveGame

*(Formerly known as LoadSaveSlotScreenshot, which is now obsolete)*

    static DynamicSprite* DynamicSprite.CreateFromSaveGame
                            (int saveSlot, int width, int height)

Loads the screenshot for save game SAVESLOT into memory, resizing it to
WIDTH x HEIGHT.

Returns the DynamicSprite instance of the image if successful, or
returns *null* if the screenshot could not be loaded (perhaps the save
game didn't include one).

In order for this to work, the "Save screenshots in save games" option
must be ticked in the main Game Settings pane.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    // at top of script, outside event functions
    DynamicSprite *buttonSprite;

    // inside an event function
    buttonSprite = DynamicSprite.CreateFromSaveGame(1, 50, 50);
    if (buttonSprite != null) {
      btnScrnshot.NormalGraphic = buttonSprite.Graphic;
    }

will load the screenshot for save game 1 and resize it to 50x50. It then
places it onto the btnScrnshot GUI button.

Once the GUI is disposed of, Delete should be called on the sprite.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete),
[Game.GetSaveSlotDescription](ags54#Game.GetSaveSlotDescription),
[DynamicSprite.CreateFromFile](ags52#DynamicSprite.CreateFromFile),
[DynamicSprite.CreateFromScreenShot](ags52#DynamicSprite.CreateFromScreenShot)

---

### CreateFromScreenShot

    static DynamicSprite* DynamicSprite.CreateFromScreenShot
                            (optional int width, optional int height)

Creates a new DynamicSprite instance with a copy of the current screen
in it, resized to WIDTH x HEIGHT. If you do not supply the width or
height, then a full screen sized sprite will be created.

This command can be useful if you're creating a save game screenshots
GUI, in order to display the current game position as well as the saved
slot positions.

**NOTE:** This command can be slow when using the Direct3D graphics
driver.

**IMPORTANT:** This command loads an extra sprite into memory which is
not controlled by the normal AGS sprite cache and will not be
automatically disposed of. Therefore, when you are finished with the
image you **MUST** call Delete on it to free its memory.

**IMPORTANT:** If the DynamicSprite instance is released from memory
(ie. there is no longer a DynamicSprite\* variable pointing to it), then
the sprite will also be removed from memory. Make sure that you keep a
global variable pointer to the sprite until you are finished with it,
and at that point call Delete.

Example:

    // at top of script, outside event functions
    DynamicSprite *buttonSprite;

    // inside an event function
    buttonSprite = DynamicSprite.CreateFromScreenShot(80, 50);
    if (buttonSprite != null) {
      btnScrnshot.NormalGraphic = buttonSprite.Graphic;
    }

places a screen grab of the current game session onto btnScrnshot.

Once the GUI is disposed of, Delete should be called on the sprite.

*See Also:* [DynamicSprite.Delete](ags52#DynamicSprite.Delete),
[Game.GetSaveSlotDescription](ags54#Game.GetSaveSlotDescription),
[DynamicSprite.CreateFromFile](ags52#DynamicSprite.CreateFromFile),
[DynamicSprite.CreateFromSaveGame](ags52#DynamicSprite.CreateFromSaveGame)

---

### ChangeCanvasSize

    DynamicSprite.ChangeCanvasSize(int width, int height, int x, int y);

Changes the sprite size to *width* x *height*, placing the current image
at offset (x, y) within the new canvas. Unlike the
[Resize](ags52#DynamicSprite.Resize) command, the current image is
kept at its original size.

This function allows you to enlarge the sprite background in order to
draw more onto it than its current boundaries allow. It is effectively
the opposite of [Crop](ags52#DynamicSprite.Crop). The additional
surface area will be transparent.

The width and height are specified in 320x200-resolution units.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromExistingSprite(10);
    sprite.ChangeCanvasSize(sprite.Width + 10, sprite.Height, 5, 0);
    DrawingSurface *surface = sprite.GetDrawingSurface();
    surface.DrawingColor = 14;
    surface.DrawLine(0, 0, 5, surface.Height);
    surface.Release();
    sprite.Delete();

creates a dynamic sprite as a copy of sprite 10, enlarges it by 5 pixels
to the left and right, and draws a line in the new area to the left.

*See Also:* [DynamicSprite.Crop](ags52#DynamicSprite.Crop),
[DynamicSprite.Resize](ags52#DynamicSprite.Resize),
[DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Width](ags52#DynamicSprite.Width)

---

### CopyTransparencyMask

    DynamicSprite.CopyTransparencyMask(int fromSpriteSlot)

Copies the transparency mask from the specified sprite slot onto the
dynamic sprite. The dynamic sprite's transparency and/or alpha channel
will be replaced with the one from the other sprite.

This command is designed for special effects. It is fairly slow since it
involves inspecting each pixel of the image, so it's not recommended
that you use it often.

The source sprite must be the same size and colour depth as the dynamic
sprite.

**NOTE:** This command makes all pixels that are transparent in the
source sprite also transparent in the dynamic sprite. It does not make
opaque pixels from the source sprite into opaque pixels on the dynamic
sprite (because it wouldn't know what colour to make them).

If the source image has an alpha channel, then the dynamic sprite will
have an alpha channel created as a copy of the one from the source
sprite.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromExistingSprite(10);
    sprite.CopyTransparencyMask(11);
    object[0].Graphic = sprite.Graphic;
    Wait(80);
    sprite.Delete();

creates a dynamic sprite as a copy of sprite 10, changes its
transparency mask to use that of sprite 11, and displays it on object 0.

*See Also:*
[DynamicSprite.CreateFromExistingSprite](ags52#DynamicSprite.CreateFromExistingSprite)

---

### Crop (dynamic sprite)

    DynamicSprite.Crop(int x, int y, int width, int height);

Crops the sprite down to *width* x *height*, starting from (x,y) in the
image. The width and height are specified in 320x200-resolution units,
as usual.

This allows you to trim the edges off a sprite, and perform related
tasks. Only the area with its top-left corner as (x,y) and of WIDTH x
HEIGHT in size will remain.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    sprite.Crop(10, 10, sprite.Width - 10, sprite.Height - 10);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 100, sprite.Graphic);
    surface.Release();
    sprite.Delete();

will load the CustomAvatar.bmp image, cut off the left and top 10
pixels, and then draw it onto the room background at (100,100).

*See Also:*
[DynamicSprite.ChangeCanvasSize](ags52#DynamicSprite.ChangeCanvasSize),
[DynamicSprite.Flip](ags52#DynamicSprite.Flip),
[DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Width](ags52#DynamicSprite.Width)

---

### Delete (dynamic sprite)

*(Formerly known as DeleteSprite, which is now obsolete)*

    DynamicSprite.Delete();

Deletes the specified dynamic sprite from memory. Use this when you are
no longer displaying the sprite and it can be safely disposed of.

You do not normally need to delete sprites, since the AGS Sprite Cache
manages loading and deleting sprites automatically.

However, when an extra sprite has been loaded into the game (for
example, with the CreateFromFile or CreateFromScreenShot commands) then
AGS does not delete it automatically, and you must call this command
instead.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    object[1].Graphic = sprite.Graphic;
    Wait(200);
    object[1].Graphic = 22;
    sprite.Delete();

will load the file "CustomAvatar.bmp", change Object 1 to display this
graphic, wait 5 seconds, then change object 1 back to its old sprite 22
and free the new image.

*See Also:*
[DynamicSprite.CreateFromScreenShot](ags52#DynamicSprite.CreateFromScreenShot),
[DynamicSprite.Graphic](ags52#DynamicSprite.Graphic)

---

### Flip (dynamic sprite)

    DynamicSprite.Flip(eFlipDirection);

Flips the dynamic sprite according to the parameter:

*eFlipLeftToRight* flips the image from left to right\
*eFlipUpsideDown* flips the image from top to bottom\
*eFlipBoth* flips the image from top to bottom and left to right

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    sprite.Flip(eFlipUpsideDown);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 100, sprite.Graphic);
    surface.Release();
    sprite.Delete();

will load the CustomAvatar.bmp image, flip it upside down, and then draw
it onto the room background at (100,100).

*See Also:* [DynamicSprite.Crop](ags52#DynamicSprite.Crop),
[DynamicSprite.Resize](ags52#DynamicSprite.Resize),
[DynamicSprite.Rotate](ags52#DynamicSprite.Rotate)

---

### GetDrawingSurface (dynamic sprite)

    DrawingSurface* DynamicSprite.GetDrawingSurface();

Gets the drawing surface for this dynamic sprite, which allows you to
modify the sprite by drawing onto it in various ways.

After calling this method, use the various [DrawingSurface
functions](ags51#DrawingSurfaceFunctions) to modify the sprite, then
call Release on the surface when you are finished.

Example:

    DynamicSprite *sprite = DynamicSprite.CreateFromExistingSprite(object[0].Graphic);
    DrawingSurface *surface = sprite.GetDrawingSurface();
    surface.DrawingColor = 13;
    surface.DrawLine(0, 0, 20, 20);
    surface.Release();
    object[0].Graphic = sprite.Graphic;
    Wait(40);
    sprite.Delete();

this creates a dynamic sprite as a copy of Object 0's existing sprite,
draws a pink diagonal line across it, sets this new sprite onto the
object for 1 second and then removes it.

*See Also:*
[DynamicSprite.CreateFromExistingSprite](ags52#DynamicSprite.CreateFromExistingSprite),
[DrawingSurface.DrawLine](ags51#DrawingSurface.DrawLine),
[DrawingSurface.Release](ags51#DrawingSurface.Release)

---

### Resize (dynamic sprite)

    DynamicSprite.Resize(int width, int height);

Resizes an existing dynamic sprite to WIDTH x HEIGHT pixels.

The width and height are specified in 320x200-resolution units, as
usual.

**NOTE:** Resizing is a relatively slow operation, so do not attempt to
resize sprites every game loop; only do it when necessary.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    sprite.Resize(sprite.Width * 2, sprite.Height * 2);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 100, sprite.Graphic);
    surface.Release();
    sprite.Delete();

will load the CustomAvatar.bmp image, stretch it to double its original
size, and then draw it onto the room background at (100,100).

*See Also:*
[DynamicSprite.ChangeCanvasSize](ags52#DynamicSprite.ChangeCanvasSize),
[DynamicSprite.Crop](ags52#DynamicSprite.Crop),
[DynamicSprite.Flip](ags52#DynamicSprite.Flip),
[DynamicSprite.Rotate](ags52#DynamicSprite.Rotate),
[DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Width](ags52#DynamicSprite.Width)

---

### Rotate (dynamic sprite)

    DynamicSprite.Rotate(int angle, optional int width, optional int height)

Rotates the dynamic sprite by the specified *angle*. The angle is in
degrees, and must lie between 1 and 359. The image will be rotated
clockwise by the specified angle.

Optionally, you can specify the width and height of the rotated image.
By default, AGS will automatically calculate the new size required to
hold the rotated image, but you can override this by passing the
parameters in.

Note that specifying a width/height does not stretch the image, it just
allows you to set the image dimensions to crop the rotation.

**NOTE:** Rotating is a relatively slow operation, so do not attempt to
rotate sprites every game loop; only do it when necessary.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    sprite.Rotate(90);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 100, sprite.Graphic);
    surface.Release();
    sprite.Delete();

will load the CustomAvatar.bmp image, rotate it 90 degrees clockwise,
draw the result onto the screen, and then delete the image.

*See Also:* [DynamicSprite.Flip](ags52#DynamicSprite.Flip),
[DynamicSprite.Resize](ags52#DynamicSprite.Resize),
[DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Width](ags52#DynamicSprite.Width)

---

### SaveToFile (dynamic sprite)

    DynamicSprite.SaveToFile(string filename)

Saves the dynamic sprite to the specified file.

The filename you supply must have a .PCX or .BMP extension; they are the
only two file types that the engine supports.

Returns 1 if the sprite was saved successfully, or 0 if it failed.

**NOTE:** Since AGS 3.4.1 you can use location tokens in filename, like
with [File.Open](ags53#File.Open) and similar commands.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    sprite.Rotate(90);
    sprite.SaveToFile("RotatedAvatar.bmp");
    sprite.Delete();

will load the CustomAvatar.bmp image, rotate it 90 degrees clockwise,
then save the result back to the disk.

*See Also:*
[DynamicSprite.CreateFromFile](ags52#DynamicSprite.CreateFromFile),
[SaveScreenShot](ags54#SaveScreenShot)

---

### Tint (dynamic sprite)

    DynamicSprite.Tint(int red, int green, int blue, int saturation, int luminance)

Tints the dynamic sprite to (RED, GREEN, BLUE) with SATURATION percent
saturation. For the meaning of all the parameters, see
[SetAmbientTint](ags54#SetAmbientTint).

The tint set by this function is permanent for the dynamic sprite --
after the tint has been set, it is not possible to remove it. If you
call Tint again with different parameters, it will apply the new tint to
the already tinted sprite from the first call.

**NOTE:** This function only works with hi-colour sprites.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromExistingSprite(object[0].Graphic);
    sprite.Tint(255, 0, 0, 100, 100);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 80, sprite.Graphic);
    surface.Release();
    sprite.Delete();

creates a copy of object 0's sprite, tints it red, and draws it onto the
room background.

*See Also:* [DynamicSprite.Flip](ags52#DynamicSprite.Flip),
[DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Width](ags52#DynamicSprite.Width),
[SetAmbientTint](ags54#SetAmbientTint)

---

### ColorDepth property (dynamic sprite)

    readonly int DynamicSprite.ColorDepth;

Gets the colour depth of this dynamic sprite. This can be 8, 16 or 32
and is not necessarily the same as the game colour depth (though this
usually will be the case).

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    if (sprite != null) {
      Display("The image is %d x %d pixels, at %d-bit depth.", sprite.Width, sprite.Height, sprite.ColorDepth);
      sprite.Delete();
    }

displays the colour depth of the CustomAvatar.bmp image.

*See Also:* [DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Width](ags52#DynamicSprite.Width)

---

### Graphic property (dynamic sprite)

    readonly int DynamicSprite.Graphic;

Gets the sprite slot number in which this dynamic sprite is stored. This
value can then be passed to other functions and properties, such as
[Button.NormalGraphic](ags57#Button.NormalGraphic).

Example:

    DynamicSprite* ds = DynamicSprite.CreateFromScreenShot(50, 50);
    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawImage(100, 100, ds.Graphic);
    surface.Release();
    ds.Delete();

takes a screen shot, and draws it onto the background scene at
(100,100).

*See Also:*
[DynamicSprite.CreateFromScreenShot](ags52#DynamicSprite.CreateFromScreenShot),
[DynamicSprite.Delete](ags52#DynamicSprite.Delete)

---

### Height property (dynamic sprite)

    readonly int DynamicSprite.Height;

Gets the height of this dynamic sprite. The height is always returned in
320x200-resolution units.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    if (sprite != null) {
      Display("The image is %d x %d pixels.", sprite.Width, sprite.Height);
      sprite.Delete();
    }

displays the size of the CustomAvatar.bmp image.

*See Also:* [DynamicSprite.Resize](ags52#DynamicSprite.Resize),
[DynamicSprite.Width](ags52#DynamicSprite.Width)

---

### Width property (dynamic sprite)

    readonly int DynamicSprite.Width;

Gets the width of this dynamic sprite. The width is always returned in
320x200-resolution units.

Example:

    DynamicSprite* sprite = DynamicSprite.CreateFromFile("CustomAvatar.bmp");
    if (sprite != null) {
      Display("The image is %d x %d pixels.", sprite.Width, sprite.Height);
      sprite.Delete();
    }

displays the size of the CustomAvatar.bmp image.

*See Also:* [DynamicSprite.Height](ags52#DynamicSprite.Height),
[DynamicSprite.Resize](ags52#DynamicSprite.Resize)
