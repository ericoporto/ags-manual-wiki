## Editor Command Line Options

Running AGS Editor from the command line can be useful for automation purposes.

We will use `cmd.exe` here, but you can call AGS Editor from other command lines, though they may require special handling.

**NOTE:** If you are using the MSYS2 bash prompt on Windows, remember that `/` command flags need two slashes. (e.g. use `AGSEditor.exe //compile my-project/Game.agf`).


### Opening the Editor

You can open the Editor in the command line by simply calling its executable and passing the path to it.

```cmd
C:\path\to\AGSEditor.exe
```

We won't use the full path in the rest of the text, but you still need to either pass it, put your AGS Editor folder in your system PATH, or change the directory to it before.

You can also open the editor in a specific project by passing your project's `Game.agf` location.

```cmd
AGSEditor.exe path\to\Game.agf
```

As an example, in Windows, you can create a shortcut for the AGS Editor and edit its properties to put your `Game.agf` there so you can create a shortcut that opens AGS Editor in your project.


### Compile Flag

This flag will load the AGS Editor in your project, compile it, and exit.

```cmd
AGSEditor.exe /compile path\to\Game.agf
```

Outputs that would normally be a message box or in the output panel will instead be printed in the command line. A successful compilation will have exit code 0, and any error will give a non-zero exit code.

This option can be used for automation purposes, you could use it to build your AGS Game in a Continuous Integration pipeline.
