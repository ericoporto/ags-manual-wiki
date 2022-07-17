## Global functions (Wait)

Since AGS 3.6.0, All Wait related functions can return a **Skip Reason** on why they were skipped:

- `0` - ended by timeout or `SkipWait()`;
- `!= 0` - an integer value which combines [InputType](StandardEnums#inputtype), [KeyMod](Keycodes#key-modifiers), and a key or button code corresponding to that input type; that describes what input device and which button on that device were used to skip this "wait".

If you only need to find out whether WaitX ended with a timeout or a player's input, all you need is to compare it with `0`:

    if (WaitMouseKey(100) == 0) {
        Display("Time out!");
    }

    if (WaitMouse(100) != 0) {
        Display("Skipped by a mouse click.");
    }

If you need to determine exact details of how the "wait" was skipped, you have to split returned value into `InputType`, key mod, and a button code using [bitwise operations](ScriptKeywords#operators):

    int result = WaitMouseKey(100);
    InputType type = result & eInputAny;
    int keymod = result & eKeyModMask; // extract key mod flags
    int keycode = result & eKeyCodeMask; // extract key or button code

For example, this is how you may Wait until player presses either Space key or Left Mouse button:

    while (true) {
        int result = WaitMouseKey(-1);
        InputType type = result & eInputAny;
        int keycode = result & eKeyCodeMask;
        if ((type == eInputMouse && keycode == eMouseLeft) ||
            (type == eInputKey && keycode == eKeySpace)) {
            break; // break the waiting loop
        }
    }

and this is how the key combinations may be tested (Ctrl + S in this case):

    while (true) {
        int result = WaitKey(-1);
        int keycode = result & eKeyCodeMask;
        int keymod = result & eKeyModMask;
        if (keymod == eKeyModCtrl && keycode == eKeyS) {
            break; // break the waiting loop
        }
    }

---

### `SkipWait`

    void SkipWait ()

Cancels current Wait function, regardless of its type, if one was active at the moment.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`WaitKey`](Globalfunctions_Wait#waitkey),
[`WaitMouse`](Globalfunctions_Wait#waitmouse),
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`Game.BlockingWaitSkipped`](Game#gameblockingwaitskipped)

---

### `Wait`

    void Wait (int time)

Pauses the script and lets the game continue for TIME loops. There are
normally 40 loops/second (unless you change it with SetGameSpeed), so
using a value of 80 will wait 2 seconds. Note that no other scripts can
run while the Wait function is in the background.

Example:

    cEgo.Walk(120, 140, eBlock, eWalkableAreas);
    Wait(80);
    cEgo.FaceLocation(1000,100);

will move the character EGO to 120,140, wait until he gets there then
wait for 2 seconds (80 game cycles) and then face right.

*See also:* [`WaitKey`](Globalfunctions_Wait#waitkey),
[`WaitMouse`](Globalfunctions_Wait#waitmouse),
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`Game.BlockingWaitSkipped`](Game#gameblockingwaitskipped)

---

### `WaitInput`

    int WaitInput(InputType types, int timeout = -1)

Pauses the script and lets the game continue until EITHER:

- `timeout` loops have elapsed, or
- the player presses a key or button on one of the devices listed in `types`

The `types` may contain any combined values from the [`InputType` enum](StandardEnums#inputtype).

If `timeout` is -1, it will Wait forever, until a key is pressed.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- `0` - ended by timeout;
- `!= 0` - ended by player input;

Example:

    WaitInput(eInputKeyboard + eInputMouse, 200);

will pause the script and wait until 5 seconds have passed (if game is 40 frames per second) or the player
presses a key or clicks the mouse.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Wait`](Globalfunctions_Wait#wait), 
[`WaitKey`](Globalfunctions_Wait#waitkey), 
[`WaitMouse`](Globalfunctions_Wait#waitmouse),
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`Game.BlockingWaitSkipped`](Game#gameblockingwaitskipped),
[`SkipWait`](Globalfunctions_Wait#skipwait)

---

### `WaitKey`

    int WaitKey (int timeout = -1)

Pauses the script and lets the game continue until EITHER:

- `timeout` loops have elapsed, or
- the player presses a key

If `timeout` is -1, it will Wait forever, until a key is pressed.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- `0` - ended by timeout;
- `!= 0` - ended by key keycode;

Example:

    WaitKey(200);

will pause the script and wait until 5 seconds have passed or the player
presses a key.

*See also:* [`Wait`](Globalfunctions_Wait#wait),
[`WaitMouse`](Globalfunctions_Wait#waitmouse),
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`Game.BlockingWaitSkipped`](Game#gameblockingwaitskipped)

---

### `WaitMouseKey`

    int WaitMouseKey (int timeout = -1)

Pauses the script and lets the game continue until EITHER:

- `timeout` loops have elapsed, or
- the player presses a key, or
- the player clicks a mouse button

If `timeout` is -1, it will Wait forever, until either a key is pressed or the mouse is clicked.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- `0` - ended by timeout;
- `!= 0` - ended by keycode or mouse click;

Example:

    WaitMouseKey(200);

will pause the script and wait until 5 seconds have passed or the player
presses a key or clicks the mouse.

*See also:* [`Wait`](Globalfunctions_Wait#wait), 
[`WaitKey`](Globalfunctions_Wait#waitkey),
[`WaitMouse`](Globalfunctions_Wait#waitmouse),
[`Game.BlockingWaitSkipped`](Game#gameblockingwaitskipped)

---

### `WaitMouse`

    int WaitMouseKey (int timeout = -1)

Pauses the script and lets the game continue until EITHER:

- `timeout` loops have elapsed, or
- the player clicks a mouse button

If `timeout` is -1, it will Wait forever, until the mouse is clicked.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- `0` - if the time elapsed, or 
- `!= 0` - ended by mouse click;

Example:

    WaitMouse(200);

will pause the script and wait until 5 seconds have passed (if game is 40 frames per second) or the player
presses clicks the mouse.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Wait`](Globalfunctions_Wait#wait), 
[`WaitKey`](Globalfunctions_Wait#waitkey), 
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`Game.BlockingWaitSkipped`](Game#gameblockingwaitskipped),
[`SkipWait`](Globalfunctions_Wait#skipwait)