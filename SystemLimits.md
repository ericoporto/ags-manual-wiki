## System limits

This section tells you the maximums for various parts of the system. If
you have been wondering "How many rooms can I have?" or something
similar, chances are this section will answer it.

### System restrictions

- 256 objects per room
- 299 state-saving rooms per game
- 300 inventory items
- 90000 imported sprites
- 30 options per dialog topic
- 20 timers
- 5 background frames per room
- 20 mouse cursors
- 16 audio channels
- 126 different script modules due to bytecode format
- unlimited words in the text parser dictionary
- unlimited fonts
- unlimited characters
- unlimited dialog topics
- unlimited views
- unlimited GUIs
- unlimited controls on each GUI
- unlimited loops per view
- unlimited frames per loop
- unlimited custom properties
- unlimited screen overlays at a time

### Additional considerations

- In AGS integers and floats are 32-bit. Integers can be from -2147483648 to +2147483647, and floats are a bit more complicated, so it's better to test them.

- You should be able to have up to 15 parameters to a function.

- To ensure the pathfinder always works, your walkable areas should always be at least 3 pixels wide.

- AGS currently allows the call stack to be 50 levels deep, so if you have a recursive function that calls itself more often you'll get the "call stack overflow" error. Additionally, the stack size is set at 4 KB so if the recursive function declares a lot of local variables you could reach the limit that way, too.

- There is a total overall limit on the number of functions that can be exported by all plugins added together, which in theory it would be possible for a single plugin to exceed. It's in the region of a couple of hundred though, so it shouldn't be an issue. It wouldn't be too difficult to increase, if the need arose.

We are working on removing existing limitations in the AGS, so some of the remaining restrictions might be loosened or eliminated in the following updates.

### Changelog of lifted limits

AGS v3.6:
- Audio channels number increased from 8 to 16.
- Increased Room Objects limit to 256 (was 40).
- 20 screen overlays at a time lifted
- Removed limit of simultaneous Button animations (was 15).
- Removed limit of Character followers (was 30).

AGS v3.5
- packed sprites file (acsprset.spr) lifted from 2 GB limit
- Imported sprites count limit raised from 30000 to 90000
- Total number of sprites in game (includes both imported and Dynamic Sprites) lifted to around 2 billions of dynamic sprites
- Font count limit of 30 removed
- length limit on the Button lifted from 50 character
- length limit on TextBox lifted from 200 lines
- ListBox item count limit lifted from 200
- hidden limit for DoOnceOnly token length lifted from 200 characters
- local messages per room limit lifted from 100 (excluding script)
