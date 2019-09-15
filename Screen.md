## Screen Functions and Properties

Screen struct has properties where you can retrieve the current game resolution width and height, and also references to existing viewports. Additionally, screen provides convenience functions to help with point conversion between room and screen coordinates. 

---

### ScreenToRoomPoint

    static Point * Screen.ScreenToRoomPoint(int sx, int sy)

Converts a point displayed in the screen to the corresponding room coordinates. This function returns null if there is no Viewport on screen under these coordinates. This is because if there will be multiple viewports supported in the future then engine simply won't know which to choose having none under these coords.

*See Also:* [Viewport.RoomToScreenPoint](Viewport#roomtoscreenpoint), [Viewport.ScreenToRoomPoint](Viewport#screentoroompoint), [Screen.RoomToScreenPoint](Screen#roomtoscreenpoint)

---

### RoomToScreenPoint

    static Point *RoomToScreenPoint(int rx, int ry)

Returns an object of Point type containing on screen (x,y) coordinates, corresponding to the given room coordinates relative to the main viewport.

*See Also:* [Viewport.RoomToScreenPoint](Viewport#roomtoscreenpoint), [Viewport.ScreenToRoomPoint](Viewport#screentoroompoint), [Screen.ScreenToRoomPoint](Screen#screentoroompoint)

---

### Width

    static readonly attribute int Width

Gets the width of the game resolution.

---

### Height

    static readonly attribute int Heigh

Gets the height of the game resolution.

---

### AutoSizeViewportOnRoomLoad

    static attribute bool AutoSizeViewportOnRoomLoad

Gets/sets whether the viewport should automatically adjust itself and camera to the new room's background size.

---

### Viewport

    static readonly attribute Viewport *Viewport

Gets the primary room viewport.

*See Also:* [Viewport.Create](Viewport#create), [Viewport.Delete](Viewport#delete)

---

### Viewports

    static readonly attribute Viewport *Viewports[]

Gets a Viewport by index.

*See Also:* [Viewport.Create](Viewport#create), [Viewport.Delete](Viewport#delete)

---

### ViewportCount

    static readonly attribute int ViewportCount

Gets the number of viewports.

*See Also:* [Viewport.Create](Viewport#create), [Viewport.Delete](Viewport#delete)