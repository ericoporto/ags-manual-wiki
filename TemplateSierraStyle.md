## Sierra-style template

This template was previously listed as the 'default' template, with the majority
of functions used being native to the engine itself. i.e. there is no separate
script file to implement any additional behavior for the mouse cursor. This
makes it a good choice for learning how AGS works, since it makes heavy use of
the [mouse cursor functions](Mouse).

As a general guide, right clicking changes your cursor mode, left clicking uses
the current cursor mode.

This template also contains the majority of examples for save game and option
handling, and also demonstrates the default handling for an inventory window.

One script module is included, which allows the main character to be controlled
with the keyboard. This is switched on and configured with some default
settings, but can be reconfigured or switched off entirely by using the defined
functions.

Example:

```ags
// configure the player for arcade action
KeyboardMovement.Mode = eKeyboardMovementModePressing;
KeyboardMovement.KeyUp = eKeyW;
KeyboardMovement.KeyDown = eKeyS;
KeyboardMovement.KeyLeft = eKeyA;
KeyboardMovement.KeyRight = eKeyD;
```

---

### `KeyboardMovement.Mode`

```ags
KeyboardMovementMode KeyboardMovement.Mode
```

Sets the keyboard movement mode. Possible values are:

`eKeyboardMovementModeNone` (disable keyboard control)<br>
`eKeyboardMovementModeTapping` (tap a direction to move)<br>
`eKeyboardMovementModePressing` (hold down a direction to move)

---

### `KeyboardMovement.KeyUp`

```ags
eKeyCode KeyboardMovement.KeyUp
```

Assigns the key used to move the player upwards.

---

### `KeyboardMovement.KeyDown`

```ags
eKeyCode KeyboardMovement.KeyDown
```

Assigns the key used to move the player downwards.

---

### `KeyboardMovement.KeyLeft`

```ags
eKeyCode KeyboardMovement.KeyLeft
```

Assigns the key used to move the player to the left.

---

### `KeyboardMovement.KeyRight`

```ags
eKeyCode KeyboardMovement.KeyRight
```

Assigns the key used to move the player to the right.


*See also*: [Templates](Templates), [Setting up the game](Settingupthegame)
