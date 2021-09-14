## Global functions (Wait)


Since AGS 3.6.0, All Wait related functions can return a **Skip Reason** on why they were skipped:

- `0 =` ended by timeout;
- `> 0 =` keycode;
- `< 0 =` negated mouse button code minus one (because of how mouse codes start with 0). In order to get mouse code do this: MouseButton btn = -(result + 1);


---

### `SkipWait`

    void SkipWait ()

Cancels current Wait function, regardless of its type, if one was active at the moment.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`WaitKey`](Globalfunctions_General#waitkey),
[`WaitMouse`](Globalfunctions_General#waitmouse),
[`WaitMouseKey`](Globalfunctions_General#waitmousekey),
[`BlockingWaitSkipped`](Game#blockingwaitskipped)

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

*See also:* [`WaitKey`](Globalfunctions_General#waitkey),
[`WaitMouse`](Globalfunctions_General#waitmouse),
[`WaitMouseKey`](Globalfunctions_General#waitmousekey),
[`BlockingWaitSkipped`](Game#blockingwaitskipped)

---

### `WaitKey`

    int WaitKey (int timeout = -1)

Pauses the script and lets the game continue until EITHER:

\(a) `timeout` loops have elapsed, or

\(b) the player presses a key

If `timeout` is -1, it will Wait forever, until a key is pressed.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- `0 =` ended by timeout;
- `> 0 =` keycode;

Example:

    WaitKey(200);

will pause the script and wait until 5 seconds have passed or the player
presses a key.

*See also:* [`Wait`](Globalfunctions_Wait#wait),
[`WaitMouse`](Globalfunctions_General#waitmouse),
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`BlockingWaitSkipped`](Game#blockingwaitskipped)

---

### `WaitMouseKey`

    int WaitMouseKey (int timeout = -1)

Pauses the script and lets the game continue until EITHER:

\(a) `timeout` loops have elapsed, or

\(b) the player presses a key, or

\(c) the player clicks a mouse button

If `timeout` is -1, it will Wait forever, until either a key is pressed or the mouse is clicked.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- `0 =` ended by timeout;
- `> 0 =` keycode;
- `< 0 =` negated mouse button code minus one (because of how mouse codes start with 0). In order to get mouse code do this: MouseButton btn = -(result + 1);

Example:

    WaitMouseKey(200);

will pause the script and wait until 5 seconds have passed or the player
presses a key or clicks the mouse.

*See also:* [`Wait`](Globalfunctions_Wait#wait), 
[`WaitKey`](Globalfunctions_Wait#waitkey),
[`WaitMouse`](Globalfunctions_General#waitmouse),
[`BlockingWaitSkipped`](Game#blockingwaitskipped)

---

### `WaitMouse`

    int WaitMouseKey (int timeout = -1)

Pauses the script and lets the game continue until EITHER:

\(a) `timeout` loops have elapsed, or

\(b) the player clicks a mouse button

If `timeout` is -1, it will Wait forever, until the mouse is clicked.

Returns the **Skip Reason** of why it was skipped (see top of this page for more details):

- 0 if the time elapsed, or 
- `< 0 =` negated mouse button code minus one (because of how mouse codes start with 0). In order to get mouse code do this: MouseButton btn = -(result + 1);

Example:

    WaitMouse(200);

will pause the script and wait until 5 seconds have passed (if game is 40 frames per second) or the player
presses clicks the mouse.


*Compatibility:* Supported by **AGS 3.6.0** and later versions.

*See also:* [`Wait`](Globalfunctions_Wait#wait), 
[`WaitKey`](Globalfunctions_Wait#waitkey), 
[`WaitMouseKey`](Globalfunctions_Wait#waitmousekey),
[`BlockingWaitSkipped`](Game#blockingwaitskipped),
[`SkipWait`](Globalfunctions_Wait#skipwait)