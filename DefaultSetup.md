## Default Setup

The Default setup pane lets you create the default runtime configuration
for your game. Since AGS 3.3.5 you cannot directly do that using game's
setup utility (winsetup.exe) anymore, because it modifies config file in
the user's personal documents folder instead of game folder. For that
reason you should be doing it from this Editor's page now.

Most of the options here correspond to the ones you may find in the
setup utility. For their meaning please refer to [related topic](Setup).

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