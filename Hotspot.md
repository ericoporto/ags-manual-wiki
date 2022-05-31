## `Hotspot` functions and properties

### `Hotspot.GetAtRoomXY`

    static Hotspot* Hotspot.GetAtRoomXY(int x, int y)

Returns the hotspot at ROOM co-ordinates (X,Y). If there is no hotspot
there, or if invalid co-ordinates are specified, the Hotspot\*
representing hotspot 0 will be returned.

Example:

    if (Hotspot.GetAtRoomXY(player.x, player.y) == hPressurePlate) {
      Display("As soon as adventurer stands on the pressure plate the door opens.");
    }

will display the message if the player character is over the hPressurePlate hotspot.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See also:* [`Hotspot.GetAtScreenXY`](Hotspot#hotspotgetatscreenxy),
[`Character.GetAtRoomXY`](Character#charactergetatroomxy),
[`Object.GetAtRoomXY`](Object#objectgetatroomxy),
[`Region.GetAtRoomXY`](Region#regiongetatroomxy),
[`Game.GetLocationName`](Game#gamegetlocationname), [`GetLocationType`](Globalfunctions_General#getlocationtype)

---

### `Hotspot.GetAtScreenXY`

*(Formerly known as global function `GetHotspotAt`, which is now
obsolete)*

    static Hotspot* Hotspot.GetAtScreenXY(int x, int y)

Returns the hotspot at SCREEN co-ordinates (X,Y). If there is no hotspot
there, or if invalid co-ordinates are specified, the Hotspot\*
representing hotspot 0 will be returned.

Example:

    if (Hotspot.GetAtScreenXY(mouse.x, mouse.y) == hDoor)
      Display("Mouse on the door");
    else if (Hotspot.GetAtScreenXY(mouse.x, mouse.y) != hotspot[0])
      Display("Mouse is on something (but not the door)!");
    else
      Display("Mouse not on a hotspot");

will display a message depending on what the mouse is on.

*See also:* [`Hotspot.GetAtRoomXY`](Hotspot#hotspotgetatroomxy), [`Character.GetAtScreenXY`](Character#charactergetatscreenxy), [`Object.GetAtScreenXY`](Object#objectgetatscreenxy), [`Region.GetAtScreenXY`](Region#regiongetatscreenxy), [`Game.GetLocationName`](Game#gamegetlocationname), [`GetLocationType`](Globalfunctions_General#getlocationtype)

---

### `Hotspot.GetDrawingSurface`

    static DrawingSurface* Hotspot.GetDrawingSurface()

Gets a drawing surface for the current room's 8-bit hotspot mask, which allows you to directly draw onto that mask. Note that this function is static and relates to all hotspots at once (not a particular hotspot), because all of them are painted on the same mask.

After calling this method, use the various [DrawingSurface functions](DrawingSurface) to modify the mask. Since this is a 8-bit mask, DrawingColor will match the hotspot's index. Color value 0 will refer to "no hotspot" (eraser), color value 1 to hotspot number 1, and so forth. Don't forget to call `Release()` on the surface when you are finished to update the room's state.

Any changes you make will only last until the player leaves the room, at which point they will be lost. If you need to make long-lasting changes, you can use this method in the Player Enters Room event, which will recreate these changes whenever player returns back.

Example:

    DrawingSurface *surface = Hotspot.GetDrawingSurface();
    surface.DrawingColor = 4;
    surface.DrawRectangle(50, 50, 100, 100);
    surface.Release();

will paint a rectangle for the hotspot 4.

*See also:* [`GetDrawingSurfaceForWalkbehind`](Globalfunctions_Room#getdrawingsurfaceforwalkbehind),
[`GetDrawingSurfaceForWalkableArea`](Globalfunctions_Room#getdrawingsurfaceforwalkablearea),
[`Region.GetDrawingSurface`](Region#regiongetdrawingsurface)

---

### `Hotspot.GetProperty`

*(Formerly known as `GetHotspotProperty`, which is now obsolete)*

    Hotspot.GetProperty(string property)

Returns the custom property setting of the PROPERTY for the hotspot.

This command works with Number properties (it returns the number), and
with Boolean properties (returns 1 if the box was checked, 0 if not).

Use the equivalent GetTextProperty function to get a text property.

Example:

    if (hotspot[1].GetProperty("Value") > 200)
      Display("Hotspot 1's value is over 200!");

will print the message if hotspot 1 has its "Value" property set to more
than 200.

*See also:* [`Hotspot.GetTextProperty`](Hotspot#hotspotgettextproperty)

---

### `Hotspot.GetTextProperty`

*(Formerly known as `GetHotspotPropertyText`, which is now obsolete)*<br>
*(Formerly known as `Hotspot.GetPropertyText`, which is now obsolete)*

    String Hotspot.GetTextProperty(string property)

Returns the custom property setting of the PROPERTY for the hotspot.

This command works with Text properties only. The property's text will
be returned from this function.

Use the equivalent GetProperty function to get a non-text property.

Example:

    String description = hotspot[2].GetTextProperty("Description");
    Display("Hotspot 2's description: %s", description);

will retrieve hotspot 2's "description" property and display it.

*See also:* [`Hotspot.GetProperty`](Hotspot#hotspotgetproperty)

---

### `Hotspot.SetProperty`

    bool Hotspot.SetProperty(const string property, int value)

Sets the new *value* for the custom *property* for the specified
hotspot. Returns TRUE if such property exists and FALSE on failure.

This command works with Number properties (it sets the numeric value),
and with Boolean properties (sets FALSE is value is equal to 0, or TRUE
otherwise).

Use the equivalent SetTextProperty function to set new text property
value.

Example:

    hDoor.SetProperty("LockDifficulty", 5);

will change Door hotspot's "LockDifficulty" custom property to 5.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See also:* [`Hotspot.SetTextProperty`](Hotspot#hotspotsettextproperty)

---

### `Hotspot.SetTextProperty`

    bool Hotspot.SetTextProperty(const string property, const string value)

Sets the new *value* text for the custom *property* for the specified
hotspot. Returns TRUE if such property exists and FALSE on failure.

This command works with Text properties only. The property's text will
be changed to new value.

Use the equivalent SetProperty function to set a non-text property.

Example:

    hDoor.SetTextProperty("Description", "The sturdy door");

will change Door's "description" property.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See also:* [`Hotspot.SetProperty`](Hotspot#hotspotsetproperty)

---

### `Hotspot.IsInteractionAvailable`

    Hotspot.IsInteractionAvailable(CursorMode)

Checks whether there is an event handler defined for activating the
hotspot in cursor mode MODE.

This function is very similar to RunInteraction, except that rather than
run the event handler script function, it simply returns *true* if
something would have happened, or *false* if unhandled_event would have
been run.

Example:

    if (hTable.IsInteractionAvailable(eModeLookat) == 0)
      Display("looking on this table would not do anything.");

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See also:* [`IsInteractionAvailable`](Globalfunctions_General#isinteractionavailable),
[`Hotspot.RunInteraction`](Hotspot#hotspotruninteraction)

---

### `Hotspot.RunInteraction`

*(Formerly known as `RunHotspotInteraction`, which is now obsolete)*

    Hotspot.RunInteraction(CursorMode)

Processes the event handler as if the player had clicked the mouse on
the hotspot using the specified cursor mode.

Example:

    hDoor.RunInteraction(eModeLookat);

will run the code defined in the "LOOK AT HOTSPOT" event for hotspot
hDoor.

*See also:* [`Room.ProcessClick`](Room#roomprocessclick),
[`Hotspot.IsInteractionAvailable`](Hotspot#hotspotisinteractionavailable),
[`Character.RunInteraction`](Character#characterruninteraction),
[`Object.RunInteraction`](Object#objectruninteraction)

---

### `Hotspot.Enabled`

*(Formerly known as `DisableHotspot`, which is now obsolete)*<br>
*(Formerly known as `EnableHotspot`, which is now obsolete)*

    bool Hotspot.Enabled

Enables/disables the specified hotspot. If you set this to false, then
all areas of the screen that were previously made up of the hotspot now
act as type 0 (no hotspot). You can turn the hotspot back on later by
setting this back to true.

This setting is persisted in-game; that is, it will not be reset when
the player re-enters the room.

The default value of this property is always *true*.

Example:

    hBrownTree.Enabled = false;

will disable the hBrownTree hotspot.

*See also:* [`Region.Enabled`](Region#regionenabled),
[`RemoveWalkableArea`](Globalfunctions_Room#removewalkablearea),
[`RestoreWalkableArea`](Globalfunctions_Room#restorewalkablearea)

---

### `Hotspot.ID`

    readonly int Hotspot.ID

Gets the hotspot number of this hotspot. This allows you to interoperate
with old script using the number-based hotspot functions.

Example:

    Display("Hotspot hDoor is hotspot number %d.", hDoor.ID);
    Display("Hotspot 3 is number %d.", hotspot[3].ID);

displays hDoor's hotspot number, and then displays hotspot 3's number
(which will be 3).

*See also:* [`Hotspot.GetAtScreenXY`](Hotspot#hotspotgetatscreenxy)

---

### `Hotspot.Name`

*(Formerly known as `GetHotspotName`, which is now obsolete)*<br>
*(Formerly known as `Hotspot.GetName`, which is now obsolete)*

    readonly String Hotspot.Name;

Gets the name of the hotspot.

This property is read-only; it is currently not possible to change
hotspot names at run-time.

Example:

    Display("Hotspot 3's name is %s.", hotspot[3].Name);

will retrieve and then display hotspot 3's name.

*See also:* [`Game.GetLocationName`](Game#gamegetlocationname)

---

### `Hotspot.WalkToX`

*(Formerly known as `GetHotspotPointX`, which is now obsolete)*

    readonly int Hotspot.WalkToX

Gets the X room co-ordinate of the hotspot's walk-to point. If the
hotspot does not have a walk-to point, returns -1.

Example:

    player.Walk(hTable.WalkToX, hTable.WalkToY, eBlock, eWalkableAreas);

will move the character to hotspot hTable's walk-to point.

*See also:* [`Hotspot.WalkToY`](Hotspot#hotspotwalktoy),
[`MoveCharacterToHotspot`](Globalfunctions_General#movecharactertohotspot)

---

### `Hotspot.WalkToY`

*(Formerly known as `GetHotspotPointY`, which is now obsolete)*

    readonly int Hotspot.WalkToY

Gets the Y room co-ordinate of the hotspot's walk-to point. If the
hotspot does not have a walk-to point, returns -1.

Example:

    player.Walk(hTable.WalkToX, hTable.WalkToY, eBlock, eWalkableAreas);

will move the character to hotspot hTable's walk-to point.

*See also:* [`Hotspot.WalkToX`](Hotspot#hotspotwalktox),
[`MoveCharacterToHotspot`](Globalfunctions_General#movecharactertohotspot)
