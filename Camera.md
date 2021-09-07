## `Camera` functions and properties

The Camera struct lets you manage room cameras. Each camera may be considered a rectangular viewer that looks into the room and captures what it sees. This captured image may then be translated somewhere else. Right now AGS only supports drawing what a camera can see within a [`Viewport`](Viewport), but its uses may be extended in the future.

Cameras have a variable size and position within the room. The camera's size (i.e. the viewing rectangle) is linked to how much of the room they can see, the larger the size the larger the visible portion of the room. The maximum camera size is determined by the dimensions of the room background, so it may not be larger than the room. It is not possible to move the camera beyond the edges of the room background, even by a pixel.

By default there is a single camera, known as the "primary camera", and you may create more. Note that, although cameras display the room, in their current implementation they are considered global persistent objects and will automatically change rooms with the player's character.

Cameras are linked to a Viewport using the [`Viewport.Camera`](Viewport#viewportcamera) property. A camera may be linked to any number of different Viewports, in which case all of the Viewports will display the same image of the room. When a camera is linked to a Viewport the camera's contents are stretched to fill Viewport's rectangle, the difference in size between the viewport and the camera determines the level of scaling that is applied:

* If the camera is larger than the viewport the displayed image will be zoomed-out (scaled down)
* If the camera is smaller than the viewport the displayed image will be zoomed-in (scaled up)

By default each camera follows the player character, this is know as "auto-tracking". You may override this by disabling [`Camera.AutoTracking`](Camera#cameraautotracking) property.

**IMPORTANT:** Cameras are initialized with an automatic sizing mode that snaps the primary Viewport and the camera to the size of the game screen or size of a room background (whichever is *smaller*), each time that a new room is loaded. This is convenient if you want to rely on a common behavior. If you prefer to manage the sizing  yourself this behavior may be disabled using the [`Screen.AutoSizeViewportOnRoomLoad`](Screen#screenautosizeviewportonroomload) property.

*Compatibility:* The Camera struct is supported by **AGS 3.5.0** and later versions.

*See also:* [`Viewport`](Viewport), [`Screen.AutoSizeViewportOnRoomLoad`](Screen#screenautosizeviewportonroomload), [`Game.Camera`](Game#gamecamera), [`Game.Cameras`](Game#gamecameras)

---

### `Camera.Create`

    static Camera* Camera.Create();

Creates a new camera and returns a pointer which you may use to operate it. Any camera created like this may be also accessed at [`Game.Cameras`](Game#gamecameras) by index.
The new camera will, by default, be located at the room's origin (0, 0) and be sized to fit either the game screen or the room background, whichever is *smaller*. It will also have auto-tracking enabled. You may change any of its properties later.

*See also:* [`Camera.Delete`](Camera#cameradelete), [`Game.Camera`](Game#gamecamera), [`Game.Cameras`](Game#gamecameras), [`Viewport.Camera`](Viewport#viewportcamera)

---

### `Camera.Delete`

    void Camera.Delete();

Removes an existing camera.

**IMPORTANT:** The "primary camera" can be never removed and calling this function on it will have no effect.

**IMPORTANT:** In the **Game.Cameras** array cameras are arranged in the order they were created. If you delete one from the middle all of the cameras with a higher index will be shifted towards the beginning of array.

*See also:* [`Camera.Create`](Camera#cameracreate), [`Game.Camera`](Game#gamecamera), [`Game.Cameras`](Game#gamecameras)

---

### `Camera.SetAt`

    void Camera.SetAt(int x, int y);

Changes the camera's position in the room and disables automatic tracking of the player character.

*See also:* [`Camera.SetSize`](Camera#camerasetsize), [`Camera.AutoTracking`](Camera#cameraautotracking), [`Camera.X`](Camera#camerax), [`Camera.Y`](Camera#cameray), [`Camera.Width`](Camera#camerawidth), [`Camera.Height`](Camera#cameraheight)

---

### `Camera.SetSize`

    void Camera.SetSize(int width, int height);

Changes the camera's capture dimensions, in room coordinates.

If the camera's size is larger than the Viewport it is drawn in, then the room will be scaled down (producing a zoomed-out effect). If the camera's size is smaller than the Viewport then the room will be scaled up (producing a zoomed-in effect).

*See also:* [`Camera.SetAt`](Camera#camerasetat), [`Camera.X`](Camera#camerax), [`Camera.Y`](Camera#cameray), [`Camera.Width`](Camera#camerawidth), [`Camera.Height`](Camera#cameraheight), [`Screen.AutoSizeViewportOnRoomLoad`](Screen#screenautosizeviewportonroomload)

---

### `Camera.AutoTracking`

    bool Camera.AutoTracking;

Gets/sets whether this camera will automatically follow the player character's position in the room. When disabled, the camera retains its position until you change it using script commands or turn auto-tracking back on.

*See also:* [`Camera.SetAt`](Camera#camerasetat), [`Camera.X`](Camera#camerax), [`Camera.Y`](Camera#cameray)

---

### `Camera.Height`

    int Camera.Height;

Gets/sets the camera's capture height in room coordinates.

*See also:* [`Camera.SetAt`](Camera#camerasetat), [`Camera.SetSize`](Camera#camerasetsize), [`Camera.X`](Camera#camerax), [`Camera.Y`](Camera#cameray), [`Camera.Width`](Camera#camerawidth), [`Screen.AutoSizeViewportOnRoomLoad`](Screen#screenautosizeviewportonroomload)

---

### `Camera.Width`

    int Camera.Width;

Gets/sets the camera's capture width in room coordinates.

*See also:* [`Camera.SetAt`](Camera#camerasetat), [`Camera.SetSize`](Camera#camerasetsize), [`Camera.X`](Camera#camerax), [`Camera.Y`](Camera#cameray), [`Camera.Height`](Camera#cameraheight), [`Screen.AutoSizeViewportOnRoomLoad`](Screen#screenautosizeviewportonroomload)

---

### `Camera.X`

    int Camera.X;

Gets/sets the X position of this camera in the room. Setting a value will also disable auto-tracking.

*See also:* [`Camera.SetAt`](Camera#camerasetat), [`Camera.SetSize`](Camera#camerasetsize), [`Camera.AutoTracking`](Camera#cameraautotracking), [`Camera.Y`](Camera#cameray), [`Camera.Width`](Camera#camerawidth), [`Camera.Height`](Camera#cameraheight)

---

### `Camera.Y`

    int Camera.Y;

Gets/sets the Y position of this camera in the room. Setting a value will also disable auto-tracking.

*See also:* [`Camera.SetAt`](Camera#camerasetat), [`Camera.SetSize`](Camera#camerasetsize), [`Camera.AutoTracking`](Camera#cameraautotracking), [`Camera.X`](Camera#camerax), [`Camera.Width`](Camera#camerawidth), [`Camera.Height`](Camera#cameraheight)
