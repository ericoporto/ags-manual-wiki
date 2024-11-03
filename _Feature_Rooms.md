## Rooms

In AGS Rooms are logical parts of the game. A Room may play various roles depending on the game's genre and your needs: it may represent a physical location in a game's world, a world's map or a closeup of an object, a mini game scene, just a placeholder for displaying something else on screen (such as a title screen, main menu or end credits).

A Room may be fixed in its looks and composition, or have its state changed over time completely with the use of scripting. For example, you could have a room showing a game's title, and then scroll sideways to the gameplay position. Or have same Room depict multiple similar locations, by toggling decorations and backdrops. Or depict same location but in different times of a day, and so on.

Rooms are identified simply by a number, ranging from 0 to 999 (number 0 is traditionally not used, but it's still available).

A Room may be "state-saving" and "not state-saving". The former keep their state when you leave them and have it restored when you enter them again. The latter have their state reset to initial setup when they are revisited.

The way it currently works in AGS, Room numbers 0-300 are defined as state-saving, and Room numbers 301-999 are non-state-saving. This makes AGS support up to 1000 rooms in a single game, 301 of them save their state and the rest 699 not.

Non-state-saving rooms help to save on memory, and also they guarantee that upon entering them their state will be exactly the same as you set it in the Editor each time player revisits this room. It's a good practice to have rooms serving as title screens, menus and similar be non-state-saving, because these usually don't need to be restored. Same goes to rooms which you know will only be visited once during a playthrough, such as cutscenes, for instance.

See Also: [Tutorial: Creating your first room](acintro2)

### Changing Rooms

Engine can have only a single Room loaded and active at the same time. The active Room is defined by the player character location. When the game is launched it first loads the room assigned as a player character's "starting room". Changing rooms is done by moving a player character elsewhere using [Character.ChangeRoom()](Character#characterchangeroom) script function.

Naturally, only one character is defined as "playable" at any given time. If you assign another character as playable using a script command (see [Character.SetAsPlayer()](Character#charactersetasplayer)), and that character happens to be in another room, then the rooms will get changed automatically.

### Displaying Rooms

A Room has a size, it's defined by the size of primary Room's background image. Room's coordinate system has a center (0,0) point at its background's top-left corner, X axis pointing from left to right and Y axis pointing from top to bottom, so the right-bottom point of the Room has coordinates (Width - 1, Height - 1).

Only Room Objects and Characters positioned within these coordinates are guaranteed to be visible, although technically they may take positions outside of the room's bounds too. Having objects outside of the room background is one way to keep them out of sight, or prepare them before entering the scene. For instance, it's possible to place a Character at negative coordinates at room's load event prior to "fade-in", then in the "after fade-in" event make that character walk onto the room background as a small cutscene. It is similarly possible to make Characters walk outside of the room background before transitioning to another room.

Speaking of displaying a room on screen, AGS uses a concept of Room's Camera and Viewport. You may think of a Camera as of an "eye" located inside the Room and showing it whole or a part of its area, while Viewport is a "monitor" that displays what Camera can see on screen. By default both Camera and the Viewport are automatically set to either the Game's resolution or Room's size - whatever is smaller.

What that means, for example, if the Game's resolution is 320x200, and room is 320x200, then the room will occupy whole game screen. If room is 160x100, then it will occupy only portion of the game screen. In both of these cases the room will be fully seen on screen at all times.

However, if the room is larger than the Game's resolution, say it's 640x200, the room's Viewport will still be restricted by the game's resolution - 320x200, and only half of the room will be visible at once. As the camera moves around the room, different parts of it will be seen on screen. Rooms larger than the game are traditionally called "scrolling rooms", because when the camera moves it looks like the room is scrolling before player's eyes.

By default the camera is centered at player character. When player character walks around the room, the camera will follow as far as it can without crossing the room's bounds. There are ways to control the camera using [relevant script commands](Camera).

See Also: [Camera functions and properties](Camera), [Viewport functions and properties](Viewport)

### Room contents

Besides their basic settings, rooms may have following contents in them:

* Backgrounds
* Edges
* Hotspots
* Room Objects
* Walkable areas
* Regions
* Walk-behinds

See Also: [Room Editor](EditorRoom)

### Room Backgrounds

Backgrounds are images that are displayed at the back of the room. Room must have at least a single background (this is called "main background"), but it does not have to be an actual image, and may be just a bitmap filled with a black color, for instance. It's still necessary to have one, as main background defines the room's size: that is the area that will ever be visible on screen.

It's possible to add up to 5 backgrounds total for a room. The extra backgrounds are commonly meant for two purposes:
1. Displaying different variants of the room. This may be used, for example, to have day and night versions of the same room.
2. Animating room background. That is known as a full room animation, and usually used when the whole background must change as one piece.

Backgrounds are limited in what you may achieve with them alone, not only because their max number is small (5), but also because they are just flat images.
For complex room transformations and visual effects (such as parallax, for instance) isually one would use a combination of background and multiple room objects, moving and animating simultaneously.

### Room Edges

Room Edges are four lines that define room's playable area (Left, Right, Top and Bottom edges). These are optional, and may be ignored if not needed.
Their purpose is to detect when player character crosses them, in which case they trigger a respective [room event](EventTypes#room-events): "Walk off left edge", "Walk off right edge", and so on. This is commonly used to script exits to other rooms.

One downside of using a Room Edge is that it is a straight line running across the whole room, and will trigger regardless of which poi character crosses it. If the room has a more complex layout, then Hotspots or Regions would be more suitable for the same purpose.

See Also: [Room events](EventTypes#room-events)

### Hotspots

Hotspots are parts of the room background that may be interacted with by the player. They are created by drawing areas of different colors on a "hotspot mask" image, - that is a sort of a layer that covers whole room but is invisible at runtime. Each hotspot is associated with its distinct color.

There's only the single "hotspot mask" for all hotspots, which means that hotspots *cannot overlap*. On another hand, a single hotspot may consist of multiple disconnected parts and all of these parts will act as one.

As hotspots are a part of a mask, they do not have any visual representation of their own, they rather use the room background for that. That's why hotspots are commonly used to add interaction to certain areas, or things drawn on the room background that *do not change position or shape*.

Hotspots can react to following:
* Player clicking on them;
* Player character standing on them;
* Cursor moving over them.

Each of the above triggers [corresponding event](EventTypes#hotspot-events), which in turn may run a custom function in script.

Hotspot may have a Walk-to Point: that's an optional setting that tells where a character will walk to automatically when the player clicks on hotspot.

A hotspot may be enabled or disabled by a [script command](Hotspot#hotspotenabled). Disabled hotspots do not react to any interactions.

See Also: [Tutorial: hotspots](acintro3#hotspots), [Hotspot events](EventTypes#hotspot-events), [Hotspot functions and properties](Hotspot)

### Room Objects

Room Objects are things in room that have their own image, position and visual properties. They may be moved around, change their visuals, turned on and off.

Room Objects may be clicked on by player to trigger one of their interaction events.

See Also: [Tutorial: room objects](acintro4#objects), [Object events](EventTypes#object-events), [Object functions and properties](Object)

### Walkable areas

### Regions

### Walk-behinds
