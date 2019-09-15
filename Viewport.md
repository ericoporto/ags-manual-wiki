## Viewport functions and properties

Viewport struct lets you manage screen viewports. You may think of them as of "windows" through which player sees the current room. Viewport is defined by its position on the game screen, in screen coordinates, and has linked Camera which contents it displays.

There's always at least one viewport called "primary viewport", and you may create more. Viewport has a link to camera, and same camera may be linked to multiple viewports at once. If no camera is linked then viewport is not displayed at all. Viewports are allowed to go partially or fully offscreen, which may be useful to create transition effects, for instance. Viewports may overlap, in which case their order of display is defined by [ZOrder](Viewport#zorder) property.

By default viewport covers whole game screen, but you may change that anytime. Camera's contents are stretched to fill viewport's rectangle, and because of that the difference between viewport's and camera's sizes create zoom effect (scaling). If the camera is larger than the viewport that would work as a zoom-out (scale down). If the camera is smaller than the viewport that would work as a zoom-in (scale up).

**IMPORTANT:** The game starts in automatic viewport mode that snaps primary viewport to whole screen and adjusts the camera to the same size (or at least the size of room background) each time new room is loaded. This is convenient in case you want to rely on a common behavior. If you prefer to customize viewports yourself standard behavior may be disabled using [Screen.AutoSizeViewportOnRoomLoad](Screen#autosizeviewportonroomload) property.

*Compatibility:* Viewport struct is supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera](Camera), [Screen.AutoSizeViewportOnRoomLoad](Screen#autosizeviewportonroomload), [Screen.Viewport](Screen#viewport), [Screen.Viewports](Screen#viewports)

---

### Create

    static Viewport* Viewport.Create()

Creates a new viewport and returns a pointer which you may use to operate it. Any viewport created like this may be also accessed by [Screen.Viewports](Screen#viewports) by index.
The new viewport will cover whole game screen by default and does not have any camera linked initially (this is something that you will have to do).

*See Also:* [Viewport.Camera](Viewport#camera), [Viewport.Delete](Viewport#delete), [Screen.Viewport](Screen#viewport), [Screen.Viewports](Screen#viewports)

---

### Delete

    void Viewport.Delete();

Removes an existing viewport. Primary viewport can be never removed and this command issued for the primary viewport will be ignored.

**IMPORTANT:** in **Screen.Viewports** array viewports are arranged in the order they were created. When you delete one in the middle all the following viewports will be shifted towards beginning of array.

*See Also:* [Viewport.Create](Viewport#create), [Screen.Viewport](Screen#viewport), [Screen.Viewports](Screen#viewports)

---

### GetAtScreenXY

    static Viewport* Viewport.GetAtScreenXY(int x, int y)

Finds if there's any viewport at the specified screen coordinates and returns the topmost one. Hidden viewports will not be tested, but those without camera will still be. If no viewport found returns null.

---

### RoomToScreenPoint

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

*See Also:* [Viewport.ScreenToRoomPoint](Viewport#screentoroompoint), [Screen.RoomToScreenPoint](Screen#roomtoscreenpoint), [Screen.ScreenToRoomPoint](Screen#screentoroompoint)

---

### SetPosition

    void Viewport.SetPosition(int x, int y, int width, int height);

Changes viewport's position on the screen.

*See Also:* [Viewport.X](Viewport#x), [Viewport.Y](Viewport#y), [Viewport.Width](Viewport#width), [Viewport.Height](Viewport#height), [Viewport.ZOrder](Viewport#zorder)

---

### ScreenToRoomPoint

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

*See Also:* [Viewport.RoomToScreenPoint](Viewport#screentoroompoint), [Screen.RoomToScreenPoint](Screen#roomtoscreenpoint), [Screen.ScreenToRoomPoint](Screen#screentoroompoint)

---

### Camera

    Camera *Viewport.Camera;

Gets/sets the camera to be displayed in this viewport. Changing cameras is safe anytime, and the looks inside viewport will be changed during next drawing frame.

*See Also:* [Camera.Create](Camera#create), [Game.Camera](Game#camera), [Game.Cameras](Game#cameras)

---

### Height

    int Viewport.Height;

Gets/sets the viewport's height in screen coordinates.

*See Also:* [Viewport.SetPosition](Viewport#setposition), [Viewport.X](Viewport#x), [Viewport.Y](Viewport#y), [Viewport.Width](Viewport#width), [Viewport.ZOrder](Viewport#zorder)

---

### ZOrder

    int Viewport.ZOrder;

Gets/sets the viewport's z-order relative to other viewports. This will be taken into account if multiple viewports overlap.

*See Also:* [Viewport.SetPosition](Viewport#setposition), [Viewport.X](Viewport#x), [Viewport.Y](Viewport#y), [Viewport.Width](Viewport#width), [Viewport.Height](Viewport#height)

---

### Visible

    bool Viewport.Visible;

Gets/sets whether the viewport is enabled and drawn on screen.

---

### Width

    int Viewport.Width;

Gets/sets the viewport's width in screen coordinates.

*See Also:* [Viewport.SetPosition](Viewport#setposition), [Viewport.X](Viewport#x), [Viewport.Y](Viewport#y), [Viewport.Height](Viewport#height), [Viewport.ZOrder](Viewport#zorder)

---

### X

    int Viewport.X;

Gets/sets the X position on the screen where this viewport is located.

*See Also:* [Viewport.SetPosition](Viewport#setposition), [Viewport.Y](Viewport#y), [Viewport.Width](Viewport#width), [Viewport.Height](Viewport#height), [Viewport.ZOrder](Viewport#zorder)

---

### Y

    int Viewport.Y;

Gets/sets the Y position on the screen where this viewport is located.

*See Also:* [Viewport.SetPosition](Viewport#setposition), [Viewport.X](Viewport#x), [Viewport.Width](Viewport#width), [Viewport.Height](Viewport#height), [Viewport.ZOrder](Viewport#zorder)