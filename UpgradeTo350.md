## Upgrading to 3.5.0

3.5.0 is another big update and it has few serious changes to both editor UI and scripting.

**Room editor and multilayer mode**

Room editor has got a new navigation bar on the top of the panel instead of the plain drop-down list where you used to select edit mode. This navigation bar lets you do following:

* See full list of objects grouped into layers by type (characters, objects, edges and so forth).
* Select editing mode, and particular item for edit.
* Toggle each group's and even each item's visibility in any combinations. This lets you display, for example, characters, objects and walkable areas at the same time. The only exception is that you may only display one type of area mask at the same time (that is - either walkable areas, regions, hotspots or walk-behinds).
* Toggle each group's and each item's locked state. When locked the object cannot be moved or has its shaped changed (as with mask areas which may be changed by painting).

Note that you can still only select and edit objects of the chosen group, not all at once.

**Deprecated relative asset resolutions**

This is something users do not know much about now, but may stumble upon sometimes. In the long past AGS divided all games into "low-resolution" and "high-resolution" games, "high-res" was defined roughly as 640x400 and higher while "low-res" was 320x200 or 320x240. Similarily AGS allowed certain assets, such as sprites, fonts and rooms, be tagged as "low-res" or "high-res". The idea behind this was that if a "low-res" asset is used in a "high-res" game then it get automatically scaled up x2, and vice-versa a "high-res" asset in a "low-res" game would be downscaled x2.

Although such practice is not commonly used for a while, you could still experience this effect if you, for example, take game template or project made in low resolution and convert it to high resolution. Some sprites from original game which were marked as "low-res" will be scaled up. Sometimes this behavior may be useful - in case you are using these sprites as placeholders, but may cause confusion among unexperienced users.

In AGS 3.5.0 we are deprecating concept of resolution tags and disable these conversions *by default*. We also make asset scaling more explicit in attempt to prevent its misuse.

1. Rooms no longer have a resolution tag, and are always considered having "real" resolution. This is actually only relevant if you are upgrading from pre-AGS 3.0 era. If you import 2.72 game into AGS 3.5.0 your rooms will get resized to match game resolution (unless they aready do).

2. Sprites retain resolution tag for backwards compatibility, but it is now set to "Real" by default and not recommended to change. When you import older project sprites get "promoted" to "real" resolution if their tag matches the game: for example if a sprite is tagged as "low-res" and your game is 320x200, or if a sprite is tagged as "high-res" and your game is 640x400 or higher.

3. "Fonts designed for high resolution" setting was removed, because it no longer makes sense. Instead, each font has an individual ScalingMultiplier property. When importing older project each font will be scaled x2 if it was a "high-res" game and this setting was OFF.

**Room sizes and mask resolution**

Previously AGS had a restriction that a room background must be at least size of a game resolution. With 3.5.0 this restriction is gone and you can now make rooms any size. This became possible after rewrite of the viewport system, which is explained in its own section below.

Another change is related to the room masks that define walkable areas, hotspots and so forth. Historically only walk-behinds mask was always made equal to the size of room background. Other masks were 1:1 to room background's size only in "low-res" games (below 640x400). In "high-res" games (640x400 and above) hotspots, regions and walkable masks were made x2 smaller resolution than the room, which means that for 4 room pixels (2x2 square) there was 1 mask pixel. That in turn caused these masks to be less precise. Originally this was done to reduce both memory size of a room and speed up any operations run against these masks (such as pathfinding), but sometimes caused annoyance to users who were unable to draw exactly a region they want.

Since 3.5.0 each room has a property called MaskResolution which currently ranges from 1:1 to 1:4. This resolution determines resolution factor for hotspots, regions and walkable masks (but not walk-behinds which is still fixed at 1:1). Default is 1:1, but you may change it anytime for any individual room if you prefer your room to have *less precise* area masks.<br>
To make things more convenient there's also an option in General Settings called "Default mask resolution" which lets you choose a value that will be applied to every newly created room.<br>
Note that when importing older projects the mask resolution is kept unchanged.
