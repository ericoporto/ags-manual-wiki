## Engine Plugin Design-time API

Since the AGS Editor is currently windows only, you can use a macro to not include the design-time parts when building the plugin for other platforms.

### DllMain

Your DLL should have the following entry points:

The standard Windows DLL entry point, you know how to use this.

This will get called once when the editor first starts up, and once when it finally shuts down. The plugins are kept in memory at all times, so you will not get lots of load-unloads during the editor's lifetime.

### Design-time events

#### AGS_GetPluginName
```
DLLEXPORT LPCSTR AGS_GetPluginName ();
```

Called by the editor to retrieve a user-friendly name for the plugin. This is the very first function the editor calls as soon as it starts up, in order to build its list of plugins.

Normally, you will implement this as a simple one-line function that returns a static string with the plugin description.

#### AGS_EditorStartup
```
DLLEXPORT int AGS_EditorStartup (IAGSEditor *lpEditor);
```

Called by the editor when the user selects to add the plugin to their game. This function should perform any initialization necessary for design-time operation.

The parameter passed to the function is a pointer to the editor interface, which your plugin can execute various methods on to communicate with the editor.

In particular, this function should register any additions to the script header files that it uses.

You should return 0 to indicate success; any other value indicates that a problem occurred, and the editor will not attempt any further communication with the plugin unless the user tries to start it again.

#### AGS_EditorShutdown
```
DLLEXPORT void AGS_EditorShutdown ();
```

Called by the editor when the user elects to remove the plugin from their game. The plugin should un-register anything that it registered at startup, since if the user later decides to add the plugin again, the Startup function will be run again.

#### AGS_EditorProperties
```
DLLEXPORT void AGS_EditorProperties (HWND parent);
```

_(Optional - plugin does not have to have this function)_

Called by the editor when the user highlights the plugin and clicks the Properties button. You can use this to display a copyright message, or allow the user to set options for your plugin, for instance. This will only be called when the plugin is selected (ie. `EditorStartup` has been called).

The parameter gives you the parent window handle you should use if you want to pop up a dialog. You should make any dialogs modal so that this function does not return until they are dismissed.

#### AGS_EditorSaveGame
```
DLLEXPORT int AGS_EditorSaveGame (char *buffer, int bufsize);
```

_(Optional - plugin does not have to have this function)_

Called by the editor when the current game is saved to disk. This will only be called if your plugin is selected into the current game.

`buffer` is a byte array of size `bufsize`, which you can write any data to as you see fit. The buffer will then be written into the user's game file. You must return the number of bytes actually used, which can be up to and including `bufsize`.

If you need more storage space than `bufsize` provides, you will have to write your own separate file out to disk, store in the registry, or do some compression.

The current version of AGS gives you a 5120 byte buffer, but future versions may increase or decrease this amount, so be sure to check `bufsize` before using it.

You will probably only need this function if you have some options in the Properties that the user can set, otherwise there's no need to use it.

#### AGS_EditorLoadGame
```
DLLEXPORT void AGS_EditorLoadGame (char *buffer, int bufsize);
```

_(Optional - plugin does not have to have this function)_

Called by the editor when a game is loaded from disk. This will only be called if your plugin is selected into the new game.

`buffer` is a byte array of size `bufsize`, which contains any data you wrote out in a previous session with `AGS_EditorSaveGame`. Note that the buffer is not persistent - when your function returns, the buffer is freed, so you should copy any important data you need to elsewhere.

#### AGS_PluginV2
```
DLLEXPORT int AGS_PluginV2 ();
```

This entry point is never called by AGS, but it must be present and exported from your DLL in order to let AGS know that it is a valid plugin that supports version 5 and later of the engine interface. If you don't export this, AGS won't load the plugin.

### The IAGSEditor interface

This interface is provided to the plugin as the way of calling back to the editor. It provides these members:

#### IAGSEditor.version
```
int version;
```

Specifies the interface version. You should check this to determine what version of the editor is being used, because certain interface methods will have been added in later versions, and attempting to use them with an earlier version will crash the system.

The current version number for the latest version of AGS is **1**.

#### IAGSEditor.GetEditorHandle
```
HWND GetEditorHandle ();
```

Returns the window handle to the AGS Editor's main frame. This might be useful if you wanted to add extra menu options to the editor, for example.

_Added in version: 1_

#### IAGSEditor.GetWindowHandle
```
HWND GetWindowHandle ();
```

Returns the window handle to the current active window. If you want to pop up a messagebox, for instance, you should always use this handle as the parent, because using the main frame's handle would un-modal any dialog boxes currently displayed.

_Added in version: 1_

#### IAGSEditor.RegisterScriptHeader
```
void RegisterScriptHeader (const char * header);
```

Adds the contents of `header` to the built-in script header, which is compiled into every script in the game. The idea here is that you would use this to register your text script functions, for example:

```
char *header = "import int Add (int, int);
                import int Substract(int, int); ";
RegisterScriptHeader (header);
```

Note that the editor only keeps a reference to this string rather than a copy, so do not overwrite or destroy the string after calling this function.

_Added in version: 1_

#### IAGSEditor.UnregisterScriptHeader
```
void UnregisterScriptHeader (const char *header);
```

Unregisters the specified script header, which you earlier used with `RegisterScriptHeader`.

_Added in version: 1_
