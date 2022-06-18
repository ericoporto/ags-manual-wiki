## Cursor Editor

The Cursors node of the editor shows you the current mouse cursor modes available in the game. Each cursor mode performs a different action within the game. There's always a number of precreated cursors, which editor won't allow to remove, and you also may create more if necessary. Right clicking on the "Cursors" node itself allows you to create a new custom cursor. Creating a new cursor or double clicking an existing one will open it for edit.

The Cursor editor pane allows to preview the cursor's graphic, set its "hotspot" (the point on the cursor's graphic which triggers interaction with underlying objects), as well as configure other properties.

The "StandardMode" option in the property grid tells AGS that this is a "normal" cursor mode - i.e. using this cursor will fire an event on whatever is clicked on as usual. This mode applies to the standard Walk, Look, Interact and Talk modes, but you can create others too. Do not tick it for the Use Inventory mode, since this is a special mode.

The "Animate" option allows you to specify that the mouse cursor will animate while it is on the screen. Choose a view number, and the cursor will animate using the first loop of that view. You can make it animate only when over something (hotspot, object or character) by enabling the "AnimateOnlyOnHotspots" option.

The "AnimateOnlyWhenMoving" box allows you to do a QFG4-style cursor, where it only animates while the player is moving it around.

Three of the cursor modes are hard-coded special meanings into AGS:
-   **Mode 4 (Use Inventory)**. This is special because the game decides
    whether to allow its use or not, depending on whether the player has
    an active inventory item selected.
-   **Mode 6 (Pointer)**. This cursor is used whenever a modal dialog is
    displayed (i.e. a GUI that pauses the game). Normally this is a
    standard arrow pointer.
-   **Mode 7 (Wait)**. This cursor is used whenever the player cannot
    control the action, for example during a scripted cutscene. For a
    LucasArts-style game where the cursor disappears completely in this
    state, simply import a blank graphic over the wait cursor.

For the standard modes,
-   Mode 0 will cause the player to walk to the mouse pointer location
    when clicked.
-   Modes 1, 2, 3, 5, 8 and 9 will run the event with the same name as
    the cursor mode.