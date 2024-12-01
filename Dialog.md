## `Dialog` functions and properties

### `Dialog.GetByName`

```ags
static Dialog* Dialog.GetByName(string scriptName)
```

Returns a pointer to the Dialog with the specified script name, or null if it does not exist.

Normally you do not need to use this, as there will be a automatically created global script variable for each Dialog which got a script name.
Where GetByName() function may come useful is situation in which you a) do not know exact name, b) had to store object's reference in a string for some reason. Good examples of this are saving object's name in a [custom property](CustomProperties), or a [file](File), then reading it back.

Example:

```ags
String dialogName = cNPC.GetTextProperty("MyDialog");
Dialog* dlg = Dialog.GetByName(dialogName);
if (dlg != null) {
    dlg.Start();
}
```

Retrieves a dialog name from the character's custom property, and gets a pointer to an actual Dialog using that name, then runs it.

*Compatibility:* Supported by **AGS 3.6.1** and later versions.

*See also:* [`Dialog.ScriptName`](Dialog#dialogscriptname), [`Dialog.Start`](Dialog#dialogstart)

---

### `Dialog.AreOptionsDisplayed`

```ags
static readonly attribute bool Dialog.AreOptionsDisplayed
```

Returns `true` if dialog options are currently displayed on the screen, or false otherwise.

Example:

```ags
bool _previousOptionsDisplayed;

void repeatedly_execute_always()
{
    if (Dialog.AreOptionsDisplayed && !_previousOptionsDisplayed)
    {
        System.Log(eLogInfo, "Dialog options are currently displayed.");
    }
    else if(!Dialog.AreOptionsDisplayed && _previousOptionsDisplayed)
    {
        System.Log(eLogInfo, "No dialog options are visible right now.");
    }
    _previousOptionsDisplayed = Dialog.AreOptionsDisplayed;
}
```

In this example, whenever there is a transition from options being displayed or them not being displayed, it logs the new state of dialog options being shown.

**Compatibility:** Supported by **AGS 3.6.2** and later versions.

**See also:** [`Dialog.DisplayOptions`](Dialog#dialogdisplayoptions), [`Dialog.Start`](Dialog#dialogstart)
```

---

### `Dialog.CurrentDialog`

```ags
static readonly attribute Dialog* Dialog.CurrentDialog
```

Gets the currently running dialog. Returns `null` if no dialog is currently active.

**NOTE:** in dialog is a specific state of the AGS Engine, it means a dialog script created in the editor is being ran. It's not the same as any character speaking.
You can use `Speech.TextOverlay` to detect if any character is speaking and then check each character's Speaking property if you need to know which character is speaking.

Example:

```ags
void repeatedly_execute_always()
{
    if (Dialog.CurrentDialog != null)
    {
        // a dialog is running, show our custom frames
        gDialogBorders.Visible = true;
    }
    else
    {
        // there is no dialog, let's hide our custom frames
        gDialogBorders.Visible = false;
    }
}
```

In this example, the script checks whether a dialog is active, and show or hide a GUI that contains decorative frames.

*Compatibility:* Supported by **AGS 3.6.2** and later versions.

**See also:** [`Dialog.Start`](Dialog#dialogstart),
[`Speech.TextOverlay`](Speech#speechtextoverlay),
[`Character.Speaking`](Character#characterspeaking)

---

### `Dialog.ExecutedOption`

```ags
static readonly attribute int Dialog.ExecutedOption
```

Gets the currently executed dialog option, or `-1` if none is being executed.

Example:

```ags
void repeatedly_execute_always()
{
    if (Dialog.ExecutedOption != -1)
    {
        System.Log(eLogInfo, "Currently executed dialog option: %d", Dialog.ExecutedOption);
    }
}
```

This example checks if a dialog option is being executed and logs its number.

*Compatibility:* Supported by **AGS 3.6.2** and later versions.

**See also:** [`Dialog.GetOptionText`](Dialog#dialoggetoptiontext), 
[`Dialog.GetOptionState`](Dialog#dialoggetoptionstate)

---

### `Dialog.DisplayOptions`

```ags
int Dialog.DisplayOptions(optional DialogOptionSayStyle)
```

Presents the options for this dialog to the user and waits until they
select one of them. The selected option number is returned.

**NOTE:** This command does not run any dialog scripts, it simply
displays the options and waits for the player to choose one. To run the
dialog normally, use the [`Dialog.Start`](Dialog#dialogstart) command
instead.

This command is useful if you want to implement your own dialog system,
but still use the standard AGS dialog option selection screens.

The optional *DialogOptionSayStyle* parameter determines whether the
chosen option is automatically spoken by the player character. The
default is *eSayUseOptionSetting*, which will use the option's "Say"
setting from the dialog editor. You can alternatively use *eSayAlways*,
which will speak the chosen option regardless of its setting in the
editor; or *eSayNever*, which will not speak the chosen option.

If the text parser is enabled for this dialog and the player types
something into it rather than selecting an option, the special value
`DIALOG_PARSER_SELECTED` will be returned, and AGS will have
automatically called [`Parser.ParseText`](Parser#parserparsetext) with
the player's text. Therefore, you can call
[`Parser.Said`](Parser#parsersaid) to process it.

Example:

```ags
int result = dOldMan.DisplayOptions();
if (result == DIALOG_PARSER_SELECTED)
{
    Display("They typed something into the parser!!");
}
else
{
    Display("They chose dialog option %d.", result);
}
```

will show the options for dialog *dOldMan* and display a message
depending on what the player selected.

*Compatibility:* Supported by **AGS 3.0.2** and later versions.

*See also:* [`Dialog.Start`](Dialog#dialogstart),
[`Parser.ParseText`](Parser#parserparsetext)

---

### `Dialog.GetOptionState`

*(Formerly known as global function `GetDialogOption`, which is now
obsolete)*

```ags
Dialog.GetOptionState(int option)
```

Finds out whether an option in a conversation is available to the player
or not.

OPTION is the option number within the dialog, from 1 to whatever the
highest option is for that topic.

The return value can have the following values:

    eOptionOff
      The option is disabled - the player will not see it
    eOptionOn
      The option is enabled - the player can now see and use it
    eOptionOffForever
      The option is permanently disabled - no other command can ever turn
      it back on again.

These are the same as the options passed to Dialog.SetOptionState.

Example:

```ags
if (dJoeExcited.GetOptionState(2) != eOptionOn)
    Display("It's turned off");
```

Will display a message if option 2 of dialog dJoeExcited is not
currently switched on.

*See also:*
[`Dialog.HasOptionBeenChosen`](Dialog#dialoghasoptionbeenchosen),
[`Dialog.SetHasOptionBeenChosen`](Dialog#dialogsethasoptionbeenchosen),
[`Dialog.SetOptionState`](Dialog#dialogsetoptionstate)

---

### `Dialog.GetOptionText`

```ags
String Dialog.GetOptionText(int option)
```

Returns the text for the specified dialog option.

OPTION is the option number within the dialog, from 1 to whatever the
highest option is for that topic.

Example:

```ags
String optionText = dJoeBloggs.GetOptionText(3);
Display("Option 3 of dialog dJoeBloggs is %s!", optionText);
```

will display the text for the third option of the dJoeBloggs dialog.

*Compatibility:* Supported by **AGS 3.0.2** and later versions.

*See also:* [`Dialog.OptionCount`](Dialog#dialogoptioncount),
[`Dialog.GetOptionState`](Dialog#dialoggetoptionstate)

---

### `Dialog.HasOptionBeenChosen`

```ags
bool Dialog.HasOptionBeenChosen(int option)
```

Finds out whether the player has already chosen the specified option in
this dialog. This is mainly useful when drawing your own custom dialog
options display, since it allows you to differentiate options that have
already been chosen.

OPTION is the option number within the dialog, from 1 to whatever the
highest option is for that topic.

Example:

```ags
if (dJoeExcited.HasOptionBeenChosen(2))
    Display("The player has chosen option 2 in dialog dJoeExcited!");
```

will display a message if the player has used option 2 of the dialog
before.

*Compatibility:* Supported by **AGS 3.1.1** and later versions.

*See also:* [`Dialog.GetOptionState`](Dialog#dialoggetoptionstate),
[`Dialog.SetHasOptionBeenChosen`](Dialog#dialogsethasoptionbeenchosen),

---

### `Dialog.ID`

```ags
readonly int Dialog.ID;
```

Gets the dialog ID number from the editor.

This might be useful if you need to interoperate with legacy scripts
that work with dialog ID numbers.

Example:

```ags
Display("dFisherman is Dialog %d!", dFisherman.ID);
```

will display the ID number of the dFisherman dialog

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

---

### `Dialog.OptionCount`

```ags
readonly int Dialog.OptionCount;
```

Gets the number of options that this dialog has.

This might be useful in a script module if you want to iterate through
all the possible choices in the dialog.

Example:

```ags
Display("dFisherman has %d options!", dFisherman.OptionCount);
```

will display the number of options in the dFisherman dialog.

*Compatibility:* Supported by **AGS 3.0.2** and later versions.

*See also:* [`Dialog.GetOptionText`](Dialog#dialoggetoptiontext),
[`Dialog.GetOptionState`](Dialog#dialoggetoptionstate)

---

### `Dialog.ScriptName`

```ags
readonly String Dialog.ScriptName;
```

Gets the script name of the dialog, which serves as a unique identifier.

This may be useful if you have a pointer to some dialog stored in your variable, and want to know what it actually is. Normally you don't need a script name, as you have an automatic global variable for each dialog in the game, but sometimes you may want to save its script name as a text either to display it somewhere for testing purposes, or keep as a reference. You may later use [Dialog.GetByName](Dialog#dialoggetbyname) function to retrieve the dialog by the previously saved script name.

Example:

```ags
function CustomDialogStart(this Dialog*)
{
  this.Start();
  String dialogName = this.ScriptName;
  System.Log(eLogInfo, "Starting dialog: %s", dialogName);
}
```

Starting a dialog using the `CustomDialogStart()` method, like `dExampleDialog.CustomDialogStart()`, will log its script name for debugging purposes.

*Compatibility:* Supported by **AGS 3.6.1** and later versions.

*See also:* [`Dialog.GetByName`](Dialog#dialoggetbyname), [`Dialog.Start`](Dialog#dialogstart)

---

### `Dialog.SetHasOptionBeenChosen`

```ags
Dialog.SetHasOptionBeenChosen(int option, bool chosen)
```

Changes whether an option in a conversation is marked as previously
chosen by the player. The option is marked as chosen whenever player
selects it during the conversation, and is usually highlighted with
different text color. This function lets you to reset the option state,
or force it change at any random moment.

OPTION is the option number within the dialog, from 1 to whatever the
highest option is for that topic.

Example:

```ags
if (dDialog1.HasOptionBeenChosen(1))
    dDialog1.SetHasOptionBeenChosen(1, false); // reset the option state
```

will mark option 1 of dialog dDialog1 as "not chosen yet".

*Compatibility:* Supported by **AGS 3.3.0** and later versions.

*See also:* [`Dialog.GetOptionState`](Dialog#dialoggetoptionstate),
[`Dialog.HasOptionBeenChosen`](Dialog#dialoghasoptionbeenchosen)

---

### `Dialog.SetOptionState`

*(Formerly known as global function `SetDialogOption`, which is now
obsolete)*

```ags
Dialog.SetOptionState(int option, DialogOptionState)
```

Changes whether an option in a conversation is available to the player
or not. This allows you to add extra options to a conversation once the
player has done certain things.

OPTION is the option number within the topic, from 1 to whatever the
highest option is for that topic.

The DialogOptionState controls what happens to this option. It can have
the following values:

    eOptionOff
      The option is disabled - the player will not see it
    eOptionOn
      The option is enabled - the player can now see and use it
    eOptionOffForever
      The option is permanently disabled - no other command can ever turn
      it back on again.

These are equivalent to the option-off, option-on, and
option-off-forever dialog commands.

Example:

```ags
dFriend1.SetOptionState(2, eOptionOn);
```

will enable option 2 of topic number 4.

*See also:* [`Dialog.GetOptionState`](Dialog#dialoggetoptionstate),
[`Dialog.Start`](Dialog#dialogstart),
[`StopDialog`](Dialog#stopdialog)

---

### `Dialog.ShowTextParser`

```ags
readonly bool Dialog.ShowTextParser;
```

Gets whether this dialog shows a text box allowing the player to type in
text.

This property is initially set in the Dialog Editor.

Example:

```ags
if (dFisherman.ShowTextParser)
{
    Display("dFisherman has a text box!");
}
```

will display a message if dFisherman has the option enabled

*Compatibility:* Supported by **AGS 3.2.1** and later versions.

---

### `Dialog.Start`

*(Formerly known as global function `RunDialog`, which is now obsolete)*

```ags
Dialog.Start()
```

Starts a conversation from the specified topic.

NOTE: The conversation will not start immediately; instead, it will be
run when the current script function finishes executing.

If you use this command from within the dialog_request function, it
will specify that the game should return to this new topic when the
script finishes.

Example:

```ags
dMerchant.Start();
```

will start the conversation topic named dMerchant.

*See also:* [`Dialog.DisplayOptions`](Dialog#dialogdisplayoptions),
[`Dialog.SetOptionState`](Dialog#dialogsetoptionstate)

---

### `StopDialog`

```ags
StopDialog ()
```

This command can only be used from within the dialog_request function.
It tells AGS that when dialog_request finishes, the whole conversation
should stop rather than continuing with the dialog script.

You can use this function to end the conversation depending on whether
the player has/does a certain thing.

Example:

```ags
function dialog_request (int dr) {
    if (dr==1) {
        cEgo.AddInventory(iPoster);
        StopDialog();
    }
}
```

will give the player the inventory item 3 and then end the conversation.

*See also:* [`Dialog.SetOptionState`](Dialog#dialogsetoptionstate)

