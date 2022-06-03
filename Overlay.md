## `Overlay` functions and properties

The overlays are simple sprite placeholders, they are created in script, and display images on screen. They cannot be interacted with by player, nor interact with other game objects. This makes them ideal for creating temporary visual effects. But they also may be used to script a custom object from ground up; that may involve some advanced scripting though.

Overlays may be created as *screen overlays* and *room overlays*. This defines the visual layer they are positioned in, and which other game objects they are visually sorted with.

---

### `Overlay.CreateGraphical`

*(Formerly known as `CreateGraphicOverlay`, which is now obsolete)*

    static Overlay* Overlay.CreateGraphical(int x, int y, int slot, optional bool transparent, optional bool clone)

Creates a *screen overlay* using an image from SLOT sprite. The image is placed at (X,Y) in the screen coordinates.

The screen overlays are positioned in the screen graphic layer, and are visually sorted among other screen overlays and GUI using overlay's [ZOrder](Overlay#overlayzorder) property.

If *transparent* is true then the overlay will be drawn in the same way
as characters/objects, if it is false then a black rectangle will be
painted behind the sprite. Default value is "true".
**NOTE:** for "historical reasons", *transparent* parameter works only in 8-bit games, and does not work in 16-bit and 32-bit games at all, so it's currently useless there.

If *clone* is true then the overlay will make a copy of the SLOT image, otherwise it will create a shared reference, similar to how room objects or characters do. Default value is "false". In practice this only makes a difference if you are creating an overlay from the [DynamicSprite](DynamicSprite): if you make a copy then the original dynamic sprite is safe to discard; also any changes to dynamic sprite will be applied to overlay only if it uses shared reference (no copy). If you create alot of overlays, sharing (non copying) may improve game's perfomance and decrease the memory requirements. For the same perfomance reasons regular sprites are never copied, regardless of this parameter's value (because they cannot be deleted or edited at runtime).

**NOTE:** if you are using a [DynamicSprite](DynamicSprite) when creating an overlay, and *not* copying the image, then you have to make sure the sprite is not deleted so long as overlay stays on screen, or overlay's image will reset to sprite 0.

**NOTE:** if the Overlay variable goes out of scope, the overlay will be removed. Hence, if you want the overlay to last on-screen outside of the
script function where it was created, the `Overlay*` variable declaration needs to be at the top of the script and outside any script
functions.

**NOTE:** if the player goes to a different room all active overlays are removed automatically.

Example:

    Overlay* myOverlay = Overlay.CreateGraphical(100, 100, 300);
    Wait(40);
    myOverlay.Remove();

will create an overlay using sprite number 300, at the coordinates 100,100. It will display for 1 second, then remove it.

*See also:* [`Overlay.CreateRoomGraphical`](Overlay#overlaycreateroomgraphical),
[`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.CreateRoomTextual`](Overlay#overlaycreateroomtextual),
[`Overlay.Remove`](Overlay#overlayremove),
[`Overlay.Graphic`](Overlay#overlaygraphic)

---

### `Overlay.CreateRoomGraphical`

    static Overlay* Overlay.CreateRoomGraphical(int x, int y, int slot, optional bool transparent, optional bool clone)

Creates a *room overlay* using an image from SLOT sprite. The image is placed at (X,Y) in the screen coordinates.

The room overlays are positioned in the room graphic layer, and are visually sorted among other room overlays, characters, room objects and walk-behinds using overlay's [ZOrder](Overlay#overlayzorder) property, similar to how other objects in rooms use `Baseline` property.

All the parameters and use are identical to [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical) function, please refer to its description for more details.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical),
[`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.CreateRoomTextual`](Overlay#overlaycreateroomtextual),
[`Overlay.Remove`](Overlay#overlayremove),
[`Overlay.Graphic`](Overlay#overlaygraphic)

---

### `Overlay.CreateRoomTextual`

    static Overlay* Overlay.CreateRoomTextual(int x, int y, int width,
                                          FontType font, int color, string text)

Creates a *room overlay* containing the text you pass at the position specified. This overlay looks identical to the way speech text is
displayed in conversations, except that with this command the text stays on the screen until either you remove it with the Remove command, or the
player goes to a different room, in which case it is automatically removed.

The room overlays are positioned in the room graphic layer, and are visually sorted among other room overlays, characters, room objects and walk-behinds using overlay's [ZOrder](Overlay#overlayzorder) property, similar to how other objects in rooms use `Baseline` property.

All the parameters and use are identical to [`Overlay.CreateTextual`](Overlay#overlaycreatetextual) function, please refer to its description for more details.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical),
[`Overlay.CreateRoomGraphical`](Overlay#overlaycreateroomgraphical),
[`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.Remove`](Overlay#overlayremove)

---

### `Overlay.CreateTextual`

*(Formerly known as `CreateTextOverlay`, which is now obsolete)*

    static Overlay* Overlay.CreateTextual(int x, int y, int width,
                                          FontType font, int color, string text)

Creates a *screen overlay* containing the text you pass at the position
specified. A screen overlay looks identical to the way speech text is
displayed in conversations, except that with this command the text stays
on the screen until either you remove it with the Remove command, or the
player goes to a different room, in which case it is automatically
removed.

The screen overlays are positioned in the screen graphic layer, and are visually sorted among other screen overlays and GUI using overlay's [ZOrder](Overlay#overlayzorder) property.

The X and Y parameters specify the upper-left corner of where the text
will be written. WIDTH is the width, in pixels, of the text area. FONT
is the font number from the editor to use (0 is the normal font, 1 is
the speech font). COLOR is the text color - use one of the colors from
1 to 15. Finally, TEXT is obviously the text that gets displayed.

The function returns the Overlay, which you use later to reposition and
remove the overlay.

You can insert the value of variables into the message. For more
information, see the [string formatting](StringFormats)
section.

**NOTE:** if the Overlay variable goes out of scope, the overlay will be
removed. Hence, if you want the overlay to last on-screen outside of the
script function where it was created, the `Overlay*` variable
declaration needs to be at the top of the script and outside any script
functions.

**NOTE:** if the player goes to a different room all active overlays are removed automatically.

Example:

    Overlay* myOverlay = Overlay.CreateTextual(50,80,120, Game.SpeechFont, 15,"This is a text overlay");
    Wait(40);
    myOverlay.Remove();

will display a 120 pixels text area with its upper left corner at
coordinates 50,80 containing the string "This is a text overlay" using
the speech font and white color. It will be displayed for 1 second, then
removed.

*See also:*
[`Overlay.CreateGraphical`](Overlay#overlaycreategraphical),
[`Overlay.CreateRoomGraphical`](Overlay#overlaycreateroomgraphical),
[`Overlay.CreateRoomTextual`](Overlay#overlaycreateroomtextual),
[`Overlay.X`](Overlay#overlayx), [`Overlay.Y`](Overlay#overlayy),
[`Overlay.Remove`](Overlay#overlayremove)

---

### `Overlay.Remove`

*(Formerly known as `RemoveOverlay`, which is now obsolete)*

    Overlay.Remove()

Removes the specified overlay from the screen. Use this when you are
done using the overlay.

Example:

    Overlay* myOverlay = Overlay.CreateTextual(50,80,120,2,15,"This is a text overlay");
    Wait(200);
    myOverlay.Remove();

will create a text overlay , wait for 200 game cycles (about 5 seconds)
and then remove the overlay from the screen.

*See also:* [`Overlay.CreateTextual`](Overlay#overlaycreatetextual)

---

### `Overlay.SetText`

*(Formerly known as `SetTextOverlay`, which is now obsolete)*

    Overlay.SetText(int width, FontType font, int color, string text, ...)

Replaces the specified overlay with a new one, at the same co-ordinates
but with the new specified text, width, font and color.

You can insert the value of variables into the message. For more
information, see the [string formatting](StringFormats)
section.

Example:

    Overlay* myOverlay = Overlay.CreateTextual(50,80,120,Game.SpeechFont,15,"This is a text overlay");
    Wait(200);
    myOverlay.SetText(120,Game.SpeechFont,15,"This is another text overlay");

will create a text overlay , wait for 200 game cycles (about 5 seconds)
and then replace the overlay with another one.

*See also:* [`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.Remove`](Overlay#overlayremove)

---

### `Overlay.Graphic`

    int Overlay.Graphic;

Gets/sets the sprite slot number that the overlay is currently using. Textual overlays always return -1, as their image is generated and stored internally, and does not have a formal "number". Setting `Graphic` of a textual overlay will effectively change them to a graphical overlay.

**NOTE:** unlike [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical), where you may choose whether to make an image's copy or a shared reference, setting `Graphic` will always make a shared reference to the sprite. If this is a [DynamicSprite](DynamicSprite), you have to make sure it is not deleted so long as overlay stays on screen, or overlay's image will reset to sprite 0.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical),
[`Overlay.CreateRoomGraphical`](Overlay#overlaycreateroomgraphical),
[`Overlay.X`](Overlay#overlayx), [`Overlay.Y`](Overlay#overlayy),
[`Overlay.Width`](Overlay#overlaywidth),
[`Overlay.Height`](Overlay#overlayheight)

---

### `Overlay.GraphicHeight`

    readonly int Overlay.GraphicHeight;

Gets the original height of the overlay's image. This property may be used to know the unscaled image's size (as [`Height`](Overlay#overlayheight) property scales it), which is useful if the original sprite was disposed, or for textual overlays that generate its own internal image.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.X`](Overlay#overlayx), [`Overlay.Y`](Overlay#overlayy), [`Overlay.GraphicWidth`](Overlay#overlaygraphicwidth), [`Overlay.Height`](Overlay#overlayheight),
[`Overlay.Width`](Overlay#overlaywidth)

---

### `Overlay.GraphicWidth`

    readonly int Overlay.GraphicWidth;

Gets the original width of the overlay's image. This property may be used to know the unscaled image's size (as [`Width`](Overlay#overlaywidth) property scales it), which is useful if the original sprite was disposed, or for textual overlays that generate its own internal image.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.X`](Overlay#overlayx), [`Overlay.Y`](Overlay#overlayy), [`Overlay.GraphicHeight`](Overlay#overlaygraphicheight),
[`Overlay.Width`](Overlay#overlaywidth),
[`Overlay.Height`](Overlay#overlayheight)

---

### `Overlay.Height`

    int Overlay.Height;

Gets/sets the height of this overlay. Changing this property *will stretch or shrink* the overlay's image vertically. Works with both graphical and textual overlays.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.X`](Overlay#overlayx), [`Overlay.Y`](Overlay#overlayy), [`Overlay.Width`](Overlay#overlaywidth)

---

### `Overlay.InRoom`

    readonly bool Overlay.InRoom;

Tells whether current overlay is a room (returns "true") or screen (if "false") overlay.

*See also:* [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical),
[`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.CreateRoomGraphical`](Overlay#overlaycreateroomgraphical),
[`Overlay.CreateRoomTextual`](Overlay#overlaycreateroomtextual)

---

### `Overlay.Transparency`

    int Overlay.Transparency;

Gets/sets the transparency of this overlay.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Object.Transparency`](Object#objecttransparency)
[`Character.Transparency`](Character#charactertransparency),
[`GUI.Transparency`](GUI#guitransparency)

---

### `Overlay.Valid`

*(Formerly known as `IsOverlayValid`, which is now obsolete)*

    readonly bool Overlay.Valid;

Checks whether the overlay is a current overlay or not. Returns 1 if it
is, 0 if it isn't.

Example:

    Overlay* myOverlay = Overlay.CreateTextual(50,80,120,2,15,"This is a text overlay");
    Display("Overlay valid before: %d", myOverlay.Valid);
    myOverlay.Remove();
    Display("Overlay valid after: %d", myOverlay.Valid);

creates an overlay, and prints out the Valid property (which will be 1).
Then, removes the overlay and prints Valid again (which will now be 0).

*See also:* [`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.Remove`](Overlay#overlayremove)

---

### `Overlay.Width`

    int Overlay.Width;

Get/sets the width of this overlay. Changing this property *will stretch or shrink* the overlay's image horizontally. Works with both graphical and textual overlays.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Overlay.X`](Overlay#overlayx), [`Overlay.Y`](Overlay#overlayy), [`Overlay.Height`](Overlay#overlayheight)

---

### `Overlay.X`

*(Formerly known as `MoveOverlay`, which is now obsolete)*

    int Overlay.X;

Gets/sets the X co-ordinate of the overlay (i.e. the left hand side of
the overlay).

This allows you to dynamically move overlays around the screen.

Example:

    Overlay* testOverlay = Overlay.CreateTextual(50,80,120,2,15,"This is a text overlay");
    while (testOverlay.X < 100) {
      testOverlay.X++;
      Wait(1);
    }
    testOverlay.Remove();

creates a text overlay, then gradually slides it across the screen.

*See also:* [`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.Y`](Overlay#overlayy),
[`Overlay.Remove`](Overlay#overlayremove)

---

### `Overlay.Y`

*(Formerly known as `MoveOverlay`, which is now obsolete)*

    int Overlay.Y;

Gets/sets the Y co-ordinate of the overlay (i.e. the top edge of the
overlay).

This allows you to dynamically move overlays around the screen.

Example:

    Overlay* testOverlay = Overlay.CreateTextual(50,50,120,2,15,"This is a text overlay");
    while (testOverlay.Y < 100) {
      testOverlay.Y++;
      Wait(1);
    }
    testOverlay.Remove();

creates a text overlay, then gradually slides it down the screen.

*See also:* [`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.X`](Overlay#overlayx),
[`Overlay.Remove`](Overlay#overlayremove)

---

### `Overlay.ZOrder`

    int Overlay.ZOrder;

Gets/sets the overlay's z-order relative to other overlays and on-screen objects.

The Z-order setting is an arbitrary integer number that can be positive or negative. AGS draws
the Overlays and GUIs in order, from the lowest numbered at the back to the highest numbered at the front.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`GUI.ZOrder`](GUI#guizorder)

