## Tumbleweed Action Functions

These functions are mainly used to control the verb buttons.

---

### Verbs.UsedAction

```
void Verbs.UsedAction (Action test_action);
```

Used to determine, which action has been selected by the player. Instead of checking cursor modes, this function is used.

---

### Verbs.IsAction

```
bool Verbs.IsAction(Action test_action);
```

Used to check, if the current action is the one, given in the parameter.

---

### Verbs.SetActionButtons

```
void Verbs.SetActionButtons(Action action, int btn_ID, int sprite, int sprite_highlight, char key);
```

This functions connects the verb buttons with the action and is also used to assign / change the graphics of the verb buttons.

*See also:*
[Verbs.AdjustLanguage](Tumbleweed_translation#verbsadjustlanguage)

---

### Verbs.SetDefaultAction

```
void Verbs.SetDefaultAction(Action def_action);
```

Used to define, which action is being used, if no verb has been clicked. Usually this is "walk to".

---

### Verbs.SetAction

```
void Verbs.SetAction(Action new_action);
```

Since the cursor modes are bypassed, this function defines the current action. Among other things, this function is called by clicking a verb button.

---

### Verbs.SetAlternativeAction

```
void Verbs.SetAlternativeAction(char extension, Action alt_action);
```

This function makes the right-click shortcuts work. If you use extensions like ">p" (e.g. pickup), this function makes sure, that the correct verb button is highlighted.

*See also:*
[Verbs.CheckDefaultAction](Tumbleweed_actions#verbscheckdefaultaction)

---

### Verbs.CheckDefaultAction

```
void CheckDefaultAction();
```

This function checks for a given extension in hotspots, objects and characters. If there isn't an extension, a default action is given, e.g.
"Talk to" if the mouse is over a character. In case of a given extension, the default actions are being overridden.
It is also defined here, which letters are causing what default action. See the chapter Extensions for more details.

*See also:*
[Extensions](Tumbleweed_extensions#tumbleweed-extensions)

---

### Verbs.UpdateActionBar

```
void UpdateActionBar();
```

This function is used to show and update the status bar. It checks for an extension, triggers the translation and renders the results on screen.

*See also:*
[Verbs.TranslateAction](Tumbleweed_translation#verbstranslateaction),
[Verbs.RemoveExtension](Tumbleweed_extensions#verbsremoveextension)

---

### Verbs.ToogleGuiStyle

```
void ToogleGuiStyle(int enable_new);
```

Switches between classic SCUMM mode and new one.
