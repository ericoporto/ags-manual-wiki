## Viewport

### Create

    static Viewport *Create();

Creates a new Viewport.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.Delete](Viewport#delete)


### Delete

    void Delete();

Removes an existing viewport; note that primary viewport will never be removed.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.Create](Viewport#create)


### GetAtScreenXY

    static Viewport *GetAtScreenXY(int x, int y);

Returns the viewport at the specified screen location.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.Delete](Viewport#delete), [Viewport.Create](Viewport#create)


### SetPosition

    void SetPosition(int x, int y, int width, int height);

Changes viewport's position on the screen.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.


### ScreenToRoomPoint

    Point *ScreenToRoomPoint(int scrx, int scry, bool clipViewport = true);

Returns the point in room corresponding to the given screen coordinates if seen through this viewport.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.RoomToScreenPoint](Viewport#roomtoscreenpoint)


### RoomToScreenPoint

    Point *RoomToScreenPoint(int roomx, int roomy, bool clipViewport = true);

Returns the point on screen corresponding to the given room coordinates if seen through this viewport.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.ScreenToRoomPoint](Viewport#screentoroompoint)


### ZOrder

    attribute int ZOrder;

Gets/sets the Viewport's z-order relative to other viewports.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.


### Visible

    attribute bool Visible;

Gets/sets whether the viewport is drawn on screen.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.



### Camera

    attribute Camera *Camera;

Gets/sets the room camera displayed in this viewport.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.Create](Camera#create)


### Width

    attribute int Viewport.Width;

Gets/sets the viewport's width in screen coordinates.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.Height](Viewport#height)

### Height

    attribute int Viewport.Height;

Gets/sets the viewport's height in screen coordinates.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.Width](Viewport#width)

### X

    static int Viewport.X;

Gets/sets the X position on the screen where this viewport is located.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.Y](Viewport#y)


### Y

    static int Viewport.Y;

Gets/sets the Y position on the screen where this viewport is located.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport.X](Viewport#x)