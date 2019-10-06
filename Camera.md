## `Camera` functions and properties

Camera struct lets you manage room cameras. Camera is like a rectangular "eye" that floats above the room and captures what it sees. Captured camera's image may then be translated somewhere else. Right now AGS only supports drawing camera's contents over viewport on screen, but its uses may be extended in future.

Camera is defined by its size and position inside the room. The larger camera's rectangle is - the more room space will be seen at once. Camera cannot be larger than the current room's background though. Also it is forbidden to move camera outside of the room background, even by a pixel.

There's always at least one camera called "primary camera", and you may create more. Note that, although cameras display the room, in their current implementation they are considered global persistent objects and automatically change rooms with player's character.

Cameras are linked to the viewports using [Viewport.Camera](Viewport#viewportcamera) property. A camera may be thus linked to any number of different viewports, in which case they all will display same place in the room.

By default camera's size is set equal to room background or game screen size, whatever is *smaller*, but you may change that anytime. When camera is linked to a viewport the camera's contents are stretched to fill viewport's rectangle, and because of that the difference between viewport's and camera's sizes create zoom effect (scaling). If the camera is larger than the viewport that would work as a zoom-out (scale down). If the camera is smaller than the viewport that would work as a zoom-in (scale up).

By default camera follows player character, this is called "auto-tracking". You may override this by disabling [Camera.AutoTracking](Camera#cameraautotracking) property.

**IMPORTANT:** The game starts in automatic viewport mode that snaps primary viewport and camera to the size of the game screen or size of a room background, whatever is *smaller*, each time new room is loaded. This is convenient in case you want to rely on a common behavior. If you prefer to customize cameras yourself standard behavior may be disabled using [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload) property.

*Compatibility:* Camera struct is supported by **AGS 3.5.0** and later versions.

*See Also:* [Viewport](Viewport), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload), [Game.Camera](Game#gamecamera), [Game.Cameras](Game#gamecameras)

---

### `Camera.Create`

    static Camera* Camera.Create();

Creates a new camera and returns a pointer which you may use to operate it. Any camera created like this may be also accessed by [Game.Cameras](Game#gamecameras) by index.
The new camera will by default be located at the room's (0, 0) and assigned a size of game screen or room background, whatever is *smaller*. It will also be autotracking. You may change any of its properties later.

*See Also:* [Camera.Delete](Camera#cameradelete), [Game.Camera](Game#gamecamera), [Game.Cameras](Game#gamecameras), [Viewport.Camera](Viewport#viewportcamera)

---

### `Camera.Delete`

    void Camera.Delete();

Removes an existing camera. Primary camera can be never removed and this command issued for the primary camera will be ignored.

**IMPORTANT:** in **Game.Cameras** array cameras are arranged in the order they were created. When you delete one in the middle all the following cameras will be shifted towards beginning of array.

*See Also:* [Camera.Create](Camera#cameracreate), [Game.Camera](Game#gamecamera), [Game.Cameras](Game#gamecameras)

---

### `Camera.SetAt`

    void Camera.SetAt(int x, int y);

Changes camera position in the room and disables automatic tracking of the player character.

*See Also:* [Camera.SetSize](Camera#camerasetsize), [Camera.AutoTracking](Camera#cameraautotracking), [Camera.X](Camera#camerax), [Camera.Y](Camera#cameray), [Camera.Width](Camera#camerawidth), [Camera.Height](Camera#cameraheight)

---

### `Camera.SetSize`

    void Camera.SetSize(int width, int height);

Changes camera's capture dimensions in room coordinates.

If the camera's size is larger than the viewport it is drawn in then the room will be scaled down (zoom-out effect), if camera is smaller than the viewport then the room will be scaled up (zoom-in effect).

*See Also:* [Camera.SetAt](Camera#camerasetat), [Camera.X](Camera#camerax), [Camera.Y](Camera#cameray), [Camera.Width](Camera#camerawidth), [Camera.Height](Camera#cameraheight), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Camera.AutoTracking`

    bool Camera.AutoTracking;

Gets/sets whether this camera will follow the player character automatically. Otherwise camera retains its position until you change it in script or turn tracking back on.

*See Also:* [Camera.SetAt](Camera#camerasetat), [Camera.X](Camera#camerax), [Camera.Y](Camera#cameray)

---

### `Camera.Height`

    int Camera.Height;

Gets/sets the camera's capture height in room coordinates.

*See Also:* [Camera.SetAt](Camera#camerasetat), [Camera.SetSize](Camera#camerasetsize), [Camera.X](Camera#camerax), [Camera.Y](Camera#cameray), [Camera.Width](Camera#camerawidth), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Camera.Width`

    int Camera.Width;

Gets/sets the camera's capture width in room coordinates.

*See Also:* [Camera.SetAt](Camera#camerasetat), [Camera.SetSize](Camera#camerasetsize), [Camera.X](Camera#camerax), [Camera.Y](Camera#cameray), [Camera.Height](Camera#cameraheight), [Screen.AutoSizeViewportOnRoomLoad](Screen#screenautosizeviewportonroomload)

---

### `Camera.X`

    int Camera.X;

Gets/sets the X position of this camera in the room. If you assign new value that will disable automatic tracking.

*See Also:* [Camera.SetAt](Camera#camerasetat), [Camera.SetSize](Camera#camerasetsize), [Camera.AutoTracking](Camera#cameraautotracking), [Camera.Y](Camera#cameray), [Camera.Width](Camera#camerawidth), [Camera.Height](Camera#cameraheight)

---

### `Camera.Y`

    int Camera.Y;

Gets/sets the Y position of this camera in the room. If you assign new value that will disable automatic tracking.

*See Also:* [Camera.SetAt](Camera#camerasetat), [Camera.SetSize](Camera#camerasetsize), [Camera.AutoTracking](Camera#cameraautotracking), [Camera.X](Camera#camerax), [Camera.Width](Camera#camerawidth), [Camera.Height](Camera#cameraheight)
