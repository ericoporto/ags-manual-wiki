## Dialog Editor

In AGS conversations between characters are done using Dialogs or "dialog topics" (not to be confused with GUI dialogs).

On the Explore Project panel, you can expand the Dialogs node to show the dialogs which are created in your game. Right clicking on the "Dialogs" node itself allows you to create a new dialog, or create a folder to help you organize them.

When creating a new dialog, or double-clicking on existing dialog within the tree, a new editor panel will open.

The dialog editor consists of two parts: the list of options and dialog script window. At the options list use "Create new option" and "Delete last option" buttons to make as many options for this dialog topic as you need. The "Option text" field represents an option's name that will be displayed in game. "Show" checkbox to the right determines whether the option is enabled on start, while "Say" checkbox determines whether the option's text will be said by the player's character when chosen in game.

**NOTE:** The options may be enabled or disabled at runtime in script using both [special dialog script's syntax](DialogScript) (`option-on`, `option-off`, `option-off-forever`) or regular script command [`Dialog.SetOptionState`](Dialog#dialogsetoptionstate).

The dialog script window is where you can write the actual conversation script, would that be what characters say, or performing any other actions. This script consists of parts each starting with a `@` label. The `@S` label defines a dialog's entry point, this part will be executed immediately as a dialog starts and before any options were shown. For each existing option there's a `@X` label, where X is a option's number. These define "jump points", and this is where the script will continue to execute whenever corresponding option is chosen. Thus you may think of options as of "table of contents" for this conversation.

Please refer to the [Dialog Script](DialogScript) topic for more detailed information on how to write dialog scripts.

**NOTE:** conversation lines from the dialog script are played in game using standard [`Character.Say`](Character#charactersay) command by default. If you prefer to script your custom speech system in your game, you may tell the dialog system to use your own script function instead. Go to [General Settings](GeneralSettings#dialog) and look for the "Custom Say function in dialog scripts" option.
