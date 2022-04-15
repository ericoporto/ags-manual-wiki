# Editor Preferences

## Android

- **ANDROID_HOME** - The path to your Android SDK directory usually 
  `C:\Users\user\AppData\Local\Android\Sdk`.
  Leave empty if your ANDROID_HOME environment variable is set.

- **JAVA_HOME** - The path to your JRE and JDK directory, usually 
  `C:\Program Files\Android\Android Studio\jre`.
  Leave empty if your JAVA_HOME environment variable is set.

- **Key Alias** - Keystore Key Alias.

- **Key Password** - Keystore Key Password. Must be the same as Keystore Password for now.

- **Keystore File Path** - Your Keystore File absolute path, it's usually a file ending in `.jks` or `.store`.

- **Keystore Password** - Keystore Password. Must be the same as Key Password for now.

- **Use gradle daemon** - Gradle daemon can severily improve building speed, but it may increase ram
  usage even when it's not actively used. 
  If you are recurrently building for Android, consider turning it on to speed build times.

## Editor Appearance

- **Ask before closing multiple tabs** - Prompt dialog on closing multiple tabs.

- **Color Theme** - Select which theme the editor should be using.

- **Editor Startup Action** - What editor should do at startup.

- **Keep Help window on top** - Should Help window always be on top of the Editor window when shown?

- **Pop-up messages on Compile** - In which cases the editor should show pop-up windows when
  compiling.
  
- **Show view preview by default in view editors** - Wheter view preview is always shown when a view
  editor is loaded.

## Import Directory

- **Import Directory** - When you import files, where do you want to look first?

## Import of 8-bit background

- **Remap palette of room backgrounds** - Remap palette of room background into allocated background
  palette slots (8-bit games only).

## Misc

- **Backup Warning Interval** - Interval of days the Editor will warn you should backup your game.

## New Game Directory

- **New Game Directory** - When you create a new game, where do you want it to go?

## Script Editor

- **Indent Uses Tabs** - Should editor use tabs instead of spaces when indenting?

- **Script file modified externally, should it reload?** - If a script is open for editing and is 
  modified by another program, should it reload?

- **Script Font** - Font used in the script editor.

- **Script Font Size** - Size of the font used in the script editor.

- **Script Tip Font** - Font used in description tips in the script editor.

- **Script Tip Font Size** - Size of the font used in description tips in the script editor. Script
  editor line height uses biggest height accross fonts.

- **Tab width** - How many space characters a tab width should be. This setting requires editor 
  restart to be applied.

## Sprite Editor

- **Default image editor** - When you double-click a sprite, what program do you want to use to edit
  it? This program must support PNG and BMP files.

- **Default sprite import transparency** - Sprite transparency import method to use by default.

## Test Game

- **Test Game Style** - A setting if the game should run in window or full-screen when you test it. 
When using F5 game will always run in a window.
