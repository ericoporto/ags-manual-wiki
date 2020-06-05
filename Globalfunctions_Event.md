## Global functions (Event Handlers)

In your global script file, some functions will have been
automatically added when you created your game. These are global event
handlers, and these functions are called when particular events occur.
There are also some optional event handlers, which you can add if you
would like specific additional events to be processed.

### `dialog_request`

    dialog_request (int parameter)

Called when a dialog script line "run-script" is processed. PARAMETER
is the value of the number following the "run-script" on that line of
the dialog script.

---

### `game_start`

    game_start ()

Called at the start of the game, before the first room is loaded. You
would typically use this to set up the initial positions of
characters, and to modify initial visibility of GUIs.

**Note:** When this function is called it is too early to run
animations or do anything else which relies on a room being loaded

---

### `interface_click`

*(This function is now obsolete)*

    interface_click (int interface, int button)

Called when the player clicks on a button on a GUI which has its
action set as "Run script". INTERFACE is the number of the GUI which
they clicked on. BUTTON is the object number of the button within this
GUI.

---

### `on_event`

    on_event (EventType event, int data)

Called whenever certain game events occur. The value of DATA depends
on which event has occurred. The possible values of event are:

    eEventEnterRoomBeforeFadein
          called just before the room's 'Player Enters Room' event occurs
          DATA = new room number
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

---

### `on_key_press`

    on_key_press (eKeyCode keycode)

Called whenever a key is pressed on the keyboard. KEYCODE holds the
ASCII value of the key. A list of these values is [available here](ASCIIcodes).

The `on_key_press` function can also be defined in individual room
scripts. This allows the room script to intercept a key-press first,
and then decide whether to pass it on to the global script or not. See
the [ClaimEvent](Globalfunctions_General#claimevent) function for more
details.

---

### `on_mouse_click`

    on_mouse_click (MouseButton button)

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
the [ClaimEvent](Globalfunctions_General#claimevent) function for
more details.

---

### `repeatedly_execute`

    repeatedly_execute()

Called every game cycle (normally 40 times per second). Additional
information is [available here](RepExec).

---

### `repeatedly_execute_always`

    repeatedly_execute_always()

Called every game cycle, even when a blocking routine (e.g speech or
cutscene) is in progress. You **cannot** call any blocking functions
from this event handler. `repeatedly_execute_always` is called
**before** the game entities (characters, rooms, etc) get updated.
Additional information is [available here](RepExec).

---

### `late_repeatedly_execute_always`

    late_repeatedly_execute_always()

Called every game cycle, even when a blocking routine (e.g. speech or
cutscene) is in progress. You **cannot** call any blocking functions
from this event handler. `late_repeatedly_execute_always` is called
**after** the game entities (characters, rooms, etc) have been
updated, but before the game screen is redrawn.

---

### `unhandled_event`

    unhandled_event (int what, int type)

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
