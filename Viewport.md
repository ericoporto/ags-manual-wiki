## `Viewport` functions and properties

Viewport struct lets you manage screen viewports. You may think of them as of "windows" through which player sees the current room. Viewport is defined by its position on the game screen, in screen coordinates, and has linked Camera which contents it displays.

There's always at least one viewport called "primary viewport", and you may create more. Viewport has a link to camera, and same camera may be linked to multiple viewports at once. If no camera is linked then viewport is not displayed at all. Viewports are allowed to go partially or fully offscreen, which may be useful to create transition effects, for instance. Viewports may overlap, in which case their order of display is defined by [ZOrder](Viewport#viewportzorder) property.

By default viewport covers whole game screen, but you may change that anytime. Camera's contents are stretched to fill viewport's rectangle, and because of that the difference between viewport's and camera's sizes create zoom effect (scaling). If the camera is larger than the viewport that would work as a zoom-out (scale down). If the camera is smaller than the viewport that would work as a zoom-in (scale up).

**IMPORTANT:** The game starts in automatic viewport mode that snaps primary viewport and camera to the size of the game screen or size of a room background, whatever is *smaller*, each time new room is loaded. This is convenient in case you want to rely on a common behavior. If you prefer to customize viewports yourself standard behavior may be disabled using [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload) property.

*Compatibility:* Viewport struct is supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera](Camera), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload), [Screen.Viewport](Screen#screenviewport), [Screen.Viewports](Screen#screenviewports)

---

### `Viewport.Create`

    static Viewport* Viewport.Create()

Creates a new viewport and returns a pointer which you may use to operate it. Any viewport created like this may be also accessed by [Screen.Viewports](Screen#screenviewports) by index.
The new viewport will cover whole game screen by default and does not have any camera linked initially (this is something that you will have to do).

*See Also:* [Viewport.Camera](Viewport#viewportcamera), [Viewport.Delete](Viewport#viewportdelete), [Screen.Viewport](Screen#screenviewport), [Screen.Viewports](Screen#screenviewports)

---

### `Viewport.Delete`

    void Viewport.Delete();

Removes an existing viewport. Primary viewport can be never removed and this command issued for the primary viewport will be ignored.

**IMPORTANT:** in **Screen.Viewports** array viewports are arranged in the order they were created. When you delete one in the middle all the following viewports will be shifted towards beginning of array.

*See Also:* [Viewport.Create](Viewport#viewportcreate), [Screen.Viewport](Screen#screenviewport), [Screen.Viewports](Screen#screenviewports)

---

### `Viewport.GetAtScreenXY`

    static Viewport* Viewport.GetAtScreenXY(int x, int y)

Finds if there's any viewport at the specified screen coordinates and returns the topmost one. Hidden viewports will not be tested, but those without camera will still be. If no viewport found returns null.

---

### `Viewport.RoomToScreenPoint`

    Point* Viewport.RoomToScreenPoint(int roomx, int roomy, bool clipViewport = true);

Returns the point on screen corresponding to the given room coordinates if seen through this viewport. Resulting Point struct will contain screen x and y coordinates.

Function does the conversion from room to screen's coordinate system, correctly taking into account viewport's position on screen, camera's position in the room and its transformation (scaling etc).

If **clipViewport** is true then this function will only return a point if given room coordinates are currently seen inside viewport and return null otherwise. If **clipViewport** is false then viewport's bounds will be ignored.

Example:

    Point* pt = myViewport.RoomToScreenPoint(player.x, player.y);
    if (pt != null) {
      Display("Player character is displayed at (%d, %d) on screen.", pt.x, pt.y);
    } else {
      Display("Player character is currently offscreen.");
    }

*See Also:* [Viewport.ScreenToRoomPoint](Viewport#viewportscreentoroompoint), [Screen.RoomToScreenPoint](Screen#screenroomtoscreenpoint), [Screen.ScreenToRoomPoint](Screen#screenscreentoroompoint)

---

### `Viewport.SetPosition`

    void Viewport.SetPosition(int x, int y, int width, int height);

Changes viewport's position on the screen.

*See Also:* [Viewport.X](Viewport#viewportx), [Viewport.Y](Viewport#viewporty), [Viewport.Width](Viewport#viewportwidth), [Viewport.Height](Viewport#viewportheight), [Viewport.ZOrder](Viewport#viewportzorder), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Viewport.ScreenToRoomPoint`

    Point* Viewport.ScreenToRoomPoint(int scrx, int scry, bool clipViewport = true);

Returns the point in room corresponding to the given screen coordinates if seen through this viewport. Resulting Point struct will contain room x and y coordinates.

Function does the conversion from screen to room's coordinate system, correctly taking into account viewport's location on screen, camera's position in the room and its transformation (scaling etc).

If **clipViewport** is true then this function will only return a point if given screen coordinates are over viewport and return null otherwise. If **clipViewport** is false then viewport's bounds will be ignored.

Example:

    Point* pt = myViewport.ScreenToRoomPoint(mouse.x, mouse.y);
    if (pt != null) {
      Display("Mouse cursor is over room location: (%d, %d).", pt.x, pt.y);
    } else {
      Display("Mouse cursor is currently outside the viewport.");
    }

*See Also:* [Viewport.RoomToScreenPoint](Viewport#viewportscreentoroompoint), [Screen.RoomToScreenPoint](Screen#screenroomtoscreenpoint), [Screen.ScreenToRoomPoint](Screen#screenscreentoroompoint)

---

### `Viewport.Camera`

    Camera *Viewport.Camera;

Gets/sets the camera to be displayed in this viewport. Changing cameras is safe anytime, and the looks inside viewport will be changed during next drawing frame.

*See Also:* [Camera.Create](Camera#cameracreate), [Game.Camera](Game#gamecamera), [Game.Cameras](Game#gamecameras)

---

### `Viewport.Height`

    int Viewport.Height;

Gets/sets the viewport's height in screen coordinates.

*See Also:* [Viewport.SetPosition](Viewport#viewportsetposition), [Viewport.X](Viewport#viewportx), [Viewport.Y](Viewport#viewporty), [Viewport.Width](Viewport#viewportwidth), [Viewport.ZOrder](Viewport#viewportzorder), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Viewport.ZOrder`

    int Viewport.ZOrder;

Gets/sets the viewport's z-order relative to other viewports. This will be taken into account if multiple viewports overlap to define which should be displayed above and which below.

The z-order is an arbitrary number and only have meaning in comparison with other viewport's setting. Similarly to [GUI.ZOrder](GUI#guizorder), the lower value puts viewport to the back and higher value to the top.

*See Also:* [Viewport.SetPosition](Viewport#viewportsetposition), [Viewport.X](Viewport#viewportx), [Viewport.Y](Viewport#viewporty), [Viewport.Width](Viewport#viewportwidth), [Viewport.Height](Viewport#viewportheight)

---

### `Viewport.Visible`

    bool Viewport.Visible;

Gets/sets whether the viewport is enabled and drawn on screen.

---

### `Viewport.Width`

    int Viewport.Width;

Gets/sets the viewport's width in screen coordinates.

*See Also:* [Viewport.SetPosition](Viewport#viewportsetposition), [Viewport.X](Viewport#viewportx), [Viewport.Y](Viewport#viewporty), [Viewport.Height](Viewport#viewportheight), [Viewport.ZOrder](Viewport#viewportzorder), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Viewport.X`

    int Viewport.X;

Gets/sets the X position on the screen where this viewport is located.

*See Also:* [Viewport.SetPosition](Viewport#viewportsetposition), [Viewport.Y](Viewport#viewporty), [Viewport.Width](Viewport#viewportwidth), [Viewport.Height](Viewport#viewportheight), [Viewport.ZOrder](Viewport#viewportzorder), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Viewport.Y`

    int Viewport.Y;

Gets/sets the Y position on the screen where this viewport is located.

*See Also:* [Viewport.SetPosition](Viewport#viewportsetposition), [Viewport.X](Viewport#viewportx), [Viewport.Width](Viewport#viewportwidth), [Viewport.Height](Viewport#viewportheight), [Viewport.ZOrder](Viewport#viewportzorder), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)
