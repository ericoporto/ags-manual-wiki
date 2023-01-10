## System limits

This section tells you the maximums for various parts of the system. If
you have been wondering "How many rooms can I have?" or something
similar, chances are this section will answer it.

### System restrictions

- 90000 imported sprites
- 300 inventory items
- 999 rooms per game, 300 of which may be state-saving (0-299)
- 5 background frames per room
- 256 objects per room
- 49 hotspots per room (50 with "no hotspot" area)
- 15 walkable areas per room (16 with "non-walkable" area)
- 15 walk-behinds per room (16 with "no walk-behind" area)
- 15 regions per room (16 with "no region" area)
- 30 options per dialog topic
- 20 mouse cursors
- 20 timers
- 16 audio channels
- 126 different script modules due to bytecode format
- unlimited characters
- unlimited dialog topics
- unlimited fonts
- unlimited GUIs
- unlimited controls on each GUI
- unlimited views (animation sets), loops in view, and frames in loop
- unlimited words in the text parser dictionary
- unlimited custom properties
- unlimited screen overlays at runtime

#### Integers and Floats limits

- In AGS integers and floats are 32-bit
    - Integers are signed and can be from -2147483648 to +2147483647 (from $-2^{31}$ to $+2^{31}-1$)
    - Floats are [a bit more complicated](https://en.wikipedia.org/wiki/Single-precision_floating-point_format): an [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) 32-bit base-2 floating-point variable has a maximum value of $(2 − 2^{-23}) × 2^{127} ≈ 3.4028235 × 10^{38}$. A float is then be able to hold integer values between $-2^{127}$ and $2^{127}$.

Following code will print all integers from 2^24 (=16777216) to 2^127 (=170141183460469231731687303715884105728), assuming that debugPrint() writes to a text file:

```
for (int i = 24; i <=127; i++) {
  float exponent = IntToFloat(i); 
  float result = Maths.RaiseToPower (2.0, exponent);
  debugPrint(String.Format("2^%d = %.0f", i,  result), false); // "%.0f" will print a float without any decimal digit, simulating an integer
}
```

Please note that direct conversion (casting) is not allowed in scripts, hence conversion from/to int/float must be explicit, using IntToFloat() or FloatToInt().


Result:

* 2^24 = 16777216     
* 2^25 = 33554432     
* 2^26 = 67108864     
* 2^27 = 134217728    
* 2^28 = 268435456    
* 2^29 = 536870912    
* 2^30 = 1073741824   
* 2^31 = 2147483648   
* 2^32 = 4294967296   
* 2^33 = 8589934592   
* 2^34 = 17179869184  
* 2^35 = 34359738368  
* 2^36 = 68719476736  
* 2^37 = 137438953472 
* 2^38 = 274877906944 
* 2^39 = 549755813888 
* 2^40 = 1099511627776
* ...
* 2^125 = 42535295865117307932921825928971026432 
* 2^126 = 85070591730234615865843651857942052864 
* 2^127 = 170141183460469231731687303715884105728

Same values are allowed as negative, so the full range of "integers as floats" is: from $-2^{127}$ to $2^{127}$ .

### Additional considerations

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
