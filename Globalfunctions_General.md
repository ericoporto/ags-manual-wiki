## Global functions (general section)

### `AbortGame`

    AbortGame(string message, ...)

Aborts the game and returns to the operating system.

The standard AGS error dialog is displayed, with the script line numbers
and call stack, along with *message* (which can include `%d` and `%s`
Display-style tokens).

You can use this function rather than QuitGame if you are writing some
debugging checks into your script, to make sure that the user calls your
functions in the correct way.

This command should ideally never be called in the final release of a
game.

Example:

    function MakeWider(int newWidth) {
      if (newWidth < 10)
        AbortGame("newWidth expects a width of at least 10!");
    }

will abort the game if MakeWider is called with a parameter less than
10.

SeeAlso: [QuitGame](Globalfunctions_General#quitgame)

---

### `CallRoomScript`

    CallRoomScript (int value)

Calls the `on_call` function in the current room script. This is useful
for things like the text parser, where you want to check for general
game sentences, and then ask the current room if the sentence was
relevant to it.

The on_call function will be called in the current room script, with
its `value` parameter having the value you pass here. This allows it to
distinguish between different tasks, and saves you having to use a
GlobalInt to tell it what to do.

If the current room has no on_call function, nothing will happen. No
error will occur.

You write the on_call function into the room script (\"Edit script\"
button on Room Settings pane), similar to the way you do dialog_request
in the global script:

    function on_call (int value) {
      if (value == 1) {
        // Check text input
        if (Parser.Said("get apple"))
          Display("No, leave the tree alone.");
      }
    }

The function doesn't get called immediately; instead, the engine will
run it in due course, probably during the next game loop, so you can't
use any values set by it immediately.

Once the on_call function has executed (or not if there isn't one),
the game.roomscript_finished variable will be set to 1, so you can
check for that in your repeatedly_execute script if you need to do
something afterwards.

SeeAlso: [The text parser documentation](TextParser), [on_call](Globalfunctions_Event#on_call)

---

### `ClaimEvent`

    ClaimEvent()

This command is used in a room script or script module's
*on_key_press* or *on_mouse_click* function, and it tells AGS not to
run the global script afterwards.

For example, if your room script responds to the player pressing the
space bar, and you don't want the global script's on_key_press to
handle it as well, then use this command.

This is useful if you have for example a mini-game in the room, and you
want to use some keys for a different purpose to what they normally do.

The normal order in which scripts are called for *on_key_press* and
*on_mouse_click* is as follows:

-   room script
-   script modules, in order
-   global script

If any of these scripts calls ClaimEvent, then the chain is aborted at
that point.

Example:

    if (keycode == ' ') {
      Display("You pressed space in this room!");
      ClaimEvent();
    }

prevents the global script on_key_press from running if the player
pressed the space bar.

SeeAlso: [Script events](Globalfunctions_Event)

---

### `Debug`

    Debug (int command, int data)

This function provides all the debug services in the system. It performs
various different tasks, depending on the value of the COMMAND
parameter. If debug mode is off, then this function does nothing. This
allows you to leave your script unaltered when you distribute your game,
so you just have to turn off debug mode in the AGS Editor.

The DATA parameter depends on the command - pass 0 if it is not used.
All the valid values for the COMMAND parameter are listed below along
with what they do:

    0   All inventory - gives the current player character one of every
        inventory item. This is useful for testing so that you don't have to
        go and pick up items every time you test part of the game where they
        are required.
    1   Display interpreter version - the engine will display its version
        number and build date.
    2   Walkable from here - fills in the parts of the screen where the player
        can walk from their current location. This is useful if you think the
        path-finder is not working properly. All walkable areas are drawn in
        their respective colors, but with blocking areas at characters feet
        removed.
    3   Teleport - displays a dialog box asking for what room you want to go
        to, and then calls ChangeRoom to teleport you there. Useful for skipping
        parts of the game or going to a specific point to test something.
    4   Show FPS - toggles whether the current frames per second is displayed
        on the screen. Pass DATA as 1 to turn this on, 0 to turn it off.

*See Also:* [Debugging features](Debuggingfeatures),
[System.RuntimeInfo](System#systemruntimeinfo)

---

### `DeleteSaveSlot`

    DeleteSaveSlot (int slot)

Deletes the save game in save slot number SLOT.

NOTE: if you specify one of the standard slots (1-50), then AGS will
rearrange the other save games to make sure there is a sequence of slots
from 1 upwards. Therefore, you will need to refresh any save game lists
you have after calling this function.

Example:

    DeleteSaveSlot (130);

deletes save game slot 130 (which we should have saved earlier).

*See Also:* [RestoreGameSlot](Globalfunctions_General#restoregameslot),
[SaveGameSlot](Globalfunctions_General#savegameslot)

---

### `DisableInterface`

    DisableInterface ()

Disables the player interface. This works the same way as it is disabled
while an animation is running: the mouse cursor is changed to the Wait
cursor, and mouse clicks will not be sent through to the
\"on_mouse_click\" function. Also, all interface buttons will be
disabled.

**NOTE:** AGS keeps a count of the number of times DisableInterface is
called. Every call to DisableInterface must be matched by a later call
to EnableInterface, otherwise the interface will get permanently
disabled.

Example:

    DisableInterface();

will disable the user's interface.

*See Also:* [EnableInterface](Globalfunctions_General#enableinterface),
[IsInterfaceEnabled](Globalfunctions_General#isinterfaceenabled)

---

### `EnableInterface`

    EnableInterface ()

Re-enables the player interface, which was previously disabled with the
DisableInterface function. Everything which was disabled is returned to
normal.

Example:

    EnableInterface();

will enable the user's interface.

*See Also:* [DisableInterface](Globalfunctions_General#disableinterface),
[IsInterfaceEnabled](Globalfunctions_General#isinterfaceenabled)

---

### `EndCutscene`

    EndCutscene()

Marks the end of a cutscene. If the player skips the cutscene, the game
will fast-forward to this point. This function returns 0 if the player
watched the cutscene, or 1 if they skipped it.

*See Also:* [SkipCutscene](Globalfunctions_General#skipcutscene), [StartCutscene](Globalfunctions_General#startcutscene),
[Game.InSkippableCutscene](Game#gameinskippablecutscene),
[Game.SkippingCutscene](Game#gameskippingcutscene)

---

### `GetGameOption`

    GetGameOption (option)

Gets the current setting of one of the game options, originally set in
the AGS Editor Game Settings pane.

OPTION specifies which option to get, and its current value is returned.

The valid values for OPTION are listed in
[SetGameOption](Globalfunctions_General#setgameoption).

Example:

    if (GetGameOption(OPT_PIXELPERFECT) == 1) {
      Display("pixel-perfect click deteciton is on!");
    }

*See Also:* [SetGameOption](Globalfunctions_General#setgameoption)

---

### `GetGameParameter`

The *GetGameParameter* function is now obsolete.

It has been replaced with the following functions and properties:

[Game.SpriteWidth](Game#gamespritewidth) (was gp_spritewidth)<br>
[Game.SpriteHeight](Game#gamespriteheight) (was gp_spriteheight)<br>
[Game.GetLoopCountForView](Game#gamegetloopcountforview) (was
GP_NUMLOOPS)<br>
[Game.GetFrameCountForLoop](Game#gamegetframecountforloop) (was
GP_NUMFRAMES)<br>
[Game.GetRunNextSettingForLoop](Game#gamegetrunnextsettingforloop)
(was GP_ISRUNNEXTLOOP)<br>
[Game.GetViewFrame](Game#gamegetviewframe) (was GP_FRAMExxx,
GP_ISFRAMEFLIPPED)<br>
[Game.GUICount](Game#gameguicount) (was gp_numguis)<br>
[Room.ObjectCount](Room#roomobjectcount) (was gp_numobjects)<br>
[Game.CharacterCount](Game#gamecharactercount) (was
GP_NUMCHARACTERS)<br>
[Game.InventoryItemCount](Game#gameinventoryitemcount)(was
GP_NUMINVITEMS)

---

### `GetGameSpeed`

    GetGameSpeed ()

Returns the current game speed (number of cycles per second).

Example:

    if (GetGameSpeed() > 40) {
      SetGameSpeed(40);
    }

will always keep the game speed at 40 cycles per second (in case the
user has raised it )

*See Also:* [SetGameSpeed](Globalfunctions_General#setgamespeed)

---

### `GetGlobalInt`

    GetGlobalInt (int index)

Returns the value of global int INDEX.

**NOTE:** GlobalInts are now considered obsolete. Consider using
[global variables](GlobalVariables) instead, which allow you to
name the variables.

Example:

    if (GetGlobalInt(20) == 1) {
      // code here
    }

will execute the code only if Global Integer 20 is 1.

*See Also:* [SetGlobalInt](Globalfunctions_General#setglobalint),
[Game.GlobalStrings](Game#gameglobalstrings)

---

### `GetGraphicalVariable`

    GetGraphicalVariable (string variable_name);

Returns the value of the interaction editor VARIABLE_NAME variable.
This allows your script to access the values of variables set in the
interaction editor.

**NOTE:** This command is obsolete, and is only provided for backwards
compatibility with AGS 2.x. When writing new code, use
[global variables](GlobalVariables) instead.

Example:

    if (GetGraphicalVariable("climbed rock")==1)
       { code here }

will execute the code only if interaction variable \"climbed rock\" is
1.

*See Also:* [GetGlobalInt](Globalfunctions_General#getglobalint),
[SetGraphicalVariable](Globalfunctions_General#setgraphicalvariable)

---

### `GetLocationType`

    LocationType GetLocationType(int x, int y)

Returns what type of room thing is seen under the given screen coordinates (x, y): whether it is a character, object, hotspot or nothing at all. This may be useful, for example, if you want to process a mouse click differently depending on what the player clicks on.

It's important to know that this will work only if there's a room viewport found on screen at that point, otherwise this function will fail and return "nothing".

Also, this function is "blocked" by any interactable non-room object, such as GUI, and will return "nothing" as well if one is found under these screen coordinates.

**NOTE:** The co-ordinates are SCREEN co-ordinates, NOT ROOM co-ordinates. This means that this function is suitable for use with the mouse cursor position variables.

The value returned is one of the following:

    eLocationNothing    nothing, GUI or inventory
    eLocationHotspot    a hotspot
    eLocationCharacter  a character
    eLocationObject     an object

Example:

    if (GetLocationType(mouse.x,mouse.y) == eLocationCharacter)
        mouse.Mode = eModeTalk;

will set the cursor mode to talk if the cursor is over a character.

*See Also:* [Hotspot.GetAtScreenXY](Hotspot#hotspotgetatscreenxy),
[Game.GetLocationName](Game#gamegetlocationname),
[Object.GetAtScreenXY](Object#objectgetatscreenxy)

---

### `GetPlayerCharacter`

    GetPlayerCharacter ()

**THIS COMMAND IS NOW OBSOLETE.**<br>
The recommended replacement is to use the player character's ID
property, as follows:

Example:

    Display("The player character number is %d", player.ID);

*See Also:* [Character.ID](Character#characterid)

---

### `GetTextHeight`

    GetTextHeight(string text, FontType font, int width)

Calculates the height on the screen that drawing TEXT in FONT within an
area of WIDTH would take up.

This allows you to work out how tall a message displayed with a command
like [DrawMessageWrapped](DrawingSurface#drawingsurfacedrawmessagewrapped)
will be. WIDTH is the width of the area in which the text will be
displayed.

The height is returned in screen pixels, so it can be
used with the screen display commands.

Example:

    int height = GetTextHeight("The message on the GUI!", Game.NormalFont, 100);
    gBottomLine.SetPosition(0, 200 - height);

will move the BOTTOMLINE GUI so that it can display the text within the
screen.

*See Also:* [GetTextWidth](Globalfunctions_General#gettextwidth),
[DrawingSurface.DrawString](DrawingSurface#drawingsurfacedrawstring)

---

### `GetTextWidth`

    GetTextWidth(string text, FontType font)

Returns the width on the screen that drawing TEXT in FONT on one line
would take up.

This could be useful if you manually need to center or right-align some
text, for example with the raw drawing routines.

The width is returned in screen pixels, so it can be used
with the screen display commands.

Example:

    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawingColor = 14;
    int width = GetTextWidth("Hello!", Game.NormalFont);
    surface.DrawString(160 - (width / 2), 100, Game.NormalFont, "Hello!");
    surface.Release();

will print \"Hello!\" onto the middle of the background scene.

*See Also:* [GetTextHeight](Globalfunctions_General#gettextheight),
[DrawingSurface.DrawString](DrawingSurface#drawingsurfacedrawstring)

---

### `GetTranslation`

    String GetTranslation(string original)

Gets the translated equivalent of the supplied string. You do not
normally need to use this since the game translates most things for you.
However, if you have used an InputBox or other form of user input, and
want to compare the user's input to a particular string, it cannot be
translated automatically. So, you can do this instead.

Example:

    String buffer = Game.InputBox("Enter the password:");
    if (buffer.CompareTo(GetTranslation("secret")) == 0) {
      // it matched the current translation of "secret"
    }

If there is no translation for the supplied string, it will be returned
unchanged, so it is always safe to use this function.

*See Also:* 
[Game.ChangeTranslation](Game#gamechangetranslation),
[Game.TranslationFilename](Game#gametranslationfilename),
[IsTranslationAvailable](Globalfunctions_General#istranslationavailable),
[Translation Manual](Translations)

---

### `GiveScore`

    GiveScore (int score)

Adds SCORE to the player's score. This is preferable to directly
modifying the variable since it will play the score sound, update any
status lines and call the GOT_SCORE on_event function.

Note that SCORE can be negative, in which case the score sound is NOT
played.

Example:

    GiveScore(5);

will give 5 points to the player.

*See Also:* [Game.DoOnceOnly](Game#gamedoonceonly)

---

### `GetFontHeight`

    int GetFontHeight (int font)

Returns the given font's height, in pixels. This value may be used, for
example, to calculate arrangement of text and GUI elements on screen.

Example:

    int h = GetFontHeight(eFontSpeech);

will store the speech font's height in the variable.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [GetFontLineSpacing](Globalfunctions_General#getfontlinespacing)

---

### `GetFontLineSpacing`

    int GetFontLineSpacing (int font)

Returns the step between two lines of text for the specified font. If
this value equals font's height, then each next line is rendered right
after previous one with no space in between. If the line spacing is
lower than font's height, then the lines of text are partially
overlapping.

**NOTE:** this is the distance between the **top** of the first line and
the **top** of the next line, and **not** distance between bottom of
first line and top of next one. If you need to calculate the **gap**
between the lines, then subtract [font's height](Globalfunctions_General#getfontheight) from
the line spacing value.

Example:

    int h = GetFontHeight(eFontSpeech);
    int spacing = GetFontLineSpacing(eFontSpeech);
    int gap = spacing - h;

will calculate the gap between two lines of text, that are drawn using
speech font.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [GetFontHeight](Globalfunctions_General#getfontheight)

---

### `InventoryScreen`

    InventoryScreen ()

This command is obsolete.

**This command was used for displaying a default inventory window in
previous versions of AGS, but is no longer supported.**

Instead of using this command, you should create your own Inventory GUI.

---

### `IsGamePaused`

    IsGamePaused ()

Returns *true* if the game is currently paused, or *false* otherwise.
The game is paused when either the icon bar interface has been popped
up, or a \"script-only\" interface has been displayed with
GUI.Visible=true. While the game is paused, no animations or other
updates take place.

Example:

    if (IsGamePaused()) UnPauseGame();

will unpause the game if it's paused.

*See Also:* [GUI.Visible](GUI#guivisible)

---

### `IsInterfaceEnabled`

    IsInterfaceEnabled()

Returns 1 if the player interface is currently enabled, 0 if it is
disabled. The user interface is disabled while the cursor is set to the
Wait cursor - i.e. while the character is performing a blocking Walk, or
other blocking action.

Example:

    if (IsInterfaceEnabled())
        DisableInterface();

will disable the user interface if it's enabled.

*See Also:* [DisableInterface](Globalfunctions_General#disableinterface),
[EnableInterface](Globalfunctions_General#enableinterface)

---

### `IsInteractionAvailable`

    int IsInteractionAvailable(int x, int y, int mode)

Checks whether there is an interaction defined inside a room for clicking on the screen at (X, Y) in cursor mode MODE.
Please note that x and y are *screen* coordinates, not room coordinates.

This function is very similar to Room.ProcessClick, except that rather than carry out any interactions it encounters, it simply returns 1 if something would have happened, or 0 if unhandled_event would have been run.

Function will fail and return 0 if there's no room viewport on screen at the given coordinates. On the other hand it ignores any non-room objects such as GUI, and "clicks through" any GUI that covers room at this location.

This function is useful for enabling options on a verb-coin style GUI, for example.

Example:

    if (IsInteractionAvailable(mouse.x, mouse.y, eModeLookat) == 0)
      Display("looking here would not do anything.");

*See Also:*
[InventoryItem.IsInteractionAvailable](InventoryItem#inventoryitemisinteractionavailable),
[Hotspot.IsInteractionAvailable](Hotspot#hotspotisinteractionavailable),
[Object.IsInteractionAvailable](Object#objectisinteractionavailable),
[Character.IsInteractionAvailable](Character#characterisinteractionavailable),
[Room.ProcessClick](Room#roomprocessclick)

---

### `IsKeyPressed`

    IsKeyPressed(eKeyCode)

Tests whether the supplied key on the keyboard is currently pressed down
or not. You could use this to move an object while the player holds an
arrow key down, for instance.

KEYCODE is one of the [ASCII codes](ASCIIcodes), with some
limitations: since it tests the raw state of the key, you CANNOT pass
the Ctrl+(A-Z) or Alt+(A-Z) codes (since they are key combinations). You
can, however, use some extra codes which are listed at the bottom of the
section.

Returns 1 if the key is currently pressed, 0 if not.

**NOTE:** The numeric keypad can have inconsistent keycodes between
IsKeyPressed and on_key_press. With IsKeyPressed, the numeric keypad
always uses keycodes in the 370-381 range. on_key_press, however,
passes different values if Num Lock is on since the key presses are
interpreted as the number key rather than the arrow key.

Example:

    if (IsKeyPressed(eKeyUpArrow))
      cEgo.Walk(cEgo.x, cEgo.y+3);

will move the character EGO upwards 3 pixels when the up arrow is
pressed.

*See Also:* [Mouse.IsButtonDown](Mouse#mouseisbuttondown)

---

### `IsTimerExpired`

    bool IsTimerExpired(int timer_id)

Checks whether the timer TIMER_ID has expired. If the timeout set with
SetTimer has elapsed, returns *true*. Otherwise, returns *false*.

Note that this function will only return *true* once - after that, the
timer is placed into an OFF state where it will always return *false*
until restarted.

Example:

    if (IsTimerExpired(1)) {
      Display("Timer 1 expired");
    }

will display a message when timer 1 expires.

*See Also:* [SetTimer](Globalfunctions_General#settimer)

---

### `IsTranslationAvailable`

    IsTranslationAvailable ()

Finds out whether the player is using a game translation or not.

Returns 1 if a translation is in use, 0 if not.

*See Also:* 
[Game.ChangeTranslation](Game#gamechangetranslation),
[Game.TranslationFilename](Game#gametranslationfilename),
[GetTranslation](Globalfunctions_General#gettranslation),
[Translation Manual](Translations)

---

### `MoveCharacterToHotspot`

**This function is now obsolete. Use Character.Walk instead**

    MoveCharacterToHotspot (CHARID, int hotspot)

Moves the character CHARID from its current location to the walk-to
point for the specified hotspot. If the hotspot has no walk-to point,
nothing happens.

This is a blocking call - control is not returned to the script until
the character has reached its destination.

Example:

    MoveCharacterToHotspot(EGO,6);

will move the character EGO to the hotspot's 6 \"walk to point\".

*See Also:* [Hotspot.WalkToX](Hotspot#hotspotwalktox),
[Hotspot.WalkToY](Hotspot#hotspotwalktoy),
[Character.Walk](Character#characterwalk),
[MoveCharacterToObject](Globalfunctions_General#movecharactertoobject)

---

### `MoveCharacterToObject`

**This function is now obsolete. Use Character.Walk instead**

    MoveCharacterToObject (CHARID, int object)

Moves the character CHARID from its current location to a position just
below the object OBJECT. This is useful for example, if you want the man
to pick up an object. This is a blocking call - control is not returned
to the script until the character has reached its destination.

Example:

    MoveCharacterToObject (EGO, 0);
    object[0].Visible = false;

Will move the character EGO below object number 0, then turn off object
0.

*See Also:* [Character.Walk](Character#characterwalk),
[MoveCharacterToHotspot](Globalfunctions_General#movecharactertohotspot)

---

### `PauseGame`

    PauseGame ()

Stops AGS processing character movement and animations. This has the
same effect on the game as happens when a modal GUI is popped up. `PauseGame()`
works as a counter, so if you call it twice, you will need to 
call `UnPauseGame()` game twice too to resume game.

To avoid this behavior make sure to only pause once:


    if (!IsGamePaused()) PauseGame();


Game processing will not resume until you call the UnPauseGame function
as needed.

**NOTE:** When the game is paused, game cycles will continue to run but
no animations or movement will be performed, and timers will not count
down. Apart from that, your scripts will continue to run as normal.

**NOTE:** GUI button animations will not be paused by this command, so
that you can run animations on a pop-up GUI while the rest of the game
is paused.

Example:

    if (IsKeyPressed(32)) PauseGame();

will pause the game if the player presses the space bar

*See Also:* [UnPauseGame](Globalfunctions_General#unpausegame)

---

### `QuitGame`

    QuitGame(int ask_first)

Exits the game and returns to the operating system.

If ASK_FIRST is zero, it will exit immediately. If ASK_FIRST is not
zero, it will first display a message box asking the user if they are
sure they want to quit.

Example:

    QuitGame(0);

will quit the game without asking the player to confirm.

*See Also:* [AbortGame](Globalfunctions_General#abortgame)

---

### `Random`

    Random (int max)

Returns a random number between 0 and MAX. This could be useful to do
various effects in your game. MAX must be a positive value in range
0-32767.

**NOTE:** Because of the way Random is implemented in AGS, the return
value will never be higher than 32767.

**NOTE:** The range returned is inclusive - i.e. if you do Random(3);
then it can return 0, 1, 2 or 3.

Example:

    int ran=Random(2);
    if (ran==0) cEgo.ChangeRoom(1);
    else if (ran==1) cEgo.ChangeRoom(2);
    else cEgo.ChangeRoom(3);

will change the current room to room 1,2 or 3 depending on a random
result.

---

### `RestartGame`

    RestartGame ()

Restarts the game from the beginning.

Example:

    if (IsKeyPressed(365)) RestartGame();

will restart the game if the player presses the F7 key.

*SeeAlso:* [SetRestartPoint](Globalfunctions_General#setrestartpoint)

---

### `RestoreGameDialog`

    RestoreGameDialog ()

Displays the restore game dialog, where the player can select a
previously saved game position to restore.

The dialog is not displayed immediately; instead, it will be displayed
when the script function finishes executing.

Example:

    if (IsKeyPressed(363)) RestoreGameDialog();

will bring up the restore game dialog if the player presses the F5 key.

*See Also:* [RestoreGameSlot](Globalfunctions_General#restoregameslot),
[SaveGameDialog](Globalfunctions_General#savegamedialog)

---

### `RestoreGameSlot`

    RestoreGameSlot (int slot)

Restores the game position saved into slot number SLOT. You might want
to use these specific slot functions if for example you only want to
allow the player to have one save game position rather than the usual
20. If this slot number does not exist, an error message is displayed to
the player but the game continues. To avoid the error, use the
GetSaveSlotDescription function to see if the position exists before
restoring it.

**NOTE:** The game will not be restored immediately; instead, it will be
restored when the script function finishes executing.

Example:

    RestoreGameSlot(30);

will restore game slot 30 if this slot number exists.

*See Also:*
[Game.GetSaveSlotDescription](Game#gamegetsaveslotdescription),
[RestoreGameDialog](Globalfunctions_General#restoregamedialog),
[SaveGameSlot](Globalfunctions_General#savegameslot)

---

### `RunAGSGame`

    RunAGSGame (string filename, int mode, int data)

Quits the current game, and loads up FILENAME instead. FILENAME must be
an AGS game EXE or AC2GAME.AGS file, and it must be in the current
directory.

MODE specifies various options about how you want to run the game.
Currently the supported values are:

    0   Current game is completely exited, new game runs as if it had been launched separately
    1   GlobalInt values are preserved and are not set to 0 for the new game.

DATA allows you to pass an integer through to the next game. The value
you pass here will be accessible to the loaded game by it reading the
game.previous_game_data variable.

The save game slots are shared between the two games, and if you load a
save slot that was saved in the other game, it will automatically be
loaded.

Bear in mind that because the games must be in the same folder, they
will also share the audio.vox, speech.vox and so forth. This is a
limitation of this command.

**NOTE:** The game you run will be loaded at the same resolution and
color depth as the current game; if you mismatch color depths some
nasty results will occur.

**NOTE:** The game you want to launch must have been created with the
same point-version of AGS as the one you are launching it from. (version
2.xy - the X must be the same version between the two games).

Example:

    RunAGSGame ("MyGame.exe", 0, 51);

will run the MyGame game, passing it the value 51.

---

### `SaveGameDialog`

    SaveGameDialog ()

Displays the save game dialog, where the player can save their current
game position. If they select to save, then the game position will be
saved.

**NOTE:** The dialog will not be displayed immediately; instead, it will
be shown when the script function finishes executing.

Example:

    if (keycode == 361) SaveGameDialog();

will bring up the save game dialog if the player presses the F3 key.

*See Also:* [RestoreGameDialog](Globalfunctions_General#restoregamedialog),
[SaveGameSlot](Globalfunctions_General#savegameslot)

---

### `SaveGameSlot`

    SaveGameSlot (int slot, string description)

Saves the current game position to the save game number specified by
SLOT, using DESCRIPTION as the textual description of the save position.
Be careful using this function, because you could overwrite one of the
player's save slots if you aren't careful.

The SaveGameDialog function uses slots numbered from 1 to 20, so if you
don't want to interfere with the player's saves, I would recommend
saving to slot numbers of 100 and above.

**NOTE:** The game will not be saved immediately; instead, it will be
saved when the script function finishes executing.

Example:

    SaveGameSlot(30, "save game");

will save the current game position to slot 30 with the description
\"Save game\".

*See Also:* [DeleteSaveSlot](Globalfunctions_General#deletesaveslot),
[RestoreGameSlot](Globalfunctions_General#restoregameslot),
[SaveGameDialog](Globalfunctions_General#savegamedialog)

---

### `SaveScreenShot`

    SaveScreenShot (string filename)

Takes a screen capture and saves it to disk. The FILENAME must end in
either \".BMP\" or \".PCX\", as those are the types of files which can
be saved. Returns 1 if the shot was successfully saved, or 0 if an
invalid file extension was provided.

**NOTE:** The screenshot will be saved to the Saved Games folder.

**NOTE:** This command can be slow when using the Direct3D graphics
driver.

Example:

    String input = Game.InputBox("Type the filename:");
    input = input.Append(".pcx");
    SaveScreenShot(input);

will prompt the player for a filename and then save the screenshot with
the filename the player typed.

*See Also:*
[DynamicSprite.SaveToFile](DynamicSprite#dynamicspritesavetofile)

---

### `SetAmbientLightLevel`

    void SetAmbientLightLevel(int light_level);

Sets an ambient light level that affects all objects and characters in
the room.

The light level is from **-100 to 100**, where 0 means that no
adjustment will be applied to sprites.

In 8-bit games you cannot use positive light level for brightening
effect, but you may still use negative values to produce darkening
effect.

To turn light level off, call this command again but pass the
*light_level* as 0.

**NOTE:** This function overrides any specific region light levels or
tints on the screen, but does NOT override individual character and
object light levels.

**NOTE**: Setting an ambient light level will disable ambient RGB tint,
if there one was previously set.

Example:

    SetAmbientLightLevel(50);

will apply light level 50 to every character and object on screen (which
do not have individual light levels).

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [SetAmbientTint](Globalfunctions_General#setambienttint),
[Character.SetLightLevel](Character#charactersetlightlevel),
[Object.SetLightLevel](Object#objectsetlightlevel),
[Region.LightLevel](Region#regionlightlevel)

---

### `SetAmbientTint`

    SetAmbientTint(int red, int green, int blue, int saturation, int luminance)

Tints all objects and characters on the screen to (RED, GREEN, BLUE)
with SATURATION percent saturation.

This allows you to apply a global tint to everything on the screen. The
RED, GREEN and BLUE parameters are from 0-255, and specify the color of
the tint.

The SATURATION parameter defines how much the tint is applied, and is
from 0-100. A saturation of 100 will completely re-colorize the sprites
to the supplied color, and a saturation of 1 will give them a very
minor tint towards the specified color.

The LUMINANCE parameter allows you to adjust the brightness of the
sprites at the same time. It ranges from 0-100. Passing 100 will draw
the sprites at normal brightness. Lower numbers will darken the images
accordingly, right down to 0 which will draw everything black.

The tint applied by this function is global. To turn it off, call this
command again but pass the saturation as 0.

**NOTE:** This function only works in hi-color games and with hi-color
sprites.

**NOTE:** This function overrides any specific region light levels or
tints on the screen.

Example:

    SetAmbientTint(0, 0, 250, 30, 100);

will tint everything on the screen with a hint of blue.

*See Also:* [SetAmbientLightLevel](Globalfunctions_General#setambientlightlevel),
[Character.Tint](Character#charactertint),
[Object.Tint](Object#objecttint),
[Region.Tint](Region#regiontint)

---

### `SetGameOption`

    SetGameOption (option, int value)

Changes one of the game options, originally set in the AGS Editor Game
Settings pane.

OPTION specifies which option to change, and VALUE is its new value.
Valid OPTIONs are listed below:

Option | Values
--- | ---
OPT_WALKONLOOK | Walk to hotspot in look mode (0 or 1)
OPT_DIALOGOPTIONSGUI | Dialog options on GUI (0=none, otherwise GUI name/number)
OPT_DIALOGOPTIONSGAP | Pixel gap between options (0=none, otherwise num pixels)
OPT_WHENGUIDISABLED | When GUI is disabled, 0=grey out, 1=go black, 2=unchanged, 3=turn off
OPT_ALWAYSSPEECH | Always display text as speech (0 or 1)
OPT_PIXELPERFECT | Pixel-perfect click detection (0 or 1)
OPT_NOWALKMODE | Don't automatically move character in Walk mode (0 or 1)
OPT_FIXEDINVCURSOR | Don't use inventory graphics as cursors (0 or 1)
OPT_DONTLOSEINV | Don't automatically lose inventory items (0 or 1)
OPT_TURNBEFOREWALK | Characters turn before walking (0 or 1)
OPT_HANDLEINVCLICKS | Handle inventory clicks in script (0 or 1)
OPT_MOUSEWHEEL | Enable mouse wheel support (0 or 1)
OPT_DIALOGNUMBERED | Number dialog options (-1=disabled, 0=shortcuts only, 1=drawn numbers)
OPT_DIALOGUPWARDS | Dialog options go upwards on GUI (0 or 1)
OPT_CROSSFADEMUSIC | Crossfade music tracks (0=no, 1=slow, 2=slow-ish, 3=medium, 4=fast)
OPT_ANTIALIASFONTS | Anti-alias rendering of TTF fonts (0 or 1)
OPT_THOUGHTGUI | Thought uses bubble GUI (GUI name/number)
OPT_TURNWHENFACING | Characters turn to face direction (0 or 1)
OPT_LIPSYNCTEXT | Whether lip-sync text reading is enabled (0 or 1)
OPT_RIGHTTOLEFT | Right-to-left text writing (0 or 1)
OPT_MULTIPLEINV | Display multiple inv items multiple times (0 or 1)
OPT_SAVEGAMESCREENSHOTS | Save screenshots into save games (0 or 1)
OPT_PORTRAITPOSITION | Speech portrait side (0=left, 1=right, 2=alternate, 3=xpos)

The game settings which are not listed here either have a separate
command to change them (such as Speech.Style), or simply cannot be
changed at run-time.

This command returns the old value of the setting.

Example:

    SetGameOption (OPT_PIXELPERFECT, 0);

will disable pixel-perfect click detection.

*See Also:* [GetGameOption](Globalfunctions_General#getgameoption),
[Speech.Style](Speech#speechstyle),
[SetTextWindowGUI](Globalfunctions_General#settextwindowgui)

---

### `SetGameSpeed`

    SetGameSpeed (int new_speed)

Sets the maximum game frame rate to NEW_SPEED frames per second, or as
near as possible to that speed. The default frame rate is 40 fps, but
you can speed up or slow down the game by using this function. Note that
this speed is also the rate at which the Repeatedly_Execute functions
are triggered.

The NEW_SPEED must lie between 10 and 1000. If it does not, it will be
rounded to 10 or 1000. Note that if you set a speed which the player's
computer cannot handle (for example, a 486 will not be able to manage 80
fps), then it will go as fast as possible.

NOTE: Because the mouse cursor is repainted at the game frame rate, at
very low speeds, like 10 to 20 fps, the mouse will appear to be jumpy
and not very responsive.

NOTE: If you set the [System.VSync](System#systemvsync) property to
*true*, the game speed will be capped at the screen's refresh rate, so
you will be unable to set it higher than 60-85 (depending on the
player's screen refresh).

Example:

    SetGameSpeed(80);

will set the game speed to 80.

*See Also:* [GetGameSpeed](Globalfunctions_General#getgamespeed)

---

### `SetGlobalInt`

    SetGlobalInt (int index, int value)

Sets the global int INDEX to VALUE. You can then retrieve this value
from any other script using GetGlobalInt.

There are 500 available global variables, from index 0 to 499.

**NOTE:** GlobalInts are now considered obsolete. Consider using
[global variables](GlobalVariables) instead, which allow you to
name the variables.

Example:

    SetGlobalInt(10,1);

will set the Global Integer 10 to 1.

*See Also:* [GetGlobalInt](Globalfunctions_General#getglobalint)

---

### `SetGraphicalVariable`

    SetGraphicalVariable(string variable_name, int value);

Sets the interaction editor VARIABLE_NAME variable to VALUE. This
allows your script to change the values of variables set in the
interaction editor.

**NOTE:** This command is obsolete, and is only provided for backwards
compatibility with AGS 2.x. When writing new code, use
[global variables](GlobalVariables) instead.

Example:

    SetGraphicalVariable("climbed rock", 1);

will set the interaction editor \"climbed rock\" variable to 1.

*See Also:* [GetGraphicalVariable](Globalfunctions_General#getgraphicalvariable)

---

### `SetMultitaskingMode`

    SetMultitaskingMode (int mode)

Allows you to set what happens when the user switches away from your
game.

If MODE is 0 (the default), then if the user Alt+Tabs out of your game,
or clicks on another window, the game will pause and not continue until
they switch back into the game.

If MODE is 1, then the game will continue to run in the background if
the user switches away (useful if, for example, you are just making some
sort of jukebox music player with AGS).

Note that mode 1 does not work with some graphics cards in full-screen
mode, so you should only rely on it working when your game is run in
windowed mode.

**Cross-Platform Support**

Windows: **Yes**<br>
Linux: **Yes**<br>
MacOS: **Yes**

Example:

    SetMultitaskingMode (1);

will mean that the game continues to run in the background.

---

### `SetRestartPoint`

    SetRestartPoint ()

Changes the game restart point to the current position. This means that
from now on, if the player chooses the Restart Game option, it will
return here.

This function is useful if the default restart point doesn't work
properly in your game - just use this function to move it.

**NOTE:** The restart point cannot be set while a script is running \--
therefore, when you call this it will actually set the restart point at
the next game loop where there is not a blocking script running in the
background.

*SeeAlso:* [RestartGame](Globalfunctions_General#restartgame)

---

### `SetTextWindowGUI`

    SetTextWindowGUI (int gui)

Changes the GUI used for text windows to the specified GUI. This
overrides the \"text windows use GUI\" setting in the editor.

You can pass -1 as the GUI number to go back to using the default white
text box.

Example:

    SetTextWindowGUI (4);

will change Textwindow GUI 4 to be used for displaying text windows in
future.

---

### `SetTimer`

    SetTimer (int timer_id, int timeout)

Starts timer TIMER_ID ticking - it will tick once every game loop
(normally 40 times per second), until TIMEOUT loops, after which it will
stop. You can check whether the timer has finished by calling the
IsTimerExpired function.

Pass TIMEOUT as 0 to disable a currently running timer.

There are 20 available timers, with TIMER_IDs from 1 to 20.

**NOTE:** the timer will not tick while the game is paused.

Example:

    SetTimer(1,1000);

will set the timer 1 to expire after 1000 game cycles.

Example 2:

When you have a hard time keeping track of the timers only by number you can use [Macros](Preprocessor#define) to replace the descriptive name with the time number everywhere the descriptive name is use. To better keep track of these macros you could put them on top of the global script.

    #define Delay_CustomAnimation 1

    SetTimer(Delay_CustomAnimation, 2000); 

this "names" timer 1 and sets it to expire after 2000 game cycles

*See Also:* [IsTimerExpired](Globalfunctions_General#istimerexpired)

---

### `SkipCutscene`

    SkipCutscene()

Explicitly commences skipping current cutscene. If game is not in a cutscene sequence or cutscene is already being skipped this function will do nothing.

SkipCutscene will work regardless of the StartCutscene parameters, but is most useful when you do not want to rely on built-in skipping controls and are coding your own. In the latter case make sure to start cutscene in **eSkipScriptOnly** mode to prevent any standard input interference.

Example:

    if (Game.InSkippableCutscene && IsKeyPressed(eKeySpace)) {
      SkipCutscene();
    }

will check if game is inside a cutscene, and if player has pressed a space bar then commands to skip it.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [EndCutscene](Globalfunctions_General#endcutscene), [SkipUntilCharacterStops](Globalfunctions_General#skipuntilcharacterstops), [StartCutscene](Globalfunctions_General#startcutscene), [Game.InSkippableCutscene](Game#gameinskippablecutscene),
[Game.SkippingCutscene](Game#gameskippingcutscene)

---

### `SkipUntilCharacterStops`

    SkipUntilCharacterStops(CHARID)

Skips through the game until the specified character stops walking, a
blocking script runs, or a message box is displayed.

The purpose of this command is to mimic the functionality in games such
as The Longest Journey, where the player can press ESC to instantly get
the character to its destination. It serves as a handy feature to allow
you to give the player character a relatively slow walking speed,
without annoying the player by making them wait ages just to get from A
to B.

If the specified character is not moving when this function is called,
nothing happens.

Example: (in on_key_press)

    if (keycode == eKeyEscape) SkipUntilCharacterStops(EGO);

This means that if the player presses ESC, the game will skip ahead
until EGO finishes moving, or is interrupted by a Display command or a
blocking cutscene.

*See Also:* [StartCutscene](Globalfunctions_General#startcutscene)

---

### `StartCutscene`

    StartCutscene(CutsceneSkipType)

Marks the start of a cutscene. Once your script passes this point, the
player can choose to skip a portion by pressing a key or the mouse
button. This is useful for things like introduction sequences, where you
want the player to be able to skip over an intro that they've seen
before.

The CutsceneSkipType determines how they can skip the cutscene:

    eSkipESCOnly
      by pressing ESC only
    eSkipAnyKey
      by pressing any key
    eSkipMouseClick
      by clicking a mouse button
    eSkipAnyKeyOrMouseClick
      by pressing any key or clicking a mouse button
    eSkipESCOrRightButton
      by pressing ESC or clicking the right mouse button
    eSkipScriptOnly
      only by calling SkipCutscene script function

**NOTE:** eSkipScriptOnly may be useful if you are coding your own cutscene skipping method in script and would like to disable built-in ones.

You need to mark the end of the cutscene with the EndCutscene command.

Be **very careful** with where you place the corresponding EndCutscene
command. The script **must** pass through EndCutscene in its normal run
in order for the skipping to work - otherwise, when the player presses
ESC the game could appear to hang.

*Compatibility:* eSkipScriptOnly cutscene mode is supported by **AGS 3.5.0** and later versions.

*See Also:* [EndCutscene](Globalfunctions_General#endcutscene), [SkipCutscene](Globalfunctions_General#skipcutscene), [SkipUntilCharacterStops](Globalfunctions_General#skipuntilcharacterstops),
[Game.InSkippableCutscene](Game#gameinskippablecutscene),
[Game.SkippingCutscene](Game#gameskippingcutscene)

---

### `UpdateInventory`

    UpdateInventory ()

Updates the on-screen inventory display. If you add or remove inventory
items manually (i.e. by using the InventoryQuantity array rather than the
AddInventory/LoseInventory functions), the display may not get updated.
In this case call this function after making your changes, to update
what is displayed to the player.

Note that using this function will reset the order that items are
displayed in the inventory window to the same order they were created in
the editor.

*See Also:* [Character.AddInventory](Character#characteraddinventory),
[Character.LoseInventory](Character#characterloseinventory),
[Character.InventoryQuantity](Character#characterinventoryquantity)

---

### `UnPauseGame`

    UnPauseGame ()

Resumes the game. 

Example:

    if (IsGamePaused() == 1)
        UnPauseGame();

will unpause the game if it is paused. 

**NOTE:** Because PauseGame works as a counter, if you called it more
than once, this won't work. To ignore this behavior, unpause as much
as needed with the below snippet.

    while (IsGamePaused()) UnPauseGame();

*See Also:* [PauseGame](Globalfunctions_General#pausegame)

---

### `Wait`

    Wait (int time)

Pauses the script and lets the game continue for TIME loops. There are
normally 40 loops/second (unless you change it with SetGameSpeed), so
using a value of 80 will wait 2 seconds. Note that no other scripts can
run while the Wait function is in the background.

Example:

    cEgo.Walk(120, 140, eBlock, eWalkableAreas);
    Wait(80);
    cEgo.FaceLocation(1000,100);

will move the character EGO to 120,140, wait until he gets there then
wait for 2 seconds (80 game cycles) and then face right.

*See Also:* [WaitKey](Globalfunctions_General#waitkey),
[WaitMouseKey](Globalfunctions_General#waitmousekey)

---

### `WaitKey`

    WaitKey (int time)

Pauses the script and lets the game continue until EITHER:

\(a) TIME loops have elapsed, or

\(b) the player presses a key

Returns 0 if the time elapsed, or 1 if the player interrupted it.

Example:

    WaitKey(200);

will pause the script and wait until 5 seconds have passed or the player
presses a key.

*See Also:* [Wait](Globalfunctions_General#wait),
[WaitMouseKey](Globalfunctions_General#waitmousekey)

---

### `WaitMouseKey`

    WaitMouseKey (int time)

Pauses the script and lets the game continue until EITHER:

\(a) TIME loops have elapsed, or

\(b) the player presses a key, or

\(c) the player clicks a mouse button

Returns 0 if the time elapsed, or 1 if the player interrupted it.

Example:

    WaitMouseKey(200);

will pause the script and wait until 5 seconds have passed or the player
presses a key or clicks the mouse.

*See Also:* [Wait](Globalfunctions_General#wait), [WaitKey](Globalfunctions_General#waitkey)
