## Plugins

AGS supports user-written plugins in order to provide functionality to
your game that AGS itself does not support.

The plugin developer's guide is available from the Resources section of
the AGS website.

Windows plugins come as DLL files with the names `AGS*.DLL`, for example
`agscircle.dll` might be a plugin providing a DrawCircle script function.

**How to use a plugin**

So, you've downloaded a plugin for AGS. What do you do with it? Well,
firstly read any readme file that the plugin author has included. But to
get any plugin to work you must do the following:

1\. Place a copy of the plugin files in the `AGSEditor.exe` directory - not your
game folder.

Ex: `C:\Program Files\Adventure Game Studio 3.5.0\`

![Right click Use plugin](images/Plugins_img1.png)

2\. Start the AGS Editor up, and load your game.
Go to the Plugins node in the main tree.
Open it up, and you should see all available plugins  listed.
To use one in your game, right-click it and choose "Use plugin".
The plugin developer should provide instructions on what to do next.
Save your game to make sure that AGS remembers that you want to use the
plugin.

For other platforms, check [Engine Plugins and other platforms](Plugins#engine-plugins-and-other-platforms) below.

**NOTE:** If you hit a "there was an error loading this plugin" message, there is a chance the problem is with the file Security Zone Identifier, check the [Troubleshooting Windows Zone Identifier](TroubleshootingWindowsZoneID) section. If this doesn't solve your problem, please post in the respective plugin page on the [Modules & Plugins board](https://www.adventuregamestudio.co.uk/forums/index.php?board=10.0) in the forums.

### Engine Plugins and other platforms

While Windows plugins are named `ags*.dll`, other platforms that the AGS Editor supports will use the `libags*.so` convention (ex: `libagsdrawcircle.so`). Once you have your plugins ported, here are the places to put them.

Below directories are mentioned related to the folder containing AGS Editor (`AGSEditor.exe`)

- Windows x86 plugins are placed in the same dir as `AGSEditor.exe`
- Linux plugins can be built for x64 (amd64) and x86 architectures, place them in the corresponding `Linux/lib64` and `Linux/lib32` directories.
- Android plugins should be placed in `Android\plugins`, under a directory for each architecture (ex: `Android\plugins\arm64-v8a\libagsdrawcircle.so`)
- Web port doesn't support plugins currently

Non Windows platforms may support a known set of plugins as stubs, meaning they won't error for the lack of the plugin alone, but you should detect this if you are not adding the plugin and handle accordingly.

### Creating Plugins

If you want to create your own plugin to extend the functionality of either the AGS Editor or what's possible with the AGS Engine, read on the respective links below.

- [Editor Plugins](EditorPlugins)
- [Engine Plugins](EnginePlugins)
  - [Engine Plugin Design-time API](EnginePluginDesign-timeAPI)
  - [Engine Plugin Run-time API](EnginePluginRun-timeAPI)
