## Upgrading to AGS 3.6

AGS version 3.6 is another big change to AGS.
First of all, this release presents a SDL2-based engine. For about 2 decades the AGS engine was based on the Allegro 4 graphic library, which was discontinued somewhere in the early 2010s, so this is overdue.

Secondly, both the Editor and the Engine have full Unicode support now. This means that you may use any language whatsoever in scripts, object descriptions, and custom properties, as well as translations, - so long as you also provide proper Unicode fonts.

Then, we have expanded a list of platforms that the Editor can directly build the game for: now this includes Android and Web (Emscripten).

Below we'll look into these and other significant changes in more detail.

### Unicode support

AGS can now work in Unicode mode, but we also support ASCII mode for backward compatibility. We recommend using Unicode mode when starting new projects, regardless of the game language.

When in Unicode mode, all game texts and text files, such as scripts, are saved in UTF-8 format.

In the Editor the switch between the two modes is called **"Text format"** and is located in "General Settings".

**IMPORTANT:** This switch is an important choice and should not be played with at random. Whenever you change the text format the Editor will convert all your game files by loading them and saving them back using a new mode. If all your game texts were using the standard Latin alphabet (English, etc), then you should not see any difference, but if you had texts with extended Latin characters or any other non-Latin languages, - these will be converted between ANSI and UTF-8. We strongly recommend doing a full project backup before doing this though.

When in Unicode mode you may type your game texts in any language whatsoever. This refers to the following:
* Human texts in-game options: such as object descriptions, and so on;
* Values of String Custom properties and Global Variables;
* String literals in scripts (any text in double-quotes);
* Character literals in a script (a character in single quotes);
* Speech lines in dialog scripts;
* Translations.

Mixing multiple languages, even in the same string, is fine (but requires having fonts that can display all of these languages).

Where Unicode won't work (and is not supposed to):
* Script names of game objects: characters, guis, views, and so on;
* Names of Custom properties and Global Variables;
* Variable names and function names in script.

All the above must be written strictly in the Latin alphabet.

String variables and related functions should work seamlessly with Unicode texts. Functions that work with characters were changed to have arguments and return values as `int`, to be able to pass any Unicode character. This includes AppendChar(), ReplaceChar() and String.Char[] property. Also, `String.Format("%c", n)` will now be able to print Unicode characters.

The Translations are not affected by the game's setting and have an individual setting of their own. When you open a TRS file made by the new version, it will have an "#Encoding" option in the file's header. This is where you may write either "UTF-8" or "ASCII" by hand to tell the translation compiler (and the engine) how this translation should be interpreted. By default this should be "UTF-8", so you only need to change this if you need the translation to be in ASCII for some reason.
If you have imported an older project and the TRS file does not have this option, then you may add one yourself. Just remember that the TRS options must be preceded with a comment sign, like this:

    //#Encoding=UTF-8

Don't forget to save the TRS in UTF-8 with whatever text editor you are using, if you want it to keep Unicode texts intact.

The engine can run the game in both Unicode and ASCII modes. It uses a game setting to set up the mode on start, but when loading a translation it will switch to the translation's setting. This behavior is meant primarily to allow adding UTF-8 translations for older ASCII games.

**NOTE:** the engine cannot convert older ASCII games to Unicode at runtime, primarily because it does not know the exact codepage its texts were made in. So if you want your older game to fully work in Unicode, the proper way is to upgrade its project and compile the game anew.

### Changes to key input handling

As a part of the Unicode support, and also to make key handling in the script more consistent, the script callbacks for key input were extended.

First of all, the `on_key_press` function now supports a second optional argument `mod`. It's optional, so you don't have to declare it, but if you do then you'll get its benefits.

The extended function definition now is:

    function on_key_press(eKeyCode key, int mod)

The `mod` argument describes which key modifiers were enabled when this exact key was pressed. It's different from, for example, using `IsKeyPressed()` in `repeatedly_execute` callback, because the engine may receive several key-presses between two game frames, while `IsKeyPressed` only tells the last state of the key. Using `mod` argument is 100% reliable.

But the `mod` contains *set of flags*, and is slightly more complicated: as you should not use regular comparison (==, !=) with it, but a bitwise operator (&):

    // these two conditions check that ctrl was pressed (these commands are equivalent)
    if (mod & eKeyModCtrl)
    if (mod & eKeyModCtrl != 0)
 
    // these two conditions check that ctrl was NOT pressed (again, two variants of the same check)
    if (!(mod & eKeyModCtrl))
    if (mod & eKeyModCtrl == 0)

Here's the full list of mod constants:

constant | meaning
-- | --
eKeyModShiftLeft | left shift key
eKeyModShiftRight | right shift key
eKeyModShift | any of the shift keys
eKeyModCtrlLeft | left control key
eKeyModCtrlRight | right control key
eKeyModCtrl | any of the control keys
eKeyModAltLeft | left alt key
eKeyModAltRight | right alt key
eKeyModAlt | any of the alt keys  
eKeyModNum | numlock key
eKeyModCaps | capslock key

The engine now supports "new style" key handling mode and "old style" mode. There's a **"Use old-style key handling"** option in the "Backwards compatibility" group that lets you choose either old or new key handling mode. This will be "off" (meaning - new mode) by default but will be enabled (meaning - old mode) when you import older projects. If you like to use the new mode you'll need to disable this setting.
What is the difference between the two modes?

**Old (classic) key mode:**
 - lone mod keys (Ctrl, Alt, Shift) are not passed further into the engine nor script, thus `on_key_press` is not called for them;
 - key + mod combinations are merged into one key code for the `on_key_press` callback: e.g. `eKeyCodeCtrlA` and similar key code;

**New key mode:**
 - all keys are passed into the engine and `on_key_press` function as-is, one by one: for example, if you press Ctrl + Z, then you get **two** `on_key_press` calls, one with `eKeyCtrlLeft` and another with `eKeyZ` argument.
 - the new `on_text_input` script function will be active and receive **printable characters**;

In the new mode each key pressed triggers `on_key_press`, and when the pressed keys form a printable character an `on_text_input` function is called. This function must look simply like this:

    function on_text_input(int ch)

Its argument (`ch`) contains a Unicode character's code. It may be used, for example, to append to a String, or add to the text field or label.

Similarily to the above, `dialog_options_key_press` had been expanded with the third `mod` argument:

    function dialog_options_key_press(DialogOptionsRenderingInfo *info, eKeyCode keycode, int mod)

And there's now `dialog_options_text_input` callback for receiving unicode chars during the custom dialog options state:

    function dialog_options_text_input(DialogOptionsRenderingInfo *info, int ch)

### New game package options

AGS now allows to package custom files into your game, and read them in script. An option called "Package custom data folder" has been added to the [General Settings](GeneralSettings). This option accepts a comma-separated list of subfolder names, which should be found in your game project's folder. All of the files in these subfolders will be added to the game package under their relative paths (e.g. "UserData/myfile.dat").

Any [File functions](File) that accept file paths can now refer to the game package files using new `$DATA$` location tag. Virtually any packaged file may be queried this way, whether custom or regular game resource. These files may only be opened for reading however, never for writing.

For example, you may read your custom file from the package as:

    File* f = File.Open("$DATA$/UserData/myfile.dat", eFileRead);

### Multiple speech voxes

AGS now supports having multiple speech vox files. This may be useful if you, for example, would like to provide separate voice-over packs for each language (translation) in your game. Creating additional voxes is done by creating subfolders in "Speech" folder and placing sound files there. AGS will then generate a file called "sp_NAME.vox" for each such subfolder, where "NAME" is subfolder's name.

In script you may switch between the speech packs using new `Game.ChangeSpeechVox()` function. Its value is not linked with the textual translation, which is set by `Game.ChangeTranslation()`. You may enable voice-over matching the language of the text, or on contrary allow player to choose different languages for the text and for the voice. For example:

    Game.ChangeTranslation("Spanish");
    Game.ChangeSpeechVox("English");

Above will change textual translation to "Spanish", and voice-over to "sp_english.vox" pack.

### New sprite compression options

First of all, the old "Compress the sprite file" option in [General Settings](GeneralSettings) has been replaced with "Sprite file compression", which lets to choose one of the supported compression types. Previous common sprite compression in AGS is called "RLE"; an "LZW" compression was added for selection. It's possible that this list will be extended in the future.

Secondly, there's now a "Enable sprite storage optimization" option, which is enabled by default. This option permits the Editor to repack sprites in a different storage format, reducing their disk size whenever possible. This option may be used alongside with the sprite compression. Note that this _does not_ change how the sprites work in game, only how they are stored in the game files.

### Multiplatform support extended

Editor can now produce game builds for Android and Web (using Web/Emscripten port). Both require corresponding component installed alongside with the Editor. In addition, for Android builds you'd also have to install Android Studio and configure certain settings in [Editor's Preferences](EditorPreferences) and your game's [General Settings](GeneralSettings). For more information see [Distributing your game](DistGame).

### TTF fonts behavior

Historically AGS applied a "fixup" to TTF fonts that shifted letters down when drawn, which in turn also increased their graphical height. This behavior is now optional, available purely for backwards compatibility, both as a global and per-font setting called "TTF font adjustment". This setting has two values: "Do nothing" and "Resize ascender to the nominal font height". We recommend having "Do nothing" at all times, except when using TTF fonts specifically created or adjusted for older versions of AGS.

Another global setting is "TTF fonts height used in the game logic". This option tells which value to use when calculating text height, line spacing etc. Its value may be either "Nominal height" or "Full graphical height". The difference is that due to font library's behavior the font's graphical height may end up different (usually larger) that the nominal height the font is imported with. While "Nominal height" is a historical default, it's up to your preference which to use.

One long time requested font feature is the automatic outline thickness. Automatic font outline has always been drawn 1px wide, but that was not enough for high-resolution games. Now fonts have a property "AutoOutlineThickness" which lets you set any outline width you need, and "AutoOutlineStyle" which toggles between "Squared" and "Rounded".

### Deprecated / replaced script functions

obsolete function | replace with
-- | --
Object.IgnoreScaling | Object.ManualScaling

### System limits update

* Max number of AudioChannels is now 16 (was 8).
* Max number of Room Objects per room is now 256 (was 40).
* Removed game Cursors limit (was 20).
* Removed Overlays limit (was 20).
* Removed limit of simultaneous Button animations (was 15).
* Removed limit of Character followers (was 30).
