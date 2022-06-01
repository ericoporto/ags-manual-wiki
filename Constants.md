## Constants

The following predefined macros and constants are available in your scripts:

Name | Description
--- | ---
DEBUG | Defined if the game is being compiled in debug mode, not defined otherwise
SCRIPT_API_vXXX | Defined if corresponding version of script API is enabled (e.g. SCRIPT_API_v340)
SCRIPT_COMPAT_vXXX | Defined if certain compatibility level is enabled (e.g. SCRIPT_COMPAT_v321)
STRICT | Defined if "Enforce Object Based Scripting" is enabled, not defined otherwise
STRICT_STRINGS | Defined if "Enforce new-style strings" is enabled, not defined otherwise
STRICT_AUDIO | Defined if "Enforce new-style audio scripting" is enabled, not defined otherwise
LRPRECEDENCE | Defined if "Left-to-right operator precedence" is enabled, not defined otherwise
AGS_NEW_STRINGS | Defined if AGS 2.71 or later (with new-String support), not defined otherwise
NEW_DIALOGOPTS_API | Defined if "Use old-style dialog options rendering API" is disabled
NEW_KEYINPUT_API | Defined if "Use old-style key handling" is disabled
AGS_SUPPORTS_IFVER | Defined if AGS 2.72 or later (with `#ifver` support), not defined otherwise
AGS_MAX_INV_ITEMS | The maximum number of inventory items
AGS_MAX_OBJECTS | The maximum objects per room
AGS_MAX_HOTSPOTS | The maximum hotspots per room
AGS_MAX_REGIONS | The maximum regions per room
MAX_LISTBOX_SAVED_GAMES | Limit of save files filled into ListBox when using [`FillSaveGameList`](ListBox#listboxfillsavegamelist)
PALETTE_SIZE | Size of game palette, for 256-color mode

You can check for whether a macro is defined or not by using the
`#ifdef` and `#ifndef` keywords:

    #ifndef STRICT
      // only compile the MoveCharacter command if not using object-based scripting
      MoveCharacter(EGO, 30, 40);
    #endif
    #ifdef DEBUG
      // only display this when the game is compiled in debug mode
      Display("Debugging information");
    #endif

There is also an `#error` directive you can use to stop the script
compiling:

    #ifndef AGS_NEW_STRINGS
    #error This script requires at least AGS 2.71
    #endif

If you'd like to know if a new API is available, test for the corresponding SCRIPT_API_vXXX constant:

    #ifdef SCRIPT_API_v360
    // can use new code added in 3.6.0
    #endif

If on contrary you need to know if a deprecated API is enabled, test for the corresponding SCRIPT_COMPAT_vXXX constant:

    #ifdef SCRIPT_COMPAT_v320
    // can use old code, deprecated after 3.2.0
    #endif

The other constants `AGS_MAX_*` are useful if you are writing some
script code that you want to be portable to different versions of AGS,
and to pick up the limits from the user's AGS version. For example, if
you wanted to store some extra information on all the inventory items,
you could do:

    int invWeights[AGS_MAX_INV_ITEMS];

To get the actual number of things in the game rather than the AGS
limit, use the
[`Game.CharacterCount`](Game#gamecharactercount)-style properties.
