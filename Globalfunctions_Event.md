## Global event handlers

In the AGS game there is a number of events, like starting the game, or pressing the key, that may be handled in script by adding a function with *predefined name*. These are called "global event handlers". If you add ones to your script, they will be called automatically whenever corresponding event occurs. All of these are optional, and may be omited if you don't need them.

You may you add multiple functions of the same kind to multiple [script modules](ScriptModules), in which case they will be called in the order of modules in your game project. It's possible to stop propagating the event (skip remaining modules) by using [`ClaimEvent`](Globalfunctions_General#claimevent) function (refer to its article for explanation).

Some of these functions may also be added to the room scripts. These are: `on_event`, `on_key_press`, `on_mouse_click`, `on_text_input`, `repeatedly_execute_always`, `late_repeatedly_execute_always`.

Some functions will only work in the room script: `on_call`.

*NOTE:* for historical reasons, function `repeatedly_execute` does not work in the room script, but there's a corresponding room event that may be linked to a custom function in the editor.

---

### `dialog_request`

```ags
dialog_request (int parameter)
```

Called when a dialog script line "run-script" is processed. PARAMETER
is the value of the number following the "run-script" on that line of
the dialog script.

---

### `game_start`

```ags
game_start ()
```

Called at the start of the game, before the first room is loaded. You
would typically use this to set up the initial positions of
characters, and to modify initial visibility of GUIs.

**Note:** When this function is called it is too early to run
animations or do anything else which relies on a room being loaded

---

### `interface_click`

```ags
interface_click (int interface, int button)
```

Called when the player clicks on a button on a GUI which has its
action set as "Run script". INTERFACE is the number of the GUI which
they clicked on. BUTTON is the object number of the button within this
GUI.

---

### `on_event`

```ags
on_event (EventType event, int data)
```

Called whenever certain game events occur. The value of DATA depends
on which event has occurred. The possible values of event are:

    eEventEnterRoomBeforeFadein
            called just before the room's 'Enter Before Fade-in' event occurs
            DATA = new room number
    eEventEnterRoomAfterFadein
            called just before the room's 'Enter After Fade-in' event occurs
            DATA = room number
    eEventLeaveRoom
            called just after the room's 'Player Leaves Room' event occurs
            DATA = room number they are leaving
    eEventGotScore
            called whenever the player's score changes
            DATA = number of points they've received
    eEventGUIMouseDown
            called when a mouse button is pressed down over a GUI
            DATA = GUI number
    eEventGUIMouseUp
            called when a mouse button is released over a GUI
            DATA = GUI number
    eEventAddInventory
            called when the player has just added an inventory item
            DATA = inventory item number that was added
    eEventLoseInventory
            called when the player has just lost an inventory item
            DATA = inventory item number that was lost
    eEventRestoreGame
            called after a saved game has been restored
            DATA = save slot number

*Compatibility:* `eEventEnterRoomAfterFadein` event type is only supported since AGS 3.6.0.

---

### `on_key_press`

```ags
on_key_press (eKeyCode keycode, optional int mod)
```

Called whenever a key is pressed on the keyboard. `keycode` holds the value of the key, while `mod` holds a combination of modifiers pressed alongside with that key. A list of these values is [available here](Keycodes).

The `mod` argument is optional and may be omited. The `mod` contains *set of flags*, and is slightly more complicated than keycode: as you should not use regular comparison (`==`, `!=`) with it, but a bitwise operator (`&`):

```ags
// these two conditions check that ctrl was pressed (these commands are equivalent)
if (mod & eKeyModCtrl)
if (mod & eKeyModCtrl != 0)


// these two conditions check that ctrl was NOT pressed (again, two variants of the same check)
if (!(mod & eKeyModCtrl))
if (mod & eKeyModCtrl == 0)
```

The `on_key_press` function can also be defined in individual room
scripts. This allows the room script to intercept a key-press first,
and then decide whether to pass it on to the global script or not. See
the [`ClaimEvent`](Globalfunctions_General#claimevent) function for more
details.

Starting with version 3.6.0 AGS supports two "key handling" modes: a new-style and old-style (backwards compatible). This mode is selected in the [General Settings](GeneralSettings#backwards-compatibility) with "Use old-style key handling" option in the "Backwards compatibility" group.

**New key mode:**
 - all keys are passed into the `on_key_press` function as-is, one by one: for example, if you press Ctrl + Z, then you get **two** `on_key_press` calls, one with `eKeyCtrlLeft` and another with `eKeyZ` argument.

**Old (classic) key mode:**
 - lone mod keys (Ctrl, Alt, Shift) are not passed into the `on_key_press`; you may only test if these are pressed using [IsKeyPressed](Globalfunctions_General#iskeypressed).
 - alphabet keys + ctrl combinations are merged into one key code for the `on_key_press` callback: e.g. `eKeyCodeCtrlA` and similar key codes.

*Compatibility:* The `mod` argument is only supported since AGS 3.6.0.

---

### `on_mouse_click`

```ags
on_mouse_click (MouseButton button)
```

Called when the player clicks a mouse button. BUTTON is either
`eMouseLeft`, `eMouseRight`, or `eMouseMiddle`, depending on which
button was clicked. The `mouse.x` and `mouse.y` global variables
contain the mouse's position.

If 'Handle inventory clicks in script' is enabled in the game options,
this function can also be called with `eMouseLeftInv`,
`eMouseMiddleInv` or `eMouseRightInv`, which indicate a left, middle
or right click on an inventory item, respectively.

If 'Enable mouse wheel support' is enabled, this function can also be
called with eMouseWheelNorth or eMouseWheelSouth, which indicate the
user moving the mouse wheel north or south, respectively.

The `on_mouse_click` function can also be defined in individual room
scripts. This allows the room script to intercept a mouse-click first,
and then decide whether to pass it on to the global script or not. See
the [`ClaimEvent`](Globalfunctions_General#claimevent) function for
more details.

---

### `on_text_input`

```ags
on_text_input(int ch)
```

Called when the player's key presses form a printable character. The difference between this and `on_key_press` is that not every key corresponds to the printable char, and some chars may be created by pressing multiple keys (which also depends on the current system language).

The `ch` argument contains a unicode character code, and may be used with the [String functions](String).

For example:

```ags
MyLabel.Text = MyLabel.Text.AppendChar(ch);
```

will append the new printed character to a label's text.

**IMPORTANT:** this function only works when your game uses "new-style key handling mode". This mode is selected in the [General Settings](GeneralSettings#backwards-compatibility) with "Use old-style key handling" option in the "Backwards compatibility" group.

*Compatibility:* supported since AGS 3.6.0.

---

### `repeatedly_execute`

```ags
repeatedly_execute()
```

Called every game cycle (normally 40 times per second). Additional
information is [available here](RepExec).

---

### `repeatedly_execute_always`

```ags
repeatedly_execute_always()
```

Called every game cycle, even when a blocking routine (e.g speech or
cutscene) is in progress. You **cannot** call any blocking functions
from this event handler. `repeatedly_execute_always` is called
**before** the game entities (characters, rooms, etc) get updated.
Additional information is [available here](RepExec).

---

### `late_repeatedly_execute_always`

```ags
late_repeatedly_execute_always()
```

Called every game cycle, even when a blocking routine (e.g. speech or
cutscene) is in progress. You **cannot** call any blocking functions
from this event handler. `late_repeatedly_execute_always` is called
**after** the game entities (characters, rooms, etc) have been
updated, but before the game screen is redrawn.

---

### `unhandled_event`

```ags
unhandled_event (int what, int type)
```

Called when an event occurs, but no corresponding event handler has
been configured. This is typically used to display a default "I can't
do that" type response in-order to avoid having to add unique
messages for all in-game interactions. The values of WHAT and TYPE
tell you what the player did. The possible values are listed below:

WHAT | TYPE | Description
--- | --- | ---
1 | 1 | Look at hotspot
1 | 2 | Interact with hotspot
1 | 3 | Use inventory on hotspot
1 | 4 | Talk to hotspot
1 | 7 | Pick up hotspot
1 | 8 | Cursor Mode 8 on hotspot
1 | 9 | Cursor Mode 9 on hotspot
2 | 0 | Look at object
2 | 1 | Interact with object
2 | 2 | Talk to object
2 | 3 | Use inventory on object
2 | 5 | Pick up object
2 | 6 | Cursor Mode 8 on object
2 | 7 | Cursor Mode 9 on object
3 | 0 | Look at character
3 | 1 | Interact with character
3 | 2 | Speak to character
3 | 3 | Use inventory on character
3 | 5 | Pick up character
3 | 6 | Cursor Mode 8 on character
3 | 7 | Cursor Mode 9 on character
4 | 1 | Look at nothing (i.e. no hotspot)
4 | 2 | Interact with nothing
4 | 3 | Use inventory with nothing
4 | 4 | Talk to nothing
5 | 0 | Look at inventory
5 | 1 | Interact with inventory (currently not possible)
5 | 2 | Speak to inventory
5 | 3 | Use an inventory item on another
5 | 4 | Other click on inventory

**Note**: the "Character stands on hotspot" event does not trigger
this function, nor will it be triggered if there is an "Any click"
event handler defined, nor if the player clicks on nothing (hotspot 0)

---

### `on_call`

```ags
on_call (int value)
```

This callback can only be declared on Room Script.

It's called after the function `CallRoomScript(value)` is executed,
but not immediately. You can read an arbitrary integer value passed
from `CallRoomScript`. Additional information is [available here](Globalfunctions_General#callroomscript).

