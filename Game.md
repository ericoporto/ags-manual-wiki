## `Game` functions

### `Game.ChangeTranslation`

    static bool Game.ChangeTranslation(string newTranslationName)

Changes the active translation to *newTranslationName*. This must be the
file name without the extension, for example \"French\" or \"Spanish\".
It can also be a blank string, in which case the current translation
will be switched off and the game will revert to the default language.

Returns *true* if the translation was changed successfully, or *false*
if there was a problem (for example, you specified an invalid
translation).

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example below.

Example:

    if (Game.ChangeTranslation("Spanish") == true)
    {
      Display("Changed the translation to Spanish!");
    }
    else
    {
      Display("Unable to change the translation");
    }

will attempt to change the translation to Spanish

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:*
[Game.TranslationFilename](Game#gametranslationfilename),
[GetTranslation](Globalfunctions_General#gettranslation),
[IsTranslationAvailable](Globalfunctions_General#istranslationavailable),
[Translation Manual](Translations)

---

### `Game.DoOnceOnly`

    static bool Game.DoOnceOnly(const string token)

This function gives you an easy way of making some code run only the
first time that the player encounters it. It is commonly used for
awarding points.

The *token* parameter is an arbitrary string. You can pass whatever you
like in for this, but **IT MUST BE UNIQUE**. It is this string that
allows AGS to determine whether this section of code has been run
before, therefore you should make sure that **you do not use the same
token string in two different places in your game**.

Returns *true* the first time that it is called with this token, and
*false* thereafter.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example below.

Example:

    if (Game.DoOnceOnly("open cupboard")) {
      GiveScore(5);
    }

will give the player 5 points the first time this script is run.

*See Also:* [GiveScore](Globalfunctions_General#givescore)

---

### `Game.GetColorFromRGB`

*(Formerly known as RawSetColorRGB, which is now obsolete)*

    static int Game.GetColorFromRGB(int red, int green, int blue)

Gets the AGS Color Number for the specified RGB color. The red, green
and blue components are values from 0 to 255. This function gives you a
run-time equivalent to the Color Finder in the editor.

This command is slow in 256-color games, since the palette has to be
scanned to find the nearest matching color.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example below.

Example:

    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawingColor = Game.GetColorFromRGB(0, 255, 0);
    surface.DrawLine(0, 0, 50, 50);
    surface.Release();

will draw a bright green line onto the room background

*See Also:*
[DrawingSurface.DrawingColor](DrawingSurface#drawingsurfacedrawingcolor)

---

### `Game.GetFrameCountForLoop`

*(Formerly part of GetGameParameter, which is now obsolete)*

    static int Game.GetFrameCountForLoop(int view, int loop)

Returns the number of frames in the specified loop of the specified
view.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example for more.

Example:

    int frameCount = Game.GetFrameCountForLoop(SWIMMING, 2);
    Display("Loop 2 in SWIMMING view has %d frames.", frameCount);

*See Also:*
[Game.GetLoopCountForView](Game#gamegetloopcountforview),
[Game.GetRunNextSettingForLoop](Game#gamegetrunnextsettingforloop),
[Game.GetViewFrame](Game#gamegetviewframe)

---

### `Game.GetLocationName`

*(Formerly known as global function GetLocationName, which is now
obsolete)*

    static String Game.GetLocationName(int x, int y)

Returns the name of whatever is seen in the room under the given screen coordinates (x, y).

It's important to know that this will work only if there's a room viewport found on screen at that point, otherwise this function will fail and return a blank string.

Also, this function is "blocked" by any interactable non-room object, such as GUI, and will return blank string if one is found under these screen coordinates.

**NOTE:** The co-ordinates are SCREEN co-ordinates, NOT ROOM co-ordinates. This means that this function is suitable
for use with the mouse cursor position variables.

This function may allow you, for instance, to create the LucasArts-style status lines reading \"Look at xxx\" as
the player moves the cursor over them.

Example:

    String location = Game.GetLocationName(mouse.x, mouse.y);
    lblDescription.Text = location;

will get the name of whatever the mouse is over into the string variable and then assign to a label lblDescription.

*See Also:* [Hotspot.Name](Hotspot#hotspotname),
[InventoryItem.Name](InventoryItem#inventoryitemname),
[GetLocationType](Globalfunctions_General#getlocationtype),
[Object.Name](Object#objectname)

---

### `Game.GetLoopCountForView`

*(Formerly part of GetGameParameter, which is now obsolete)*

    static int Game.GetLoopCountForView(int view)

Returns the number of loops in the specified view.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example for more.

Example:

    int loops = Game.GetLoopCountForView(SWIMMING);
    Display("The SWIMMING view (view %d) has %d loops.", SWIMMING, loops);

*See Also:*
[Game.GetRunNextSettingForLoop](Game#gamegetrunnextsettingforloop),
[Game.GetFrameCountForLoop](Game#gamegetframecountforloop),
[Game.GetViewFrame](Game#gamegetviewframe)

---

### `Game.GetRunNextSettingForLoop`

*(Formerly part of GetGameParameter, which is now obsolete)*

    static bool Game.GetRunNextSettingForLoop(int view, int loop)

Returns whether the specified loop in the specified view has the \"Run
the next loop after this one\" option checked.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example for more.

Example:

    if (Game.GetRunNextSettingForLoop(SWIMMING, 5) == true) {
      Display("Loop 5 in view SWIMMING does have Run Next Loop set.");
    }
    else {
      Display("Loop 5 in view SWIMMING does not have Run Next Loop set.");
    }

*See Also:*
[Game.GetLoopCountForView](Game#gamegetloopcountforview),
[Game.GetFrameCountForLoop](Game#gamegetframecountforloop),
[Game.GetViewFrame](Game#gamegetviewframe)

---

### `Game.GetSaveSlotDescription`

*(Formerly known as global function GetSaveSlotDescription, which is now
obsolete)*

    static String Game.GetSaveSlotDescription(int slot)

Gets the text description of save game slot SLOT.

If the slot number provided does not exist, returns *null*.

Example:

    String description = Game.GetSaveSlotDescription(10);

will get the description of save slot 10 into the variable.

*See Also:*
[DynamicSprite.CreateFromSaveGame](DynamicSprite#dynamicspritecreatefromsavegame),
[RestoreGameSlot](Globalfunctions_General#restoregameslot),
[SaveGameSlot](Globalfunctions_General#savegameslot)

---

### `Game.GetViewFrame`

*(Formerly part of GetGameParameter, which is now obsolete)*

    static ViewFrame* Game.GetViewFrame(int view, int loop, int frame)

Returns a *ViewFrame* instance for the specified frame in the specified
loop of the specified view.

This instance allows you to query properties of the frame itself, such
as its graphic, its frame-linked sound setting, and so forth.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example for more.

Example:

    ViewFrame *frame = Game.GetViewFrame(SWIMMING, 2, 3);
    Display("Frame 3 in loop 2 of view SWIMMING has sprite slot %d.", frame.Graphic);

*See Also:*
[Game.GetLoopCountForView](Game#gamegetloopcountforview),
[Game.GetRunNextSettingForLoop](Game#gamegetrunnextsettingforloop),
[Game.GetFrameCountForLoop](Game#gamegetframecountforloop),
[ViewFrame.Graphic](ViewFrame#viewframegraphic),
[ViewFrame.Speed](ViewFrame#viewframespeed)

---

### `Game.InputBox`

*(Formerly known as global function InputBox, which is now obsolete)*

    static String Game.InputBox(string prompt)

Pops up a window asking the user to type in a string, with PROMPT as the
text in the window. Whatever they type in will be returned from this
function.

This command displays a very basic input box, mainly useful for
debugging purposes. Due to the size of the window, only small strings up
to about 20 characters can be typed in.

The recommended way to obtain user input is to create your own GUI with
a text box on it, which allows you full customization of the look of the
window.

**TIP:** If you add a '!' character to the start of the prompt, then a
Cancel button will be available in the input box. If the player presses
this Cancel button (or the ESC key), a blank string is returned.

Example:

    String name = Game.InputBox("!What is your name?");

will prompt the user for his name and store it in the string NAME. If
the user presses Cancel, the NAME string will be blank.

*See Also:* [String.AsInt](String#stringasint)

---

### `Game.IsPluginLoaded`

    static bool Game.IsPluginLoaded(const string name)

Checks whether the plugin of the given *name* was present and loaded for
the game.

**IMPORTANT:** If the plugin exports its own script functions that you
used in your game script, and not found when the game is launched, then
the game won't start up at all, exiting with error. IsPluginLoaded may
therefore be useful to check for plugins that are not interacted with
from game script, but just run on their own.

Example:

    if (Game.IsPluginLoaded("my_plugin")) {
      Display("My plugin is found and running!");
    }

will display a message if plugin is present.

---

### `Game.PlayVoiceClip`

    static AudioChannel* Game.PlayVoiceClip(Character* c, int cue, bool as_speech)

Plays a voice clip from the **speech.vox** in a non-blocking manner. It returns an AudioChannel pointer which you may use to control playback same way you control other clips, or null if it could not be started.

Character and "cue" arguments are used to find actual clip, this works the same way as when you do `cEgo.Say("&10 speech text");` in which case "10" is a cue number. For more information about this see: [Voice speech](MusicAndSound#voice-speech).

The "as_speech" argument tells whether playback has same effect on game as regular speech. At the moment this means that music volume will drop and restore after playback is finished. This parameter "as_speech" is TRUE by default and may be omitted.

This command will be ignored if a regular blocking voice is currently playing. Also, both blocking and non-blocking voice will interrupt non-blocking voice-over if one was playing.

**NOTE:** because of how audiochannels work internally right now voice is always played on the same channel 0, therefore you could also get it as `System.AudioChannels[0]`, but it may not be a good idea to rely on this because channel behavior may change in future.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also*: [Voice speech](MusicAndSound#voice-speech), [AudioChannel](AudioChannel), [AudioClip.Play](AudioClip#audioclipplay), [Character.Say](Character#charactersay)

---

### `Game.SetSaveGameDirectory`

    static bool Game.SetSaveGameDirectory(string directory)

Changes the directory where save game files are stored to the supplied
*directory*. If the directory does not exist, AGS will attempt to create
it.

You cannot use fully qualified directories with this command (eg.
`C:\Games\Cool\Saves`), because the player might have installed your
game to any folder, and they might not be running Windows.

Therefore, only two types of path are supported:<br>
1. Relative paths (eg. \"Saves\"). This will create a subfolder inside
**default game save folder**<br>
2. The special tag `$MYDOCS$` which allows you to explicitly create a
different folder for your save games inside the user's documents
folder.

The actual folder referenced with `$MYDOCS$` is different on every
platform: Windows XP: \"My Documents\"<br>
Windows Vista and later: \"Saved Games\"<br>
Linux: `$XDG_DATA_HOME`/ags<br>
MacOS: game installation folder.

Returns *true* if the save game directory has been changed successfully;
*false* if not.

**NOTE:** We advise you against using this function without strong need.
In the most cases setting the \"Save games folder name\" property in the
General Settings of the editor should be sufficient.

Example:

    Game.SetSaveGameDirectory("$MYDOCS$/My Cool Game Saves");

will change the save game directory to \"My Cool Game Saves\" in My
Documents, and create the folder if it does not exist (might be useful
to do this in game_start).

*See Also:*
[ListBox.FillSaveGameList](ListBox#listboxfillsavegamelist),
[RestoreGameDialog](Globalfunctions_General#restoregamedialog)

---

### `Game.SimulateKeyPress`

    static Game.SimulateKeyPress(eKeyCode key)

Fires a keypress event. This is in all aspects identical to what would happen if a player pressed a key on keyboard. This function may be useful to simulate player actions in game, or create automatic demonstrations (like tutorials).

**IMPORTANT:** because of how AGS engine and scripts work the game will react to this keypress not before current script function finishes. Any things that normally react to keys (such as skippable speech, cutscenes, and certain GUI controls) will be affected only at the following internal game update.

Example:

    Game.SimulateKeyPress(eKeySpace);

This simulates a "space" key press.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Mouse.Click](Mouse#mouseclick), [List of supported key codes](ASCIIcodes#ascii-code-table)

---

### `Game.AudioClipCount`

    readonly static int Game.AudioClipCount

Returns the number of audio clips in the game.

This is useful for script modules if you need to iterate through all the
audio clips for some reason.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Game.AudioClips](Game#gameaudioclips)

---

### `Game.AudioClips`

    readonly static int Game.AudioClips[int slot]

Returns the AudioClip\* pointer by its index in game resources.

Example:

    int i = 0;
    int music_count = 0;
    while (i < Game.AudioClipCount)
    {
      if (Game.AudioClips[i].Type == eAudioTypeMusic)
        music_count++;
      i++;
    }
    Display("We have %d musical clips in our game", music_count);

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Game.AudioClipCount](Game#gameaudioclipcount)

---

### `Game.Camera`

    static readonly Camera* Game.Camera;

Gets the primary camera. This is the default camera that is created automatically at the start of the game and cannot be deleted.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Game.Cameras](Game#gamecameras), [Camera](Camera), [Camera.Create](Camera#cameracreate), [Camera.Delete](Camera#cameradelete), [Viewport.Camera](Viewport#viewportcamera)

---

### `Game.CameraCount`

    static readonly int Game.CameraCount

Gets the number of cameras.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Game.Cameras](Game#gamecameras)

---

### `Game.Cameras`

    static readonly Camera* Game.Cameras[int index];

Returns the Camera instance by its index. There's always at least primary camera at the index 0, more could be created in script using [Camera.Create](Camera#cameracreate).

**IMPORTANT:** with the current implementation when you delete a custom camera in the middle all the following cameras will be shifted towards beginning of array, changing their indexes.

Example:

    for (int i = 0; i < Game.CameraCount; i++) {
        Game.Cameras[i].SetAt(0, 0);
    }

This script positions all existing cameras at the room's top-left corner.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Game.Camera](Game#gamecamera), [Game.CameraCount](Game#gamecameracount), [Camera.Create](Camera#cameracreate), [Camera.Delete](Camera#cameradelete), [Viewport.Camera](Viewport#viewportcamera)

---

### `Game.CharacterCount`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Game.CharacterCount

Returns the number of characters in the game.

This is useful for script modules if you need to iterate through all the
characters for some reason.

Example:

    Display("The game has %d characters.", Game.CharacterCount);

---

### `Game.DialogCount`

    readonly static int Game.DialogCount

Returns the number of dialogs in the game.

This is useful for script modules if you need to iterate through all the
dialogs for some reason. Valid dialogs are numbered from 0 to
DialogCount - 1.

Example:

    Display("The game has %d dialogs.", Game.DialogCount);

*Compatibility:* Supported by **AGS 3.0.2** and later versions.

---

### `Game.FileName`

    readonly static String Game.FileName

Gets the filename that the game is running from. This will usually be
the name of the EXE file, but could also be \"ac2game.dat\" if you are
just running the game using ACWIN.EXE.

Example:

    Display("The main game file is: %s", Game.FileName);

will display the game filename.

*See Also:* [Game.Name](Game#gamename)

---

### `Game.FontCount`

    readonly static int Game.FontCount

Returns the number of fonts in the game.

This is useful for script modules if you need to iterate through all the
fonts for some reason.

Example:

    Display("The game has %d fonts.", Game.FontCount);

---

### `Game.GlobalMessages`

*(Formerly known as global function GetMessageText, which is now
obsolete)*

    readonly static String Game.GlobalMessages[int message]

Gets the text of the specified global message. The message number is one
of the global message numbers from 500 to 999.

If an invalid message number is supplied, *null* will be returned.
Otherwise, the message contents will be returned.

**NOTE:** Global Messages were a feature of AGS 2.x and are now
obsolete. You will not need to use this property in new games.

Example:

    String message = Game.GlobalMessages[997];
    Display("Global message 997 says: %s", message);

will display global message 997.

---

### `Game.GlobalStrings`

*(Formerly known as GetGlobalString, which is now obsolete)*<br>
*(Formerly known as SetGlobalString, which is now obsolete)*

    static String Game.GlobalStrings[index]

Gets/sets global string *index*. Global strings provide you with an easy
way to share string variables between scripts. There are 50 available
global strings, with *index* values from 0 to 49.

Example:

    Game.GlobalStrings[15] = "Joe";
    Display("Global string 15 is now: %s", Game.GlobalStrings[15]);

will set global string 15 to contain \"Joe\".

*See Also:* [GetGlobalInt](Globalfunctions_General#getglobalint),
[SetGlobalInt](Globalfunctions_General#setglobalint)

---

### `Game.GUICount`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Game.GUICount

Returns the number of GUIs in the game.

This is useful for script modules if you need to iterate through all the
GUIs for some reason. Valid GUIs are numbered from 0 to GUICount minus
1.

Example:

    Display("The game has %d GUIs.", Game.GUICount);

---

### `Game.IgnoreUserInputAfterTextTimeoutMs`

    static int Game.IgnoreUserInputAfterTextTimeoutMs;

Gets/sets the length of time for which user input is ignored after some
text is automatically removed from the screen.

When AGS is configured to automatically remove text after a certain time
on the screen, sometimes the player might try to manually skip the text
by pressing a key just as it is removed automatically, and thus they end
up skipping the next text line by accident. This property is designed to
eliminate this problem.

This property is specified in milliseconds (1000 = 1 second), and is set
to 500 by default.

Example:

    Game.IgnoreUserInputAfterTextTimeoutMs = 1000;

will tell AGS to ignore mouse clicks and key presses for 1 second after
text is automatically removed from the screen.

*Compatibility:* Supported by **AGS 3.2.0** and later versions.

*See Also:*
[Game.MinimumTextDisplayTimeMs](Game#gameminimumtextdisplaytimems),
[Game.TextReadingSpeed](Game#gametextreadingspeed),
[Speech.SkipStyle](Speech#speechskipstyle)

---

### `Game.InSkippableCutscene`

*(Formerly known as game.in_cutscene, which is now obsolete)*

    static bool Game.InSkippableCutscene

Returns whether the game is currently between a StartCutscene and
EndCutscene, and therefore whether the player is able to skip over this
part of the game.

When the player chooses to skip a cutscene all of the script code is run
as usual, but any blocking commands are run through without the usual
game cycle delays. Therefore, you should never normally need to use this
property since cutscenes should all be handled automatically, but it
could be useful for script modules.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example below.

Example:

    if (Game.InSkippableCutscene)
    {
      Display("The player might never see this message!");
    }

will display a message if we are within a cutscene

*Compatibility:* Supported by **AGS 3.0.1** and later versions.

*See Also:* [StartCutscene](Globalfunctions_General#startcutscene),
[EndCutscene](Globalfunctions_General#endcutscene),
[Game.SkippingCutscene](Game#gameskippingcutscene)

---

### `Game.InventoryItemCount`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Game.InventoryItemCount

Returns the number of inventory items in the game. This is the total
number of items that you created in the Inventory Items pane of the
editor, not how many the player is currently carrying.

Example:

    Display("The game has %d inventory items.", Game.InventoryItemCount);

---

### `Game.MinimumTextDisplayTimeMs`

    static int Game.MinimumTextDisplayTimeMs;

Gets/sets the minimum length of time that text is displayed on the
screen. AGS automatically adjusts the length of time that text is
displayed for depending on the length of the text (and you can customize
this calculation with
[Game.TextReadingSpeed](Game#gametextreadingspeed)), but for very
short statements like \"Hi!\", you might want the text to remain for
longer.

This property is specified in milliseconds (1000 = 1 second), and is set
to 1000 by default.

**NOTE:** This property is ignored if lip-sync is enabled, or if the
General Settings are set not to allow text to be automatically removed.

Example:

    Game.MinimumTextDisplayTimeMs = 2000;

will ensure that even the shortest \"Hi!\" text line will be displayed
for at least 2 seconds

*Compatibility:* Supported by **AGS 3.1.2** and later versions.

*See Also:*
[Character.SpeechAnimationDelay](Character#characterspeechanimationdelay),
[Game.IgnoreUserInputAfterTextTimeoutMs](Game#gameignoreuserinputaftertexttimeoutms)
[Game.TextReadingSpeed](Game#gametextreadingspeed)

---

### `Game.MouseCursorCount`

    readonly static int Game.MouseCursorCount

Returns the number of mouse cursors in the game.

This is useful for script modules if you need to iterate through all the
cursors for some reason.

Example:

    Display("The game has %d cursors.", Game.MouseCursorCount);

---

### `Game.Name`

    static String Game.Name

Gets/sets the game's name. This is initially set in the General
Settings pane of the editor, but you can change it at run-time in order
to change the window title of your game.

Example:

    Display("The game name is: %s", Game.Name);

will display the game name.

*See Also:* [Game.FileName](Game#gamefilename)

---

### `Game.NormalFont`

*(Formerly known as global function SetNormalFont, which is now
obsolete)*

    static FontType Game.NormalFont

Gets/sets the font used for all in-game text, except speech. The font
number must be a valid number from the Fonts pane of the editor.

More specifically, AGS uses the Normal Font for the following:

-   Display
-   DisplayTopBar
-   dialog options text
-   the built-in save and restore dialogs

The Normal Font is font 0 by default.

Example:

    Game.NormalFont = eFontSpecial;

will change the normal font to the font \"Special\".

*See Also:* [Game.SpeechFont](Game#gamespeechfont)

---

### `Game.SkippingCutscene`

*(Formerly known as game.skipping_cutscene, which is now obsolete)*

    static bool Game.SkippingCutscene

Returns whether the player has elected to skip the current cutscene.
This will return true if the game is between a StartCutscene and
EndCutscene command, and the player has chosen to skip it.

Although cutscene skipping is handled automatically by AGS, you can use
this property to optimize the process by bypassing any lengthy blocks of
code that don't need to be run if the cutscene is being skipped over.

**NOTE:** This is a static function, and thus need to be called with
`Game.` in front of it. See the example below.

Example:

    if (!Game.SkippingCutscene)
    {
      aScaryMusic.Play();
      Wait(100);
      Game.StopAudio();
    }

will only attempt to play the music if the player is not skipping the
cutscene.

*Compatibility:* Supported by **AGS 3.0.1** and later versions.

*See Also:* [StartCutscene](Globalfunctions_General#startcutscene),
[EndCutscene](Globalfunctions_General#endcutscene),
[Game.InSkippableCutscene](Game#gameinskippablecutscene)

---

### `Game.SpeechFont`

*(Formerly known as global function SetSpeechFont, which is now
obsolete)*

    static FontType Game.SpeechFont;

Gets/sets the font used for character speech. The font number you supply
must be a valid number from the Fonts pane of the editor.

The Speech Font is font 1 by default.

Example:

    Game.SpeechFont = eFontStandard;

will change the speech font to \"Standard\".

*See Also:* [Game.NormalFont](Game#gamenormalfont)

---

### `Game.SpriteHeight`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Game.SpriteHeight[int slot]

Returns the height of the specified sprite.

The height will be returned in the original sprite pixels (without any scaling).
If an invalid sprite slot is supplied, 0 will be returned.

Example:

    Display("Object 0's sprite is sized %d x %d.", Game.SpriteWidth[object[0].Graphic],
                                                   Game.SpriteHeight[object[0].Graphic]);

*See Also:* [Game.SpriteWidth](Game#gamespritewidth)

---

### `Game.SpriteWidth`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Game.SpriteWidth[int slot]

Returns the width of the specified sprite.

The width will be returned in the original sprite pixels (without any scaling).
If an invalid sprite slot is supplied, 0 will be returned.

Example:

    Display("Object 0's sprite is sized %d x %d.", Game.SpriteWidth[object[0].Graphic],
                                                   Game.SpriteHeight[object[0].Graphic]);

*See Also:* [Game.SpriteHeight](Game#gamespriteheight)

---

### `Game.TextReadingSpeed`

*(Formerly known as game.text_speed, which is now obsolete)*

    static int Game.TextReadingSpeed;

Gets/sets the speed at which AGS assumes the player can read text, and
therefore how long speech stays on the screen before it is automatically
removed.

Specifically, the TextReadingSpeed is the number of characters of text
that the player can read in a second. It is 15 by default. A higher
number will therefore lead to the text being removed more quickly.

It is useful to link this setting to a GUI Slider on some sort of
Control Panel GUI so that the player can adjust it depending on their
reading speed.

**NOTE:** This property is ignored if lip-sync is enabled, or if the
General Settings are set not to allow text to be automatically removed.

Example:

    Game.TextReadingSpeed = 7;

sets the text reading speed to half the default, which will leave speech
on-screen for twice as long as usual.

*Compatibility:* Supported by **AGS 3.1.2** and later versions.

*See Also:*
[Character.SpeechAnimationDelay](Character#characterspeechanimationdelay),
[Game.MinimumTextDisplayTimeMs](Game#gameminimumtextdisplaytimems),
[Speech.SkipStyle](Speech#speechskipstyle)

---

### `Game.TranslationFilename`

*(Formerly known as GetTranslationName, which is now obsolete)*

    readonly static String Game.TranslationFilename;

Gets the name of the current translation filename (without the \".tra\"
extension). This may be useful if you want to use a different graphic
somewhere depending on which translation is being used.

If no translation is in use, a blank string is returned.

Example:

    if (Game.TranslationFilename == "German") {
      Display("You are using the German translation.");
    }

*See Also:*
[Game.ChangeTranslation](Game#gamechangetranslation),
[GetTranslation](Globalfunctions_General#gettranslation),
[IsTranslationAvailable](Globalfunctions_General#istranslationavailable),
[Translation Manual](Translations)

---

### `Game.UseNativeCoordinates`

    readonly static bool Game.UseNativeCoordinates

Returns whether the game is using native co-ordinates. If native
co-ordinates are in use, then all X, Y, Top, Bottom, Width and Height
variables in the game will be expected to reflect the resolution of the
game.

If this is *false*, then the game is operating in backwards-compatible
mode where all co-ordinates are low-res.

If the game resolution is 320x200 or 320x240, this setting has no
effect.

This property is read-only; it is not possible to change this setting at
run-time.

Example:

    if (Game.UseNativeCoordinates)
    {
      Display("The player is at %d, %d -- REALLY!", player.x, player.y);
    }
    else
    {
      Display("The player is at %d, %d in the old-school system", player.x, player.y);
    }

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

---

### `Game.ViewCount`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Game.ViewCount

Returns the number of views in the game.

This is useful for script modules if you need to iterate through all the
views for some reason. Valid views are numbered from 1 to ViewCount.

Example:

    Display("The game has %d views.", Game.ViewCount);
