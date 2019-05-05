## Camera

### Create

    static Camera *Create();

Creates a new Camera.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.Delete](Camera#delete)


### Delete

    void Delete();

Removes an existing camera; note that primary camera will never be removed.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.Create](Camera#create)

### SetAt

    void SetAt(int x, int y);

Changes camera position in the room and disables automatic tracking of the player character.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.SetSize](Camera#setsize)


### SetSize

    void SetSize(int width, int height);

Changes camera's capture dimensions in room coordinates.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.SetAt](Camera#setat)


### AutoTracking

    attribute bool AutoTracking;

Gets/sets whether this camera will follow the player character automatically.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.




### Width

    attribute int Camera.Width;

Gets/sets the camera's capture width in room coordinates.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.Height](Camera#height)

### Height

    attribute int Camera.Height;

Gets/sets the camera's capture height in room coordinates.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.Width](Camera#width)

### X

    static int Camera.X;

Gets/sets the X position of this camera in the room.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.Y](Camera#y)


### Y

    static int Camera.Y;

Gets/sets the Y position of this camera in the room.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Camera.X](Camera#x)