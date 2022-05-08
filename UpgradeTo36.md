## Upgrading to AGS 3.6

AGS version 3.6 is another big change to AGS.
First of all, this release presents a SDL2-based engine. For about 2 decades AGS engine was based on Allegro 4 graphic library, which was discontinued somewhere in the early 2010s, so this is overdue.

Secondly, both the Editor and the Engine have full Unicode support now. This means that you may use any language whatsoever in scripts, object descriptions, and custom properties, as well as translations, - so long as you also provide proper Unicode fonts.

Then, we have expanded a list of platforms that the Editor can directly build the game for: now this includes Android and Web (Emscripten).

Below we'll look into these and other significant changes in more detail.

### Unicode support

AGS can now work in Unicode mode, but for backward compatibility, we have to support ASCII mode too. We recommend using Unicode mode when starting new projects, regardless of the game language.

When in Unicode mode, all game texts and text files, such as scripts, are saved in UTF-8 format.

In the Editor the switch between two modes is called **"Text format"** and is located in "General Settings".

**IMPORTANT:** This switch is an important choice and should not be played with at random. Whenever you change the text format Editor will convert all your game files by loading them and saving them back using a new mode. If all your game texts were using the standard Latin alphabet (English, etc), then you should not see any difference, but if you had texts with extended Latin characters or any other non-Latin languages, - these will be converted between ANSI and UTF-8. We strongly recommend doing a full project backup before doing this though.

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

The Translations are not affected by the game's setting and have an individual setting of their own. When you open TRS file made by the new version, it will have "#Encoding" option in the file's header. This is where you may write either "UTF-8" or "ASCII" by hand to tell the translation compiler (and the engine) how this translation should be interpreted. By default this should be "UTF-8", so you only need to change this if you need translation to be in ASCII for some reason.
If you have imported an older project and TRS file does not have this option, then you may add one yourself. Just remember that TRS options must be preceded with a comment sign, like this:

    //#Encoding=UTF-8

Don't forget to save TRS in UTF-8 with whatever text editor you are using, if you want it to keep Unicode texts intact.

The engine can run the game in both Unicode and ASCII modes. It uses a game setting to set up the mode on start, but when loading a translation it will switch to the translation's setting. This behavior is meant primarily to allow adding UTF-8 translations for older ASCII games.

**NOTE:** the engine cannot convert older ASCII games to Unicode at runtime, primarily because it does not know the exact codepage its texts were made in. So if you want your older game to fully work in Unicode, the proper way is to upgrade its project and compile the game anew.

### Changes to key input handling

As a part of the Unicode support, and also to make key handling in the script more consistent, the script callbacks for key input were extended.

First of all, the `on_key_press` function now supports a second optional argument `mod`. It's optional, so you don't have to declare it, but if you do then you'll get its benefits.

The extended function definition now is:

    function on_key_press(eKeyCode key, int mod)

The `mod` argument describes which key modifiers were enabled when this exact key was pressed. It's different from, for example, using `IsKeyPressed()` in `repeatedly_execute` callback, because the engine may receive several key-presses between two game frames, while `IsKeyPressed` only tells the last state of the key. Using `mod` argument is 100% reliable.

But the `mod` contains *set of flags*, and is slightly more complicated: as you should not use regular comparison (==, !=) with it, but bitwise operator (&):

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

### Deprecated / replaced script functions

obsolete function | replace with
-- | --
Object.IgnoreScaling | Object.ManualScaling

### System limits update

* Max number of AudioChannels is now 16 (was 8).
* Removed game Cursors limit (was 20).
* Removed Overlays limit (was 20).
* Removed limit of simultaneous Button animations (was 15).
* Removed limit of Character followers (was 30).
