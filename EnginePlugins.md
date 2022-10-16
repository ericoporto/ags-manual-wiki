## Engine Plugins

AGS supports a plugin interface, whereby you can write your own add-ons if AGS doesn't support all the features you need.

AGS supports two different types of plugins - plain API plugins, for writing plugins that add extra functionality to games and need to be included with the games at runtime; and .NET plugins, for enhancing the editor. Editor .NET plugins are explained on [this separate page](EditorPlugins); here we will continue talking about the plain API.

**IMPORTANT:** Plugins are **non-portable**. This means that if you write a plugin, you will not be able to compile a Linux version of any game that uses the plugin, unless you supply a Linux version of it yourself, and same for other platforms.

**Supported compiler per platform**
These follows the compilers used for the binaries of the Engine:
- MSVC on Windows
- GCC on Linux
- Other platforms don't have binaries provided with the editor, but currently are built with Clang.

Now, if you want to continue, on to the technical details.

AGS plugins are implemented as Windows DLL files, which must have filenames beginning with "AGS". Therefore, you will need to create your plugin as a standard Windows DLL project. When the editor starts up, it reads through all the `ags*.dll` files in the editor directory, and adds them to its plugin list. More information [about _using_ plugins in this page](Plugins).

The plugin can be started in two modes - design-time and run-time. Design-time mode is used when the plugin is loaded by the AGS Editor, and Run-time mode is used when the game is actually run.

- [Engine Plugin Design-time API](EnginePluginDesign-timeAPI)
- [Engine Plugin Run-time API](EnginePluginRun-timeAPI)
