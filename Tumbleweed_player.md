## Tumbleweed Player functions

---

### `Verbs.FreezePlayer`

```ags
vpod Verbs.FreezePlayer();
```

Use this function to prevent the player from moving by the following movement functions of the template.

*See also:*
[`Verbs.UnfreezePlayer`](Tumbleweed_player#verbsunfreezeplayer)

---

### `Verbs.UnfreezePlayer`

```ags
void Verbs.UnfreezePlayer();
```

Use this function to undo the FreezePlayer function and let the characters move again.

*See also:*
[`Verbs.FreezePlayer`](Tumbleweed_player#verbsfreezeplayer)

---

### `Verbs.SetPlayer`

```ags
void SetPlayer(Character*ch);
```

Usage:

```ags
cEgo.SetPlayer();
```

Similar to the AGS function Character.SetAsPlayer(). The difference is, that make the previous character clickable again, whereas the new character gets unclickable.

---

### `Verbs.EnterRoom`

```ags
void EnterRoom(this Character*, int newRoom, int x, int y, eDirection dir, bool onWalkable);
```

Usage:

```ags
cEgo.EnterRoom(1,15,15,eDir_Left,true);
```

Similar to the AGS function Character.ChangeRoom. The difference is, that you can also define, it which direction the character should look.
Using this function makes the character turn to the direction, mentioned above.
