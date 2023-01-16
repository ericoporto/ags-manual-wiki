## System limits

This section tells you the maximums for various parts of the system. If
you have been wondering "How many rooms can I have?" or something
similar, chances are this section will answer it.

### System restrictions

| Item | 3.5.0 | 3.5.1 | 3.6.0 |
|-|-|-|-|
| Imported sprites | 90000 | 90000 | 90000 |
| Dynamic sprites (at runtime) | 2+ billion | 2+ billion| 2+ billion |
| Characters | unlimited | unlimited  | unlimited |
| Cursors | 20 | 20 | **unlimited** |
| Fonts | unlimited | unlimited | unlimited |
| GUI | unlimited | unlimited | unlimited |
| Controls per GUI | unlimited | unlimited | unlimited |
| Inventory items | 300 | 300 | 300 |
| Overlays (at runtime) | 20 | 20 | **unlimited** |
| Views (animation sets) | unlimited  | unlimited  | unlimited  |
| Rooms per game, total | 1000 | 1000 | 1000 |
| State-saving rooms | 300 | 300 | 300 |
| Background frames per room | 5 | 5 | 5 |
| Room Objects per room | 40 | 40 | **256** |
| Hotspots per room | 49 | 49 | 49 |
| Walkable areas per room | 15 | 15 | 15 |
| Walk-behinds per room | 15 | 15 | 15 |
| Regions per room | 15 | 15 | 15 |
| Dialog topics | unlimited | unlimited | unlimited |
| Dialog options per topic | 30 | 30 | 30 |
| Custom properties | unlimited | unlimited | unlimited |
| Timers (at runtime) | 20 | 20 | 20 |
| Audio channels | 8 | 8 | **16** |
| Script modules (limited by the bytecode format) | 126 | 126 | 126 |
| Dynamic array size | 1 million | **2+ billion** | **2+ billion** |

### Integers and Floats limits 

In AGS integers and floats are 32-bit.
- Integers are signed and can be from -2147483648 to +2147483647 (from `-2^31` to `2^31-1`)
- Floats are [a bit more complicated](https://en.wikipedia.org/wiki/Single-precision_floating-point_format): an [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) 32-bit base-2 floating-point variable has a maximum value of `2 − 2^(-23) × 2^127 ≈ 3.4028235 × 10^38`. 
- A float should then be able to reliably represent integer values between -16777216 and 16777216 (from `-2^24` to `2^24`).

### Additional considerations

- You should be able to have up to 15 parameters to a function.

- To ensure the pathfinder always works, your walkable areas should always be at least 3 pixels wide.

- AGS currently allows the call stack to be 50 levels deep, so if you have a recursive function that calls itself more often you'll get the "call stack overflow" error. Additionally, the stack size is set at 4 KB so if the recursive function declares a lot of local variables you could reach the limit that way, too.

- There is a total overall limit on the number of functions that can be exported by all plugins added together, which in theory it would be possible for a single plugin to exceed. It's in the region of a couple of hundred though, so it shouldn't be an issue. It wouldn't be too difficult to increase, if the need arose.

We are working on removing existing limitations in the AGS, so some of the remaining restrictions might be loosened or eliminated in the following updates.
