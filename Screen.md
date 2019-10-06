## `Screen` Functions and Properties

Screen is a new small struct that provides access to viewports and conversion between screen and room coordinates. 

*Compatibility:* Screen struct is supported by **AGS 3.5.0** and later versions.

---

### `Screen.RoomToScreenPoint`

    static Point* Screen.RoomToScreenPoint(int rx, int ry);

Returns the point on screen corresponding to the given room coordinates if seen through **the primary viewport**. Resulting Point struct will contain screen x and y coordinates.

Function does the conversion from room to screen's coordinate system, correctly taking into account viewport's position on screen, camera's position in the room and its transformation (scaling etc).

This is a convenience function which is used when you do not manage viewports yourself but just using default one. If you have more than one custom viewport in your room consider [Viewport.RoomToScreenPoint](Viewport#viewportroomtoscreenpoint) instead.

*See Also:* [Screen.ScreenToRoomPoint](Screen#screenscreentoroompoint), [Viewport.RoomToScreenPoint](Viewport#viewportroomtoscreenpoint), [Viewport.ScreenToRoomPoint](Viewport#viewportscreentoroompoint)

---

### `Screen.ScreenToRoomPoint`

    static Point* Screen.ScreenToRoomPoint(int sx, int sy);

Returns the point in room corresponding to the given screen coordinates, but only if there's at least one visible viewport at that location. The conversion is done if seen through *the topmost viewport*. Resulting Point struct will contain room x and y coordinates.

If there are no viewports found there then this function returns null.

Function does the conversion from screen to room's coordinate system, correctly taking into account viewport's location on screen, camera's position in the room and its transformation (scaling etc).

*See Also:* [Screen.RoomToScreenPoint](Screen#screenroomtoscreenpoint), [Viewport.RoomToScreenPoint](Viewport#viewportroomtoscreenpoint), [Viewport.ScreenToRoomPoint](Viewport#viewportscreentoroompoint), [Viewport.Visible](Viewport#viewportvisible), [Viewport.ZOrder](Viewport#viewportzorder)

---

### `Screen.AutoSizeViewportOnRoomLoad`

    static bool Screen.AutoSizeViewportOnRoomLoad;

Gets/sets whether the game should automatically adjust primary viewport and primary camera to the size of the room background each time the new room is loaded. This setting is **enabled** by default, and is the standard viewport behavior in AGS.

When this setting is on then every time the new room is loaded primary viewport and camera will be resized to match either the size of a room's background or game screen, whatever is *smaller*. The viewport will also be centered on game screen.

For example, if game is 320x200 and room is also 320x200, then both viewport and camera will be resized to 320x200 and cover whole screen.
If game is 320x200 and room is 160x160, then both viewport and camera will be resized to 160x160 and viewport positioned in the center of screen (at 80, 20).
If game is 320x200 and room is 400x200, then both viewport and camera will be resized to 320x200 again, and you'll have a scrolling room (one that is only partially seen at any time).

*See Also:* [Viewport.SetPosition](Viewport#viewportsetposition), [Camera.SetSize](Camera#camerasetsize)

---

### `Screen.Height`

*(Replaces System.ScreenHeight, which is now obsolete)*<br>
*(Replaces System.ViewportHeight, which is now obsolete)*

    static readonly int Screen.Height;

Gets the native height of the game screen in pixels, which matches game resolution you set in the Editor.

**NOTE:** this is the game screen's logical size before any additional scaling is applied by the graphics renderer. It may or not be equal to the dimension of the final game image on player's display.

---

### `Screen.Width`

*(Replaces System.ScreenWidth, which is now obsolete)*<br>
*(Replaces System.ViewportWidth, which is now obsolete)*

    static readonly int Screen.Width;

Gets the native width of the game screen in pixels, which matches game resolution you set in the Editor.

**NOTE:** this is the game screen's logical size before any additional scaling is applied by the graphics renderer. It may or not be equal to the dimension of the final game image on player's display.

---

### `Screen.Viewport`

    static readonly Viewport *Screen.Viewport;

Gets the primary room viewport. This is the default viewport that is created automatically at the start of the game and cannot be deleted.

*See Also:* [Screen.Viewports](Screen#screenviewports), [Viewport](Viewport), [Viewport.Create](Viewport#viewportcreate), [Viewport.Delete](Viewport#viewportdelete), [Game.Camera](Game#gamecamera)

---

### `Screen.ViewportCount`

    static readonly int Screen.ViewportCount;

Gets the number of viewports.

*See Also:* [Screen.Viewports](Screen#screenviewports)

---

### `Screen.Viewports`

    static readonly Viewport* Screen.Viewports[int index];

Returns the Viewport instance by its index. There's always at least primary viewport at the index 0, more could be created in script using [Viewport.Create](Viewport#viewportcreate).

**IMPORTANT:** with the current implementation when you delete a custom viewport in the middle all the following viewports will be shifted towards beginning of array, changing their indexes.

Example:

    for (int i = 0; i < Screen.ViewportCount; i++) {
        Screen.Viewports[i].Visible = false;
    }

Above disables (hides) all of the existing viewports.

*See Also:* [Screen.Viewport](Screen#screenviewport), [Screen.ViewportCount](Screen#screenviewportcount), [Viewport.Create](Viewport#viewportcreate), [Viewport.Delete](Viewport#viewportdelete), [Game.Cameras](Game#gamecameras)
