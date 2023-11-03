## Default Setup

The Default Setup pane lets you create the default runtime configuration for your game. This configuration is saved as "acsetup.cfg" into the Compiled folder.

Since *AGS 3.6.0* the config file in the Compiled folder is created by merging "Default Setup" properties with an optional "acsetup.cfg" file found in the game project's folder, if one is present. This is done to allow game developers provide their own custom settings. In such case the custom file also overrides any options matching ones in Default Setup pane.

For information on possible "acsetup.cfg" contents please refer to the [related topic](EngineConfigFile).

**NOTE:** please be aware that the default game's config cannot be modified using game's [setup utility](Setup) (aka "winsetup.exe"), because that program modifies config file in the user's personal documents folder instead. The setup utility may be useful to quickly test various options, but config file for your game's distribution will be created from "Default Setup" pane anyway.

Additionally, following settings are available:

**Setup appearance**

-   **Title text** - the text that will appear on the title of the setup
    program window.

**Environment**

-   **Custom game saves path** - defines where game will store its saves
    and individual user's files (e.g. achievements). This path will be
    used to substitute default value of `$SAVEGAMEDIR$` token
    in scripts. Note that when being set up in the Editor, this option
    only accepts relative paths (when used they will be relative to the
    game's location). This has to be done this way to prevent setting
    absolute path that does not exist on the player's machine, so
    typically you have to set this if you want to have saves stored
    locally within the game's folder. Players will be able to modify
    this path in setup program (where they are actually allowed to put
    absolute paths too).
-   **Custom shared data path** - defines where game will store its
    shared data files (e.g. hi-score tables). This path will be used to
    substitute default value of `$APPDATADIR$` token in scripts. Note
    that this option only accepts relative paths, so typically you have
    to set this if you want to have data files created locally within
    the game's folder. Players will be able to modify
    this path in setup program.

**IMPORTANT:** what you set on this page is a default game configuration,
but it may be overridden by a user config. If you have run your game's setup
program at least once and chose to save, that created a user config file
[in its own location](EngineConfigFile#configuration-file-locations). 
Since then changing Default Setup won't be enough to affect your game,
you'd also have to change user config by running setup program again.
You may also delete user config file (that is safe thing to do), which
will reset settings back to default config and let you test it out.

**IMPORTANT:** the configuration file will only be recreated during next
game compilation, so if you change these settings you will need to
rebuild your game one more time to apply them.

*See also:* [Run-time engine setup](Setup), [Config file locations](EngineConfigFile#configuration-file-locations)