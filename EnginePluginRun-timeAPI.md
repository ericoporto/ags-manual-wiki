## Engine Plugin Run-time API

### Run-time events

#### AGS_EngineStartup
```
DLLEXPORT void AGS_EngineStartup (IAGSEngine *lpGame);
```

Called by the game engine when the game is loading. This function is called once AGS has loaded everything it needs to into memory, but before it loads the global script.  

Your plugin should use this opportunity to register any text script functions that it provides, and to request hooks for any game events that it wants to handle.

Once this function completes, the plugin will only regain program control when one of its text script functions is called, or when one of the hooks it registered is executed.

_![Info icon](images/icon_info.png)_ This function is called before the graphics subsystem is started, so functions like GetScreenDimensions and GetGraphicsDriverID will not work if called from this event. 

#### AGS_EngineShutdown
```
DLLEXPORT void AGS_EngineShutdown();
```

Called by the game engine just before it exits. This gives you a chance to free any memory and do any cleanup that you need to do before the engine shuts down.

_(Shutdown is only called by engine interface version 13 and above.)_

#### AGS_EngineOnEvent
```
DLLEXPORT int AGS_EngineOnEvent (int event, int data);
```

Called by the game engine when one of the events which the plugin has requested via RequestEventHook is triggered.  
`data` is an event-specific parameter - see RequestEventHook below for more information.

Return 0 to tell the engine to continue processing the event as normal. Return 1 to tell the engine not to call any other handlers, whether in other plugins or the text script, for this event.

For example, if you were handling a Keypress event, and you did something in response to the keystroke, you may wish to return 1 to stop anything else also dealing with the keystroke.

_![Warning](images/icon_warn.png)_ Only return 1 when absolutely necessary since it may interfere with other plugins operation.

#### AGS_EngineDebugHook
```
DLLEXPORT int AGS_EngineDebugHook(const char * scriptName, int lineNum, int reserved);
```

Called by the game engine when a new line of text script is about to be executed. This will only be called if you have requested the AGSE_SCRIPTDEBUG event with the RequestEventHook function (see below).

`scriptName` contains which script is running (either "Global script" or "Room XX script" (where XX is the room number)). `lineNum` contains the line number that is about to be run.

This callback is designed to allow you to create some form of script debugger using a plugin. Note that just having this hook enabled will cause a performance hit in the game - so if the plugin is not actively debugging, it should use `UnregisterEventHook` to unregister itself until such time as it needs to know again.

This callback is also called with `lineNum` set to 0 when a script finishes running.

Return 1 if you handled the debug, or 0 to allow other plugins to have a go.

_(Supported by engine interface version 13 and above)_

#### AGS_EngineInitGfx
```
DLLEXPORT void AGS_EngineInitGfx(const char *driverID, void *data);
```

Called by AGS just before the graphics driver is initialized. This allows you to make changes to how the driver starts up.

`driverID` is the ID of the graphics driver in use. This can either be "D3D9" if the player is using the Direct3D driver, or "DX5" if they are using the standard DirectDraw driver.

If `driverID` is "D3D9", then the `data` parameter is a pointer to the `D3DPRESENT_PARAMETERS` structure that AGS is about to pass into CreateDevice. If you need to enable extra features such as the Auto Depth Stencil, then you can do so by changing the member variables at this point.

If `driverID` is "DX5", then the `data` parameter will currently be passed as `NULL`.

_![Info icon](images/icon_info.png)_ This event is called just as the graphics subsystem is starting, so functions that like GetScreenDimensions that rely on the screen being initialized will not work if called from this event. 

_![Info icon](images/icon_info.png)_ This event can be called more than once. It is called every time AGS tries to initialize the screen, so if the first resolution is not supported for example then it will get called again as AGS retries.

_(Supported by engine interface version 23 and above)_

### The IAGSEngine interface

This interface is provided to the plugin as the way of calling back to the editor. It provides the following methods.

_![Warning](images/icon_warn.png)_ Very little error checking is performed on these functions for performance reasons, as they provide direct entry into AGS - therefore, mistakes in your code can crash the engine.

The text script currently supports `char`, `short` and `int` types. These are 1, 2 and 4 byte integers respectively. Text script strings are implemented as standard C-style `char*` pointers, but with preallocated buffers of 200 bytes per string. Therefore, if you write a function which takes a string from the text script, make sure that if you add anything to it you don't write past 200 characters, or problems will result.

#### IAGSEngine.version
```
int version;
```

Specifies the interface version. You should check this to determine what version of the engine is being used, because certain interface methods will have been added in later versions, and attempting to use them with an earlier version will crash the system.  

AGS v2.51 (the first version to support plugins) was distributed with interface version **7**, so you can reasonably expect that as a minimum for your plugin.

#### IAGSEngine.AbortGame
```
void AbortGame (const char * reason);
```

Aborts the game, presenting the standard AGS "An error has occured, please correct the problem" message box to the user, with the error description being the string supplied.  

To indicate that it was a user error (for example, they provided an invalid parameter to your text script function), prepend a ! to the message. For example,  

```
AbortGame ("!MyScriptFunction: Not a valid color");
```

This will use the "Please contact the game author for support" heading message.

If you need to exit the game, you should always use this instead of the standard VC++ exit() functions.

_Added in version: 1_

#### IAGSEngine.GetEngineVersion
```
const char* GetEngineVersion ();
```

Returns the full build number of the engine, for example "2.51.400". You can use this with strcmp if your plugin requires a specific engine version. 

_Added in version: 1_

#### IAGSEngine.RegisterScriptFunction
```
void RegisterScriptFunction (const char *name, void *address);
```

Allows you to add your own text script functions to AGS. `name` is the name of the function as the script knows it, for example "AddNumbers". `address` is a pointer to your function that implements the command. For example:

```
int AddNumbers (int a, int b) { return a + b; }  
...  
RegisterScriptFunction ("AddNumbers", AddNumbers);
```

Note that it is possible to override the built-in functions with this command. If you do, for example,  
```
RegisterScriptFunction ("GetLocationType", AddNumbers);
```
then any calls from the script to `GetLocationType` will be intercepted by your plugin (and in this case a stupid result returned).

_![Warning](images/icon_warn.png)_ If you want to override built-in functions, make sure that yours have identical parameters, otherwise the stack could get messed up and crash the engine.

AGS 2.7 and later support object-based scripting. In order to export an object from your plugin, you'll need to include its struct definition in the RegisterScriptHeader editor call. Then, you export functions as follows:

```
int PluginObject_DoSomething(PluginObject *obj, int a) {  
  return a + 10;  
}  
...  
RegisterScriptFunction("PluginObject::DoSomething^1",  
                       PluginObject_DoSomething);
```

In other words, the function takes the object as its first parameter. The exported name is `"structname::functionname^numparams"`, where `numparams` is the number of parameters it takes (excluding the object itself).

_Added in version: 1_

#### IAGSEngine.GetWindowHandle
```
HWND GetWindowHandle ();
```

Returns the window handle of the main game window.

_Added in version: 1_

#### IAGSEngine.GetGraphicsDriverID
```
const char* GetGraphicsDriverID();
```

Returns an ID string representing the current graphics driver. This can either be "D3D9" if the player is using the Direct3D driver, or "DX5" if they are using the standard DirectDraw driver.

If the engine interface version is less than 19, this function is not available; however, in that case you can safely assume that the DX5 driver is in use since earlier versions of AGS only supported that driver.

_![Warning](images/icon_warn.png)_ Your `AGS_EngineStartup` event is called before the graphics system is initialized. Therefore, you cannot call `GetGraphicsDriverID` from within `AGS_EngineStartup` as no driver is loaded at that point.

_![Info icon](images/icon_info.png)_ When the Direct3D driver is in use, the screen is redrawn each frame using 3D accelerated blits, and therefore there is no virtual screen. You can only manipulate the virtual screen when running with the DX5 driver.

_Added in version: 19_

#### IAGSEngine.GetDirectDraw2
```
LPDIRECTDRAW2 GetDirectDraw2 ();
```

Returns the main IDirectDraw2 interface that the game is using.

This function is only supported if the player is using the DX5 graphics driver.

_Added in version: 1_

#### IAGSEngine.GetBitmapSurface
```
LPDIRECTDRAWSURFACE2 GetBitmapSurface (BITMAP *bmp);
```

Returns the IDirectDrawSurface2 interface associated with the specified bitmap.

This function is only supported if the player is using the DX5 graphics driver.

_![Warning](images/icon_warn.png)_ This is the Allegro BITMAP structure, not the Win32 GDI BITMAP. Do not try and use a win32 BITMAP with this function, as it will crash the system.

_Added in version: 1_

#### IAGSEngine.GetScreen
```
BITMAP * GetScreen ();
```

Returns a reference to the main screen bitmap (as an _Allegro_ `BITMAP`). You can use this via DDraw with the `GetBitmapSurface` method, or use the various AGS drawing functions which are documented later.

This function is only supported if the player is using the DX5 graphics driver.

_Added in version: 1_

#### IAGSEngine.RequestEventHook
```
void RequestEventHook (int event);
```

Requests that the engine calls the plugin's `AGS_EngineOnEvent` function when the specified event occurs in future. Possible values are:

##### IAGSEngine event AGSE_KEYPRESS

triggered when the user presses a key on the keyboard

**data value:** ASCII value of keystroke, as text script on_key_press (but lower case a-z are passed as 97..122)

##### IAGSEngine event AGSE_MOUSECLICK

triggered when the user clicks a mouse button

**data value:** mouse button pressed (1=left, 2=right, 3=middle)

##### IAGSEngine event AGSE_POSTSCREENDRAW

triggered after the virtual screen has been drawn each frame, but before the mouse cursor is painted and it gets copied to the screen 

**data value:** _\*\* See Note 1 below_

##### IAGSEngine event AGSE_PRESCREENDRAW

_(version 4 and later only)_

triggered every frame after the room background has been drawn, but before anything else

**data value:** _\*\* See Note 1 below_

##### IAGSEngine event AGSE_SAVEGAME  

_(version 5 and later only)_

triggered when the game position is saved. You can then use the interface `FWrite` function to write your own data. The script engine is in an invalid state at this point, so do not call any script functions.

**data value:** file handle of save game

##### IAGSEngine event AGSE_RESTOREGAME

_(version 5 and later only)_

triggered when the game position is loaded. You then use the `FRead` function to read the data back. You **must** read back the same number of bytes as you wrote. The script engine is in an invalid state at this point, so do not call any script functions.

**data value:** file handle of save game

##### IAGSEngine event AGSE_PREGUIDRAW

_(version 6 and later only)_

triggered once the screen has been constructed, but before the GUIs have been drawn on.

**data value:** _\*\* See Note 1 below_

##### IAGSEngine event AGSE_LEAVEROOM

_(version 6 and later only)_

triggered when the player leaves the current room, after the Player Leaves Screen event but before the screen fades out.

**data value:** old room number

##### IAGSEngine event AGSE_ENTERROOM

_(version 6 and later only)_

triggered when the player enters a new room, before the screen fades in

**data value:** new room number

##### IAGSEngine event AGSE_TRANSITIONOUT

_(version 6 and later only)_

triggered when the screen is about to fade out as the player changes rooms. If you return 1, AGS will not perform its screen transition.

**data value:** _(unused, currently 0)_

##### IAGSEngine event AGSE_TRANSITIONIN

_(version 6 and later only)_

triggered when the screen is about to fade in as the player changes rooms. If you return 1, AGS will not perform its screen transition.

**data value:** _(unused, currently 0)_

##### IAGSEngine event AGSE_FINALSCREENDRAW

_(version 12 and later only)_

triggered each frame after the mouse cursor is painted and immediately before the virtual screen is copied to the screen.

**data value:** _\*\* See Note 1 below_

##### IAGSEngine event AGSE_TRANSLATETEXT

(version 12 and later only)

triggered whenever there is some in-game text that might need translating. If you return 0, AGS will translate it as usual; otherwise, you can return a `char *` pointer with the replacement text (the return pointer must point to some static memory since AGS does not take a copy)

**data value:** the text to translate (cast this parameter to `const char *`)

##### IAGSEngine event AGSE_SCRIPTDEBUG

_(version 13 and later only)_

triggers the AGS\_ EngineDebugHook function every time the game script advances to a new line.

**data value:** _N/A_

##### IAGSEngine event AGSE_SPRITELOAD

_(version 18 and later only)_

triggered whenever a sprite is loaded into memory. This allows you to modify sprites as soon as they are loaded into the sprite cache. Do **not** attempt to access any other sprites from this event, since the sprite cache may be in an inconsistent state.

**data value:** sprite number

##### IAGSEngine event AGSE_PRERENDER

_(version 21 and later only)_

triggered every frame after the game logic has run but before anything is rendered to the pre-screen sprite cache

**data value:** _(unused, currently 0)_

##### IAGSEngine event AGSE_PRESAVEGAME

_(version 24 and later only)_

triggered just before a save game is created. The script engine is still working at this point, so you can perform any tasks that you need to prior to the game data being saved

**data value:** _(unused, currently 0)_

##### IAGSEngine event AGSE_POSTRESTOREGAME

_(version 24 and later only)_

triggered after a save game has been restored. By the time this event occurs, all the game data has been restored and the script engine is operational again.

**data value:** _(unused, currently 0)_

_![Info icon](images/icon_info.png)_ Each frame (or _game loop_), AGS redraws the screen from scratch. The sequence is as follows:

**DX5 driver**

1.  Call `AGSE_PRERENDER`
2.  Update in-memory cache of current character and object images
3.  Draw current background scene
4.  Call `AGSE_PRESCREENDRAW`
5.  Draw cached objects and characters
6.  Call `AGSE_PREGUIDRAW`
7.  Draw screen overlays
8.  Draw GUIs
9.  Call `AGSE_POSTSCREENDRAW`
10. Draw mouse cursor and finalize.
11. Call `AGSE_FINALSCREENDRAW`
12. Paste the virtual screen to the real screen. 

**D3D9 driver**

1.  Call `AGSE_PRERENDER`
2.  Update in-memory cache of current character and object images
3.  `Direct3DDevice9->BeginScene`
4.  Draw current background scene
5.  Call `AGSE_PRESCREENDRAW`
6.  Draw cached objects and characters
7.  Call `AGSE_PREGUIDRAW`
8.  Draw screen overlays
9.  Draw GUIs
10. Call `AGSE_POSTSCREENDRAW`
11. Draw mouse cursor and finalize.
12. Call `AGSE_FINALSCREENDRAW`
13. `Direct3DDevice9->EndScene`

**\*\* Note 1**: The `data` parameter to these events is 0 when using the DX5 driver; when using the D3D9 driver it is a pointer to the IDirect3DDevice9 that is currently being used for rendering. You can render extra primitives by calling all the normal methods on this interface.  
(Interface version 20 and above only).

_Added in version: 2_

#### IAGSEngine.GetSavedData
```
int GetSavedData (char *buffer, int bufsize);
```

Gets the plugin data that was originally saved with AGS_EditorSaveGame. If your plugin had options that the user could set in the editor, this is how to retrieve them.

`buffer` is a byte array of `bufsize`, which the engine will copy the saved data into. It returns the number of bytes actually used.

_Added in version: 2_

#### IAGSEngine.GetVirtualScreen
```
BITMAP * GetVirtualScreen ();
```

Returns a reference to the virtual screen bitmap (as an _Allegro_ BITMAP). The virtual screen is what all drawing routines will draw onto, and usually points to a screen-sized memory bitmap that the engine paints on to construct each frame. Once it is finished, the whole thing is copied to the real screen. This is done to prevent the screen flickering as various things are painted on. 

This function is only supported if the player is using the DX5 graphics driver.

_Added in version: 3_


#### IAGSEngine.GetRawBitmapSurface
```
unsigned char ** GetRawBitmapSurface (BITMAP *bmp);
```

Gets a reference to the linear bank of memory that contains the surface of `bmp`. This allows you to directly plot pixels and so forth, simply by writing to the surface as an array.

This function locks the surface for you, which means you **must** call ReleaseBitmapSurface to release it when you are done. Failure to do so will most likely hang the engine.

_![Warning](images/icon_warn.png)_ If the bitmap color depth is 15/16 bit, the return value should be cast to `unsigned short**`.   
If the bitmap color depth is 32 bit, the return value should be cast to `unsigned long**`.   
If the bitmap color depth is 24 bit, the return value needs to be accessed in blocks of 3 bytes. The best method of doing this is left up to you.

_![Warning](images/icon_warn.png)_ If you change any areas of the virtual screen bitmap via this raw surface, you should call `MarkRegionDirty` with the affected area, so that AGS redraws that part of the screen.

_![Warning](images/icon_warn.png)_ **Be careful** when using this surface, since writing outside it will crash the engine. Make sure you use `GetBitmapDimensions` to find out how big the bitmap is.

_![Warning](images/icon_warn.png)_ This function cannot be used with the real screen bitmap - it can only be used with the virtual screen and any other bitmaps you may have access to.

_Added in version: 3_

#### IAGSEngine.ReleaseBitmapSurface
```
void ReleaseBitmapSurface (BITMAP *bmp);
```

Releases a bitmap previously locked with `GetRawBitmapSurface`.

_Added in version: 3_

#### IAGSEngine.GetScreenDimensions
```
void GetScreenDimensions (int *width, int *height, int *coldepth);
```

Fills in the supplied variables with the current display mode that the engine is running at. You can pass any of the parameters as NULL if you don't want to know them.

`coldepth` is either 8, 15, 16, 24 or 32 and reflects the actual color depth that the game is running at.

_Added in version: 3_

#### IAGSEngine.DrawText
```
void DrawText (int x, int y, int font, int color, char *text);
```

Writes the string `text` to the current virtual screen at (`x`, `y`), using game font number `font` in color `color`.

_![Info icon](images/icon_info.png)_ The `x` and `y` parameters are in actual screen co-ordinates, unlike the text script commands which always use 320-scale co-ordinates. You will need to use `GetScreenDimensions` and multiply up the co-ordinates accordingly if you wish to draw to a specific location.

_Added in version: 3_

#### IAGSEngine.GetMousePosition
```
void GetMousePosition (int *x, int *y);
```

Fills the supplied variables with the current mouse cursor co-ordinates. Note that these are real screen size co-ordinates, and so at 640x480 resolution these variables can go up to 640 and 480, unlike the text script system.

_Added in version: 3_

#### IAGSEngine.GetBitmapDimensions
```
void GetBitmapDimensions (BITMAP *bmp, int *width, int *height, int *coldepth);
```

Fills in the supplied integer variables with the properties of the specified bitmap. You can pass any of the last three parameters as NULL if you don't want to know them.

`width` is the width of the bitmap, in pixels. `height` is the height of the bitmap, in pixels. `coldepth` is the color depth of the bitmap. Note that this is not necessarily the same as the game color depth, since it is possible to use 256-color backgrounds in a hi-color game. Before doing any direct bitmap drawing, you should check this to make sure that you cast the pointer correctly.

_Added in version: 4_

#### IAGSEngine.GetNumBackgrounds
```
int GetNumBackgrounds ();
```

Returns the number of background frames that the current room has (a normal room will return 1).

_Added in version: 4_

#### IAGSEngine.GetCurrentBackground
```
int GetCurrentBackground ();
```

Returns the number of the currently displayed background frame. (0 is the default frame, 1 the first animated background, and so forth).

_Added in version: 4_

#### IAGSEngine.GetBackgroundScene
```
BITMAP * GetBackgroundScene (int frame);
```

Returns a reference to the specified background frame (0 is the default frame, 1 the first animated background, and so on).

_Added in version: 4_

#### IAGSEngine.GetCurrentRoom
```
int GetCurrentRoom ();
```

Returns the room number that the game is currently in. 

_Added in version: 4_

#### IAGSEngine.FRead
```
int FRead (void *buffer, int length, int handle);
```

Similar to the C function `fread`, this reads `length` bytes of `buffer` from file `handle`, returning the number of bytes actually read. The handle you use here **must** have been passed to you by AGS. For any other I/O, you can simply use the standard C functions.

_Added in version: 5_

#### IAGSEngine.FWrite
```
int FWrite (void *buffer, int length, int handle);
```

Similar to the C function `fwrite`, this writes `length` bytes of `buffer` to file `handle`, returning the number of bytes actually written. The handle you use here **must** have been passed to you by AGS. For any other I/O, you can simply use the standard C functions.

_Added in version: 5_

#### IAGSEngine.SetVirtualScreen
```
void SetVirtualScreen (BITMAP *bmp);
```

Sets `bmp` as the current virtual screen, so that all drawing routines will draw onto it.  You should restore the virtual screen to its original setting before returning from your plugin function. (Use GetVirtualScreen first to save the old reference).

_Added in version: 5_

#### IAGSEngine.DrawTextWrapped
```
void DrawTextWrapped (int x, int y, int width, int font, int color, const char *text);
```

Prints `text` to the current virtual screen at (`x`, `y`), using `width` pixels wide to do so, wrapping the text to ensure it does not exceed the width.  

_Added in version: 5_

#### IAGSEngine.BlitBitmap
```
void BlitBitmap (int x, int y, BITMAP *bmp, int masked);
```

Draws graphic `bmp` to the current virtual screen at (`x`,`y`).  
If `masked` is 0, the image is copied straight across.  
If `masked` is 1, then transparent pixels are skipped.

_Added in version: 5_

#### IAGSEngine.LookupParserWord
```
int LookupParserWord (const char *word);
```

Checks the text parser dictionary for `word`, and returns its word number. All synonyms of a word have the same word number, as shown in the Text Parser pane in the AGS Editor.  
Returns -1 if the word was not in the dictionary.   

_Added in version: 5_

#### IAGSEngine.PollSystem
```
void PollSystem ();
```

Updates the internally stored mouse co-ordinates, and checks for mouse clicks and keypresses (and triggers the relevant plugin events). Also runs the music decoder to make sure that there is enough data to play.

Call this function if you have a long plugin function which takes more than half a second to execute, or if you need to get mouse and keypress events while still inside your function.

_![Info icon](images/icon_info.png)_ AGS is single-threaded; this means that any background music has to be played by updating the buffer at regular intervals. Therefore, if your function takes a while to execute you should call this to make sure the music doesn't skip.

_Added in version: 5_

#### IAGSEngine.GetNumCharacters
```
int GetNumCharacters ();
```

Returns the number of characters in the current game. Valid character ID's range from 0 to the return value minus 1. 

_Added in version: 6_

#### IAGSEngine.GetCharacter
```
AGSCharacter * GetCharacter (int charid);
```

Returns the character state struct for character `charid`. This struct is documented in the header file, but is mostly identical to the `character[]` text script variable.

_![Warning](images/icon_warn.png)_ Beware when modifying character state structs. There are some caveats to watch out for, such as altering the X and Y values while the character is moving.  
Also, remember that all view numbers stored are **1 less** than the numbers shown in the editor and used in the text script.

_Added in version: 6_

#### IAGSEngine.GetGameOptions
```
AGSGameOptions * GetGameOptions ();
```

Returns a reference to the game state structure. This is similar to the text script `game.` variables.

_![Info icon](images/icon_info.png)_ One handy member here is the `AGSGameOptions.fast_forward` variable. This is set to 1 while a cut-scene is being skipped, so if you have any lengthy graphical effects you should not perform them if this is set. All operations which update any game state **must** still be performed however, or skipping the cut-scene will desync the game.

_Added in version: 6_

#### IAGSEngine.GetPalette
```
AGSColor * GetPalette ();
```

Returns a reference to the current palette. This is an array of 256 elements of the `AGSColor` struct.

_![Info icon](images/icon_info.png)_ In a game with animating backgrounds, the palette can change quite often, so you should generally only rely on the palette remaining consistent for the length of your function.  

_Added in version: 6_

#### IAGSEngine.SetPalette
```
void SetPalette (int start, int finish, AGSColor *palette);
```

Sets the current screen palette to `palette`, which must be an array of 256 `AGSColor` structs. The elements from `start` to `finish` are updated. Pass start as 0 and finish as 255 to update the entire palette.

_Added in version: 6_

#### IAGSEngine.GetPlayerCharacter
```
int GetPlayerCharacter ();
```

Returns the number of the current player character.

_Added in version: 7_

#### IAGSEngine.GetNumObjects
```
int GetNumObjects ();
```

Returns the number of objects in the current room.

_Added in version: 7_

#### IAGSEngine.GetObject
```
AGSObject * GetObject (int number);
```

Returns the state structure for object `number`.

_![Warning](images/icon_warn.png)_ Unlike the character structs, object state pointers are not constant throughout the game. Any time the room changes, these structs get reallocated. Therefore, do not keep a pointer that you get with this command after your function ends.

_Added in version: 7_

#### IAGSEngine.RoomToViewport
```
void RoomToViewport (int *x, int *y);
```

Converts the room co-ordinates (`x`, `y`) into current viewport co-ordinates. The input co-ordinates are room co-ordinates using the 320x200-style scheme that the text script uses and that object and character co-ordinates are stored as.

When you call this function, the variables you pass will be converted to hold the equivalent viewport co-ordinates. These are real resolution-sized co-ordinates within the current viewable area of the screen.  

_![Info icon](images/icon_info.png)_ You should check the resulting co-ordinates with the screen size to determine whether they are currently visible on the screen. 

_Added in version: 7_

#### IAGSEngine.ViewportToRoom
```
void ViewportToRoom (int *x, int *y);
```

Converts the viewport co-ordinates (`x`, `y`) into room co-ordinates. The input co-ordinates are screen resolution scale co-ordinates within the current viewable area of the room.

When you call this function, the variables you pass will be converted to hold the equivalent room co-ordinates, such as stored in the character and object structs, and used in the text script. 

_Added in version: 7_

#### IAGSEngine.GetSpriteGraphic
```
BITMAP * GetSpriteGraphic (int slot);
```

Returns the bitmap with the graphic for sprite slot number `slot`.

_![Info icon](images/icon_info.png)_ This method will automatically load the sprite from disk into the sprite cache if it is not already present.

_![Warning](images/icon_warn.png)_ The AGS Sprite Cache may destroy any sprite from memory at any time. Therefore, **never** keep a pointer obtained with this command. Always call this method again if you need to perform multiple operations with the bitmap.

_Added in version: 7_

#### IAGSEngine.CreateBlankBitmap
```
BITMAP * CreateBlankBitmap (int width, int height, int coldepth);
```

Creates a blank bitmap sized `width` x `height` pixels at `coldepth`-bit color. The bitmap will initially be filled with the transparent color for the color depth.

Returns NULL if the bitmap could not be created. You should always check the return value to avoid crashes.

_![Info icon](images/icon_info.png)_ To draw onto the bitmap either use `GetRawBitmapSurface`, or the `SetVirtualScreen` command followed by one of the drawing commands such as `DrawText` or `BlitBitmap`.

_![Warning](images/icon_warn.png)_ The bitmap will remain in memory until you explicitly free it with `FreeBitmap`. Use this command sparingly, as each bitmap you create eats into the engine's available memory.

 _Added in version: 7_

#### IAGSEngine.FreeBitmap
```
void FreeBitmap (BITMAP *bmp);
```

Frees the bitmap `bmp` from memory. 

_![Warning](images/icon_warn.png)_ **Only** use this command with bitmaps you created with `CreateBlankBitmap`. Using it with an AGS system bitmap, such as one obtained with `GetVirtualScreen`, `GetScreen` or `GetSpriteGraphic` will crash the engine.

 _Added in version: 7_

#### IAGSEngine.GetRoomMask
```
BITMAP * GetRoomMask (int which);
```

Returns a reference to the requested mask for the current room. `which` is one of the following values:  
`MASK_WALKABLE`  
`MASK_WALKBEHIND`  
`MASK_HOTSPOT`  
`MASK_REGIONS`

The walk-behind mask is exactly the same size as the room, and is at the current resolution. For example, a 320x200 room, being run at 640x400 in the engine, will give you a 640x400 bitmap.

The walkable area, hotspot and region masks are the size of the current room, but at the 320x200 resolution.

**All** of the masks are bitmaps with 8-bit color depth, irrespective of what color depth the game is running at.

_![Warning](images/icon_warn.png)_ The area masks are re-allocated when the player changes rooms, so do **not** keep a pointer returned by this function longer than you need it.

_Added in version: 8   (MASK_REGIONS requires version 11)._

#### IAGSEngine.GetViewFrame
```
AGSViewFrame* GetViewFrame (int view, int loop, int frame);
```

Returns the view frame structure for the specified frame. `view` is the number you get from the editor (that's used in `SetCharacterView` and so forth), not the view minus 1.

-   **Interface version 10 and later:**  
    If `frame` is not valid (eg. there aren't that many frames in the specified loop), returns NULL.
-   **Interface version 9:**  
    If `frame` is not valid (eg. there aren't that many frames in the specified loop), AGS will exit with an error message.

If `view` or `loop` are invalid, AGS will exit with an error message.

_Added in version: 9_

#### IAGSEngine.GetWalkbehindBaseline
```
int GetWalkbehindBaseline (int area);
```

Returns the baseline for walk-behind area number `area`. This is always in character-resolution, ie. the maximum value is 200 in all resolutions.

_Added in version: 9_

#### IAGSEngine.GetScriptFunctionAddress
```
void* GetScriptFunctionAddress (const char *funcName);
```

Returns the memory address of the text script exported function `funcName`. This allows you to call any of the functions which AGS makes available to the text scripts.

Returns NULL if you specify a function that doesn't exist.

_![Warning](images/icon_warn.png)_ You **must** cast the result to the correct function type in order to call it - ie. you must know how many parameters the function expects, and call it appropriately. Failure to do so will corrupt the stack and likely crash the engine.

_![Warning](images/icon_warn.png)_ If you specify the name of an actual function in the script, for example  repeatedly_execute, it will return an address - however, this will be a script address and attempting to call it will crash the game. **Only** use this feature to obtain the address of AGS's script functions as documented in the manual.

_Added in version: 9_

#### IAGSEngine.GetBitmapTransparentColor
```
int GetBitmapTransparentColor (BITMAP *bmp);
```

Returns the pixel color which is skipped when rendering the bitmap. This is 0 in 256-color bitmaps and RGB (255,0,255) in hi-color bitmaps, so this function returns the pixel value to check for if you need to know.

_Added in version: 9_

#### IAGSEngine.GetAreaScaling
```
int GetAreaScaling (int x, int y);
```

Returns the walkable area scaling level at the specified co-ordinates. This ranges from 5 to 200, and specifies the scaling percentage, as set in the editor. The co-ordinates are specified as room co-ordinates.

_Added in version: 9_

#### IAGSEngine.IsGamePaused
```
int IsGamePaused ();
```

Equivalent to the text script `IsGamePaused` function. This returns non-zero if the game is paused, or 0 if it is not paused. 

_Added in version: 9_

#### IAGSEngine.GetRawPixelColor
```
int GetRawPixelColor (int color);
```

Converts `color`, as specified in the AGS Editor, to the appropriate raw pixel color for the current graphics mode.

If the user is running 8-bit color, the value is returned unchanged.

If the user is running 16-bit color, the value is returned unchanged _unless_ it is less than 32, in which case it is converted to be the appropriate locked color from the editor.

If the user is running 15-bit color, the value is converted to an appropriate 15-bit RGB pixel value.

_Added in version: 10_

#### IAGSEngine.GetSpriteWidth
```
int GetSpriteWidth (int slot);
```

Returns the width, in pixels, of sprite number `slot`.

This is faster than using `GetBitmapDimensions` with `GetSpriteGraphic`, since the image does not need to be retrieved from the sprite cache.

_Added in version: 11_

#### IAGSEngine.GetSpriteHeight
```
int GetSpriteHeight (int slot);
```

Returns the height, in pixels, of sprite number `slot`.

This is faster than using `GetBitmapDimensions` with `GetSpriteGraphic`, since the image does not need to be retrieved from the sprite cache.

_Added in version: 11_

#### IAGSEngine.GetTextExtent
```
void GetTextExtent (int font, const char *text, int *width, int *height);
```

Calculates the width and height, in pixels, of displaying `text` in game font number `font`.

`width` or `height` can be NULL if you only want to know the other one.

_Added in version: 11_

#### IAGSEngine.PrintDebugConsole
```
void PrintDebugConsole (const char *message);
```

Prints `message` to the in-game debug console (which the user can pop up with the ~ key).

The debug console is designed to help the user find problems by tracing through what's happening in the game - so do not pump messages out to this debug console too quickly or they will scroll past too fast for the user to read. Use the console to say one-off events like "Requested move character to X,Y" and so forth.

_Added in version: 11_

#### IAGSEngine.IsChannelPlaying
```
int IsChannelPlaying (int channel);
```

Equivalent to the text script function of the same name, returns 1 if the channel is currently in use, 0 if not.

_Added in version: 11_

#### IAGSEngine.PlaySoundChannel
```
void PlaySoundChannel (int channel, int soundType, int volume, int loop, const char *filename);
```

Plays a new sound on the sound channel number `channel`. `volume` can be from 0 to 255, `loop` is 0 or 1.

`soundType` determines which sound driver is used to load the file:

|    _soundType_   |                                        |
| ---------------- | -------------------------------------- |
| `PSND_WAVE`      | Uncompressed .WAV file                 |
| `PSND_MP3STREAM` | MP3, streamed from disk                |
| `PSND_MP3STATIC` | MP3, loaded into memory before playing |
| `PSND_OGGSTREAM` | OGG, streamed from disk                |
| `PSND_OGGSTATIC` | OGG, loaded into memory before playing |
| `PSND_MIDI`      | MIDI file                              |
| `PSND_MOD`       | MOD/XM/S3M file                        |

_![Info icon](images/icon_info.png)_ You should normally just use the PlaySound, PlaySoundEx and PlayMusic functions (via GetScriptFunctionAddress) to play sounds - only use this function in specific circumstances.

_![Warning](images/icon_warn.png)_ Only one MIDI file, and one MOD/XM file can be playing at a time. You should generally keep away from these two sound types unless you are sure about what you are doing. 

_Added in version: 11_

#### IAGSEngine.MarkRegionDirty
```
void MarkRegionDirty(int left, int top, int right, int bottom);
```

Marks the rectangle (`left`, `top`) - (`right`, `bottom`) on the virtual screen as dirty. Use this if you make any changes to the virtual screen via its raw bitmap surface, to tell AGS to repaint that area of the screen.

_![Info icon](images/icon_info.png)_ All engine API functions such as `DrawText` and `BlitBitmap` call this automatically, so you only need to call it if you manually modify the bitmap surface.

_Added in version: 12_

#### IAGSEngine.GetMouseCursor
```
AGSMouseCursor* GetMouseCursor(int cursor);
```

Returns the mouse cursor struct which AGS uses to store details about the specified cursor mode.

_![Warning](images/icon_warn.png)_ The returned struct is read-only. You should not modify any members of it directly; rather, call the script functions such as `ChangeCursorGraphic` which ensure that the game state is updated properly.

_Added in version: 12_

#### IAGSEngine.GetRawColorComponents
```
void GetRawColorComponents(int coldepth, int color,int *red, int *green, int *blue, int *alpha);
```

Given a raw color (from a bitmap's raw surface, or from GetRawPixelColor) at a given color depth, returns the red, green, blue and alpha components, as values from 0-255.

You can pass any of the pointers as NULL if you don't want to know that value. The `alpha` value only has meaning for 32-bit pixels; for all other color depths, it will just be returned as 0.

_Added in version: 12_

#### IAGSEngine.MakeRawColorPixel
```
int MakeRawColorPixel(int coldepth, int red, int green, int blue, int alpha);
```

Given a color depth, and RGB values (from 0-255), this function returns the raw pixel value needed to display the requested color on a bitmap of `coldepth` bits per pixel.

The `alpha` value is only meaningful for 32-bit color alpha channel bitmaps, and it allows you to set the alpha value for the pixel. For bitmaps without an alpha channel, pass `alpha` as 0.

_Added in version: 12_

#### IAGSEngine.GetFontType
```
int GetFontType(int fontNum);
```

Returns what type of font `fontNum` is, as one of the following values:

| value         | description                  |
| ------------- | ---------------------------- |
| `FNT_INVALID` | invalid font number supplied |
| `FNT_SCI`     | font is a SCI font           |
| `FNT_TTF`     | font is a TTF font           |

 _Added in version: 12_

#### IAGSEngine.CreateDynamicSprite
```
int CreateDynamicSprite(int coldepth, int width, int height);
```

Creates a new dynamic sprite with the supplied color depth, width and height. A dynamic sprite is not controlled by the AGS Sprite Cache, and so is not removed from memory until you manually call `DeleteDynamicSprite`. Thus, you can write to its bitmap surface without a problem.

You must remember to free the memory when you are done with the sprite, by calling `DeleteDynamicSprite`.

Returns 0 if the sprite could not be created, or the sprite slot number on success.

_Added in version: 12_

### IAGSEngine.DeleteDynamicSprite
```
void DeleteDynamicSprite(int slot);
```

Removes the previously created dynamic sprite from memory. It can no longer be used in the game.

_Added in version: 12_

#### IAGSEngine.IsSpriteAlphaBlended
```
int IsSpriteAlphaBlended(int slot);
```

Determines whether the supplied sprite has an alpha channel or not. Returns 1 if it does, 0 if it does not.

This function is useful for determining whether you can ignore the alpha value when doing raw bitmap manipulations. If a sprite does have an alpha channel, you cannot ignore it since the default alpha value of 0 means totally invisible and the pixel would disappear.

Only 32-bit bitmaps can have an alpha channel. For all other color depths, this function will always return 0.

_Added in version: 12_

#### IAGSEngine.UnrequestEventHook
```
void UnrequestEventHook(int event)
```

Tells the engine not to call this plugin any longer when the specified `event` occurs. The values of `event` are the same as for `RequestEventHook`.

This is useful to call for performance reasons if you no longer require notification of an event.

_Added in version: 13_

#### IAGSEngine.BlitSpriteTranslucent
```
void BlitSpriteTranslucent(int x, int y, BITMAP *spr, int trans);
```

Draws graphic `spr` to the current virtual screen at (`x`,`y`), with translucency over the background.

`trans` is the translucency level, from 0 to 255 (where 0 is fully transparent, and 255 is fully opaque). Pixels in the bitmap's transparent color are skipped completely.

_Added in version: 13_

#### IAGSEngine.BlitSpriteRotated
```
void BlitSpriteRotated(int x, int y, BITMAP *spr, int angle);
```

Draws graphic `spr` to the current virtual screen at (`x`,`y`), but rotated to `angle`. Pixels in the bitmap's transparent color are skipped completely.

The sprite is positioned with its upper-left corner at (`x`,`y`), then it is rotated about its center by `angle`. The angle is specified as a number from 0 to 255, where 128 would turn it 180 degrees, and 64 would turn it 90 degrees.

_Added in version: 13_

#### IAGSEngine.GetDirectSound
```
LPDIRECTSOUND GetDirectSound();
```

Returns the main `IDirectSound` interface that the engine is using. This command does **not** `AddRef` the pointer it returns, so you don't need to Release it.

This function returns `NULL` if sound is disabled, or if the player is using the WaveOut driver rather than the DirectSound one.

_Added in version: 14_

#### IAGSEngine.DisableSound
```
void DisableSound();
```

Disables AGS's sound system completely. Use this if you want your plugin to take over all audio functionality.

_Added in version: 14_

#### IAGSEngine.CanRunScriptFunctionNow
```
int CanRunScriptFunctionNow();
```

Determines whether a game script function can be run now. Returns 0 if there is currently a script running, or 1 if there isn't.

_Added in version: 14_

#### IAGSEngine.CallGameScriptFunction
```
int CallGameScriptFunction(const char *name, int globalScript, int numArgs, int arg1 = 0, int arg2 = 0, int arg3 = 0);
```

Runs a script function in the game's script. `name` is the name of the function to call. If `globalScript` is 1, it will call the function in the global script; if it is 0, the function will be run in the room script.

`numArgs` specifies how many arguments the function takes - this can be from 0 to 3. The following parameters then allow you to pass the contents of the function parameters. They are all 32-bit ints, so the user should declare their script function as taking `int` parameters.

This function returns 0 on success, and a non-zero value otherwise. This will always fail when `CanRunScriptFunctionNow` returns 0.

_Added in version: 14_

#### IAGSEngine.QueueGameScriptFunction
```
void QueueGameScriptFunction(const char *name, int globalScript, int numArgs, int arg1 = 0, int arg2 = 0);
```

Queues a script function to be run in the game's script. `name` is the name of the function to call. If `globalScript` is 1, it will call the function in the global script; if it is 0, the function will be run in the room script.

`numArgs` specifies how many arguments the function takes - this can be from 0 to 2. The following parameters then allow you to pass the contents of the function parameters. They are all 32-bit ints, so the user should declare their script function as taking `int` parameters.

If no scripts are currently running, the requested script will be run straight away. If there are scripts running, however, then the requested script will be queued up to run when the current one finishes.

_Added in version: 15_

#### IAGSEngine.NotifySpriteUpdated
```
void NotifySpriteUpdated(int slot);
```

Notifies the engine that the specified sprite has been updated by the plugin. You would call this if you changed the contents of a dynamic sprite, to make sure that the screen is updated to reflect your changes.

_Added in version: 15_

#### IAGSEngine.SetSpriteAlphaBlended
```
void SetSpriteAlphaBlended(int slot, int isAlphaBlended);
```

Allows you to specify whether the sprite is alpha blended or not. This allows you to create dynamic 32-bit RGBA sprites. Pass `isAlphaBlended` as 1 to enable the sprite's alpha channel, or pass it as 0 to disable the alpha channel.

_![Warning](images/icon_warn.png)_ This function should only be used with 32-bit dynamic sprites. Using it with sprites of lower color depths, or of sprites created in the AGS Editor, can have unpredictable results.

_Added in version: 15_

#### IAGSEngine.RegisterManagedObject
```
int RegisterManagedObject(const void *object, IAGSScriptManagedObject *callback);
```

Registers a new managed object with the script engine. `object` points to the actual object itself, and `callback` points to the class implementing the `IAGSScriptManagedObject` interface, which will be called to perform operations on the object.

`callback` and `object` can, but do not have to, point to the same thing (ie. it is possible to have the actual object implement the interface; but if you do so, beware that you should not expose any normal variables from the class due to the vtable occupying the first part of the memory).

The `object` is added to the managed object pool, with a reference count of zero. Once this function has been called, `object` can be returned to the script and will be automatically picked up by the script engine.

See further down this page for a description of the `IAGSScriptManagedObject` interface.

From engine interface version 16 and later, this function returns the managed pool key for the object. You will not normally need this, but it can be useful to link a parent and child object if your structure is complex.

_Added in version: 15_

#### IAGSEngine.AddManagedObjectReader
```
void AddManagedObjectReader(const char *typeName, IAGSManagedObjectReader *reader);
```

Registers the specified managed object type with the script engine, and supplies an `IAGSManagedObjectReader`, which provides the functionality for de-serializing objects of that type. This is used when the user restores a save game, in order to recreate any managed objects that were in existence when the game was saved.

See further down this page for a description of the `IAGSManagedObjectReader` interface.

_![Warning](images/icon_warn.png)_ AGS only keeps a pointer to `typeName` and does not copy the string, so make sure you do not supply a temporary or local variable as the type name.

_Added in version: 15_

#### IAGSEngine.RegisterUnserializedObject
```
void RegisterUnserializedObject(int key, const void *object, IAGSScriptManagedObject *callback);
```

Used from within the `IAGSManagedObjectReader`, this function re-registers a managed object after it has been read back from disk (for example, when the player restores a save game).

The `key` parameter is the object's key, supplied to the `ObjectReader`, which allows AGS to match up the object internally. You should pass the key in here exactly as it is passed to the `ObjectReader`.

_Added in version: 15_

#### IAGSEngine.GetManagedObjectKeyByAddress
```
int GetManagedObjectKeyByAddress(const char *address);
```

Gets the managed pool key of the specified object address. You will not normally need to use this function, however it can be useful to link up related objects after de-serialization.

Returns -1 if there is no such object in the pool.

This function is quite slow so you should avoid using it wherever possible.

_Added in version: 16_

#### IAGSEngine.GetManagedObjectAddressByKey
```
void* GetManagedObjectAddressByKey(int key);
```

Gets the memory address of the specified object from the managed pool. You will not normally need to use this function, however it can be useful to link up related objects after de-serialization.

Returns `NULL` if the key is invalid.

_Added in version: 16_

#### IAGSEngine.CreateScriptString
```
const char * CreateScriptString(const char *fromText);
```

Creates a new script String object, containing a copy of `fromText`. This allows you to declare your plugin functions as returning a String - simply return the result of **CreateScriptString** to the calling script.

The new string becomes part of the AGS Managed Object Pool and will be freed automatically when there are no longer any script references to it. Note that it creates a copy of `fromText`, so it is safe for you to free the contents of `fromText` after calling this function.

_Added in version: 17_

#### IAGSEngine.IncrementManagedObjectRefCount
```
int IncrementManagedObjectRefCount(const char *address);
```

Increments the reference count of the specified object in the managed object pool. This should be used if you are storing a reference to a managed object between script function calls, in order to ensure that the object does not get deleted.

Returns the new reference count of the object.

_![Warning](images/icon_warn.png)_ Be **very careful** when using this function. If you adjust the reference count incorrectly, you could cause a memory leak or the game could crash.

_Added in version: 18_

#### IAGSEngine.DecrementManagedObjectRefCount
```
int DecrementManagedObjectRefCount(const char *address);
```

Decrements the reference count of the specified object in the managed object pool. This should be used if you are storing a reference to a managed object between script function calls, in order to ensure that the object does not get deleted.

Returns the new reference count of the object.

_![Warning](images/icon_warn.png)_ Be **very careful** when using this function. If you adjust the reference count incorrectly, you could cause a memory leak or the game could crash.

_Added in version: 18_

#### IAGSEngine.SetMousePosition
```
void SetMousePosition(int x, int y);
```

Changes the mouse cursor position to (x,y). As with _GetMousePosition_, these co-ordinates are specified in real resolution units, so in a 640x480 game the co-ordinates do go up to 640,480 (unlike the script function of the same name).

_Added in version: 18_

#### IAGSEngine.SimulateMouseClick
```
void SimulateMouseClick(int button);
```

Simulates the mouse being clicked by the player. `button` is which mouse button (1=left, 2=right, 3=middle) to simulate. The effect should be identical to the user clicking the equivalent button on their mouse.

_Added in version: 18_

#### IAGSEngine.GetMovementPathWaypointCount
```
int GetMovementPathWaypointCount(int pathId);
```

Gets the number of waypoints on the specified movement path.

The `GetMovementPath` family of functions allow you to access the paths for moving characters and objects in the game; and therefore allow you to anticipate where they will end up. The `pathId` is the value found in the `AGSCharacter.walking` and `AGSObject.moving` variables (but only if these variables are greater than 0; 0 or less means they are not moving).

_Added in version: 18_

#### IAGSEngine.GetMovementPathLastWaypoint
```
int GetMovementPathLastWaypoint(int pathId);
```

Gets the last waypoint that was passed on this movement path. The starting point is waypoint 0, and the destination is the `WaypointCount` minus 1 (though this can never be returned, since the move is marked as finished once the last waypoint is reached).

_Added in version: 18_

#### IAGSEngine.GetMovementPathWaypointLocation
```
void GetMovementPathWaypointLocation(int32 pathId, int32 waypoint, int32 *x, int32 *y);
```

Gets the X and Y co-ordinates of the specified waypoint on the specified path.

_![Warning](images/icon_warn.png)_ No error checking is done on these functions for performance reasons, so make sure you supply a valid `pathId` and `waypoint`.

_Added in version: 18_

#### IAGSEngine.GetMovementPathWaypointSpeed
```
void GetMovementPathWaypointSpeed(int32 pathId, int32 waypoint, int32 *xSpeed, int32 *ySpeed);
```

Gets the X and Y speed at which the character/object will move from the specified waypoint to the next. The speeds are returned as 32-bit **fixed point** numbers. This means that the high 16 bits is the whole part of the number, and the low 16 bits is the fractional part. For example, if `xSpeed` is 0x00038000, that would represent a speed of 3.5 pixels per frame.

_Added in version: 18_

#### IAGSEngine.IsRunningUnderDebugger
```
int IsRunningUnderDebugger();
```

Returns whether the game is currently running under the AGS Editor's debugger. If it is, then you are able to use the `BreakIntoDebugger` command.

_Added in version: 22_

#### IAGSEngine.BreakIntoDebugger
```
void BreakIntoDebugger();
```

Tells AGS to stop and break out into the editor's debugger. This will not happen immediately, but will happen when the next line of script code is run. This function will only work if `IsRunningUnderDebugger` returns 1.

_Added in version: 22_

#### IAGSEngine.GetPathToFileInCompiledFolder
```
void GetPathToFileInCompiledFolder(const char *fileName, char *buffer)
```

Fills in `buffer` with a path that you can use to open the specified file that resides in the Compiled folder.

If the game is running under the debugger, `buffer` will end up containing `Compiled_fileName_` .
Otherwise, `buffer` will simply be set to a copy of `fileName`.

You should allocate `buffer` as `MAX_PATH` bytes long.

_Added in version: 22_

#### IAGSEngine.GetDirectInputKeyboard
```
LPDIRECTINPUTDEVICE GetDirectInputKeyboard();
```

Returns a pointer to the `IDirectInputDevice` interface that AGS is using to control the keyboard. This command does **not** `AddRef` the pointer it returns, so you don't need to Release it.

_Added in version: 23_

#### IAGSEngine.GetDirectInputMouse
```
LPDIRECTINPUTDEVICE GetDirectInputMouse();
```

Returns a pointer to the `IDirectInputDevice` interface that AGS is using to control the mouse. This command does **not** `AddRef` the pointer it returns, so you don't need to Release it.

_Added in version: 23_

#### IAGSEngine.ReplaceFontRenderer
```
IAGSFontRenderer* ReplaceFontRenderer(int fontNumber, IAGSFontRenderer* newRenderer)
```

Replaces the font renderer that AGS is currently using to draw the specified font with one of your own. The old renderer is returned.

This allows you to override AGS's built-in font rendering with your own system. For example, if you didn't want to use SCI or TTF fonts, this allows you to provide a custom implementation. See further down this page for a description of the `IAGSFontRenderer` interface.

_Added in version: 23_

### IAGSScriptManagedObject interface

The `IAGSScriptManagedObject` interface is implemented for objects which the plugin wants to return to the game script. It allows a callback mechanism for AGS to request various operations on the object. You must implement the following:

#### IAGSScriptManagedObject.Dispose
```
int Dispose(const char *address, bool force);
```

Called when the reference count of the specified object reaches zero. The `address` parameter points to the particular object that is no longer referenced.

If `force` is zero, then you are merely being informed that the reference count has reached zero. Either you can destroy the object (in which case you should return 1), or you can leave it (return 0). If you leave it, then this function will be called again at various intervals to give you another opportunity to destroy the object.

If `force` is non-zero, then this is the object's last chance to free its memory and it will not be called again. This is the case if the player is about to restore a saved game, or is quitting the game, and so forth.

You must return 1 from this function if you destroy the object at `address` - in which case, it will be removed from the managed object pool. Return 0 if you do not destroy the object, in which case it will stick around.

_Added in version: 15_

#### IAGSScriptManagedObject.GetType
```
const char* GetType();
```

Returns the type name of the object. This must match the type name supplied to `AddManagedObjectReader` for the corresponding reader.

_Added in version: 15_

#### IAGSScriptManagedObject.Serialize
```
int Serialize(const char *address, char *buffer, int bufsize);
```

Called when the player saves the game. You must write any persistent data for the object at `address` into the supplied `buffer`. The buffer is `bufsize` bytes long, and you must not write any more data than that.

You must return the number of bytes written to the buffer.

_Added in version: 15_

### IAGSManagedObjectReader interface

The IAGSManagedObjectReader interface is implemented for each managed object type, to enable the objects to be reconstructed after being read back from disk. You must implement the following:

#### IAGSManagedObjectReader.Unserialize
```
void Unserialize(int key, const char *serializedData, int dataSize);
```

Called for each managed object when a saved game is restored. `serializedData` is the buffer that you wrote to in Serialize, and `dataSize` is the length of this buffer.

You should re-construct the object from the serialized data, and then re-register it using the `RegisterUnserializedObject` function. The `key` supplied to you here should be passed on unmodified to `RegisterUnserializedObject` in order for the object to be fully restored.

_Added in version: 15_

### IAGSFontRenderer interface

The `IAGSFontRenderer` interface can be implemented to override AGS's built-in text rendering with a custom system. The methods on the interface are as follows:

#### IAGSFontRenderer.LoadFromDisk
```
bool LoadFromDisk(int fontNumber, int fontSize);
```

Used internally by AGS to load the font from disk. However, you currently cannot insert a custom renderer early enough in the process to override this method, therefore it will never be called.

_Added in version: 23_

#### IAGSFontRenderer.FreeMemory
```
void FreeMemory(int fontNumber);
```

Called when the engine is shutting down, to free the memory associated with this font. You should perform your own clean-up here, and then call onto the `FreeMemory` method of the old renderer that you replaced.

_Added in version: 23_

#### IAGSFontRenderer.SupportsExtendedCharacters
```
bool SupportsExtendedCharacters(int fontNumber);
```

AGS will call this method to determine whether the specified font supports extended characters (ie. characters with a ASCII value of 128 or above). Return `true` or `false`, depending on your implementation.

_![Warning](images/icon_warn.png)_ If you return false from this function, AGS will not necessarily strip extended characters out of text. If you do not support extended characters, then you should implement the `EnsureTextValidForFont` method (below) to strip them out.

_Added in version: 23_

#### IAGSFontRenderer.GetTextWidth
```
int GetTextWidth(const char *text, int fontNumber);
```

AGS will call this method to find out the width, in pixels, of drawing the specified text in the specified font. You should return the number of pixels that this will take up (assuming the text is all on one line and does not wrap).

_Added in version: 23_

#### IAGSFontRenderer.GetTextHeight
```
int GetTextHeight(const char *text, int fontNumber);
```

AGS will call this method to find out the height, in pixels, of drawing the specified text in the specified font. You should return the number of pixels that this will take up (assuming the text is all on one line and does not wrap).

_Added in version: 23_

#### IAGSFontRenderer.RenderText
```
void RenderText(const char *text, int fontNumber, BITMAP *destination, int x, int y, int color);
```

AGS calls this method to render text to a bitmap. `destination` is the bitmap surface that AGS is rendering to (you can use this with other functions like `GetBitmapDimensions` and `GetRawBitmapSurface`), and you need to draw the `text` starting with its top-left position at (`x`, `y`) on this surface.

`color` is a raw pixel color, not an AGS color Number.

_Added in version: 23_

#### IAGSFontRenderer.AdjustYCoordinateForFont
```
void AdjustYCoordinateForFont(int *ycoord, int fontNumber);
```

This method is a workaround introduced for TTF fonts, which allows you to adjust the Y-position of the rendered text. You should implement this method so that it does nothing unless you have problems with text positioning.

_Added in version: 23_

#### IAGSFontRenderer.EnsureTextValidForFont
```
void EnsureTextValidForFont(char *text, int fontNumber);
```

AGS calls this method prior to actually rendering text, and allows you to check that all the characters in the text are supported by the font. If not, `text` is a writable buffer and you could replace them with question marks.

By default, you should implement this method so that it does nothing.

_Added in version: 23_
