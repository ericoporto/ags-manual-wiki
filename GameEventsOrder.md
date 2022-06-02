## Game events order

The game in AGS consists of "loops" which run repeatedly with certain speed (see [SetGameSpeed](Globalfunctions_General#setgamespeed)). On each loop it runs certain events and script callbacks, updates the game and redraws the game on screen.

The order of these actions within a single loop is consistent. When you start using AGS you probably won't care about that, but as you write more complex scripts, it may become important. This order may seem a bit strange in some parts, but it's a result of AGS development history.

Following is a sequence of actions which happen in a normal game loop:
* [`repeatedly_execute_always`](Globalfunctions_Event#repeatedly_execute_always) function is called (if found in script).
* *Main game update:* almost all in the game is updated: characters, room objects, and so forth.
* [`late_repeatedly_execute_always`](Globalfunctions_Event#late_repeatedly_execute_always) function is called (if found in script).
* Non-blocking screen shaking update (see [ShakeScreenBackground](Globalfunctions_Screen#shakescreenbackground)).
* Mouse position update.
* GUI updates, reacting to mouse state (movement and buttons).
* *Game is drawn on screen.*
* All the scheduled events are executed. Strictly speaking, the order of execution is undefined. Commonly [`repeatedly_execute`](Globalfunctions_Event#repeatedly_execute) goes first, but that's rather a coincidence and is not recommended to rely upon. Other events include: `on_key_press`, `on_mouse_click`, `on_event`, and so forth (see [their respective page](Globalfunctions_Event#global-event-handlers) for details).

