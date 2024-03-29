## Tumbleweed Semi-blocking movement functions

Semi-blocking means, that you can cancel the movement, but certain code is only executed, after the character has actually reached it's goal.
To archive this, these functions are called inside an if-clause.

Example:

```ags
if(Verbs.MovePlayer(20,20)) Display("The player has reached the destination.");
```

If the player's character reaches the coordinates 20,20, the message "I'm there" is being displayed.
If the movement is being canceled by a mouseclick, the message doesn't appear.

---

### `Verbs.MovePlayer`

```ags
int Verbs.MovePlayer(int x, int y);
```

Moves the player character around on walkable areas, a wrapper for MovePlayerEx.
Returns 1, if the character has reached it's goal and 0 if the movement has been canceled before.

*See also:*
[`Verbs.MovePlayerEx`](Tumbleweed_movement#verbsmoveplayerex)

### `Verbs.MovePlayerEx`

```ags
int Verbs.MovePlayerEx(int x, int y, WalkWhere direct);
```

Move the player character to x,y coordinates, waiting until he/she gets there, but allowing to cancel the action by pressing a mouse button.
Returns 1, if the character hasn't canceled the movement and 0 if the movement has been canceled before.
2 is returned, if the characters has actually reached it's goal: e.g. if a walkable area is being removed while the player is still moving.

---

### `Verbs.GoToCharacter`

```ags
int Verbs.GoToCharacter(Character*charid, eDirection dir, bool NPCfacesplayer, int blocking);
```

The same as GoToCharacterEx, just with the one character being the player and a default offset of x=35px and y=20px.
Returns 1, if the character has reached it's goal and 0 if the movement has been canceled before.

*See also:*
[`Verbs.GoToCharacterEx`](Tumbleweed_movement#verbsgotocharacterex)

---

### `Verbs.GoToCharacterEx`

```ags
int Verbs.GoToCharacterEx(Character*chwhogoes, Character*ch, eDirection dir, int xoffset, int yoffset, bool NPCfacesplayer, int blocking);
```

Goes to a character staying at the side defined by 'direction': 1 up, 2 right, 3 down, 4 left and it stays at xoffset or yoffset from the character.
blocking: 0=non-blocking; 1=blocking; 2=semi-blocking
Returns 1, if the character has reached it's goal and 0 if the movement has been canceled before.

*See also:*
[`Verbs.GoToCharacter`](Tumbleweed_movement#verbsgotocharacter),
[`Verbs.NPCGoToCharacter`](Tumbleweed_movement#verbsnpcgotocharacter)

---

### `Verbs.NPCGoToCharacter`

```ags
int Verbs.NPCGoToCharacter(Character*charidwhogoes, Character*charidtogoto, eDirection dir, bool NPCfacesplayer, int blocking);
```

The same as GoToCharacterEx, just with an default offset of x=35 and y=20
Returns 1, if the character has reached it's goal and 0 if the movement has been canceled before.

*See also:*
[`Verbs.GoToCharacterEx`](Tumbleweed_movement#verbsgotocharacterex)

---

### `Verbs.AnyClickMove`

```ags
int Verbs.AnyClickMove(int x, int y, eDirection dir);
```

Moves the player character to the coordinates given in the parameters. If the player reaches the destination, it's turns to the given direction.
Returns 1, if the character has reached it's goal and 0 if the movement has been canceled before.
You can use this kind of functions (including the movePlayer function which is called by this function),
to check if the player actually reached it's destination. For example:

```ags
if (Verbs.AnyClickMove(130,110,eDir_Left) == 1 ) player.Say("I've reached the place.");
```

So the Message is only displayed, if the movement hasn't been canceled.

*See also:*
[`Verbs.MovePlayer`](Tumbleweed_movement#verbsmoveplayer),
[`Verbs.MovePlayerEx`](Tumbleweed_movement#verbsmoveplayerex)

---

### `Verbs.AnyClickWalk`

```ags
int Verbs.AnyClickWalk(int x, int y, eDirection dir);
```

This function is almost similar to AnyClickMove. But it's only called, if the current action is eGA_WalkTo.

*See also:*
[`Verbs.MovePlayer`](Tumbleweed_movement#verbsmoveplayer),
[`Verbs.MovePlayerEx`](Tumbleweed_movement#verbsmoveplayerex),
[`Verbs.AnyClickMove`](Tumbleweed_movement#verbsanyclickmove)

---

### `Verbs.AnyClickWalkLook`

```ags
int Verbs.AnyClickWalkLook(int x, int y, eDirection dir, String lookat);
```

This function moves the player character to the given location, turns it to the given direction and lets it say the message, given in the string.

*See also:*
[`Verbs.AnyClickWalk`](Tumbleweed_movement#verbsanyclickwalk)

---

### `Verbs.AnyClickWalkLookPick`

```ags
int Verbs.AnyClickWalkLookPick(int x, int y, eDirection dir, String lookat, int objectID, InventoryItem*item, AudioClip *sound);
```

This function starts the same as any_click_walk_look. If an object ID > 0 has been given, this object is set invisible. Afterwards the inventory item is going to be added to the player's inventory and if there's an audioclip in the parameters, that one is played too.

The function return 0 if the action has been canceled, before the player has reached the coordinates. 1 is returned if the player has reached the given destination, but has not picked up the item. 2 is returned, if the item has been picked up.

*See also:*
[`Verbs.AnyClickWalkLook`](Tumbleweed_movement#verbsanyclickwalklook),
[`Verbs.AnyClickWalk`](Tumbleweed_movement#verbsanyclickwalk)

---

### `Verbs.AnyClickUseInv`

```ags
int Verbs.AnyClickUseInv (InventoryItem*item, int x, int y, eDirection dir);
```

This function moves the player to the given destination. It returns 0, if the action is unhandled, 1 is returned,
if the action is handled, but has been canceled. 2 is returned, if everything went fine. A possible usage is:

```ags
if (Verbs.AnyClickUseInv(iWrench,100,130,eDir_Left) == 2 ) player.Say("I will now repair this pipe.");
```

*See also:*
[`Verbs.AnyClickWalkLook`](Tumbleweed_movement#verbsanyclickwalklook),
[`Verbs.AnyClickWalk`](Tumbleweed_movement#verbsanyclickwalk)

---

### `Verbs.GoTo`

```ags
int Verbs.GoTo(int blocking);
```

Go to whatever the player clicked on. This function is used to intercept a walk-to event and check if the player has reached it's goal.
E.g. this is used in the exit extension processing.
blocking: 0=non-blocking; 1=blocking; 2=semi-blocking (default)

*See also:*
[`Verbs.MovePlayer`](Tumbleweed_movement#verbsmoveplayer),
[`Verbs.WalkOffScreen`](Tumbleweed_movement#verbswalkoffscreen)

---

### `Verbs.WalkOffScreen`

```ags
void Verbs.WalkOffScreen();
```

Handles the action of hotspots or objects with the exit extension ('>e'). Take a look at chapter about extensions to see what this function does.

*See also:*
[Extensions](Tumbleweed_extensions#tumbleweed-extensions)

---

### `Verbs.SetApproachingChar`

```ags
void Verbs.SetApproachingChar(bool enable);
```

If set to true, the player walks to other chars before talking or giving items. This behavior is initially defined in the guiscript, this function is used to change it during runtime.
