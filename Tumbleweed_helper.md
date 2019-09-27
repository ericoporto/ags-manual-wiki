## Math and Helper Functions

---

### Verbs.Distance

```
float Verbs.Distance(int x1, int y1, int x2, int y2);
```

Returns the distance between two coordinates

---

### Verbs.Offset

```
int Verbs.Offset(int point1, int point2);
```

Returns the offset between to two given values.

---

### Verbs.GetButtonAction

```
int Verbs.GetButtonAction(int action);
```

Returns the connected action of a verb button. The actions for the verb buttons are not "hard-wired" inside the GUI-script, but defined in the function SetButtonAction.

*See also:*
[Verbs.SetActionButtons](Tumbleweed_actions#verbssetactionbuttons),
[Verbs.AdjustLanguage](Tumbleweed_translation#verbsadjustlanguage)

---

### Verbs.DisableGui

```
void Verbs.DisableGui();
```

This functions disables the GUI and hides it.

*See also:*
[Verbs.IsGuiDisabled](Tumbleweed_helper#verbsisguidisabled),
[Verbs.EnableGui](Tumbleweed_helper#verbsenablegui)

---

### Verbs.EnableGui

```
void Verbs.EnableGui();
```

This function enables the GUI again.

*See also:*
[Verbs.IsGuiDisabled](Tumbleweed_helper#verbsisguidisabled),
[Verbs.DisableGui](Tumbleweed_helper#verbsdisablegui)

---

### Verbs.IsGuiDisabled

```
bool Verbs.IsGuiDisabled();
```

Returns true, if the GUI is currently disabled, false otherwise

*See also:*
[Verbs.DisableGui](Tumbleweed_helper#verbsdisablegui)

---

### Verbs.GlobalCondition

```
int Verbs.GlobalCondition(int parameter);
```

Used to check for conditions that are used many times in the script. For example, it's used to check, if the mouse cursor is in the inventory and the mode walk or pickup are selected.
Returns 1, if the condition is true and 0 otherwise.

---

### Verbs.InitGuiLanguage

```
void Verbs.InitGuiLanguage();
```

This is a helper function to set the correct sprites for the verb GUI.

---

### Verbs.SetDoubleClickSpeed

```
void Verbs.SetDoubleClickSpeed(int speed)
```

Defines the double click speed

---

### Verbs.HandleInvArrows

```
void Verbs.HandleInvArrows()
```

Takes care of showing or hiding the inventory scroll sprites.
