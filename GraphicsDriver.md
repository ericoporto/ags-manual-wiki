## Graphics driver selection

AGS supports three graphics drivers: Software, Direct3D and OpenGL. Software driver is available on any system, Direct3D may be used on Windows only, OpenGL on most systems but its actual performance depends on the installed system components.

Software is the 'classic' software graphics driver, that AGS has used
ever since the initial Windows version was released. It draws whole game a single surface using software method, and that surface is then rendered as a texture in the game window, scaled as necessary. Only the final texture render is performed using graphics card (GPU), but the main bulk of work is done on your CPU, where the rest of the game is processed. It's perfectly fine for simple low-resolution games that don't use many large sprites or graphical effects (such as scaling, tinting or alpha blending), but may be burdensome to your computer when running high-resolution games or games with many simultaneous sprites on screen.

Software driver is currently the only driver that fully supports 8-bit dynamic palette effects. But in any other case it is the last resort if nothing else works for any reasons.

Direct3D and OpenGL drivers are relying on your graphics card (GPU) and hardware acceleration. This means that the game will run a lot faster for high-resolution games, and if your game uses features such as object scaling, tinting and alpha blending.

OpenGL is the primary choice on multiple unix systems (Linux, Mac, Android, iOS), and may be equally used on most Windows systems. On Windows OpenGL is is not strictly linked to particular version of DirectX, thus it may work where Direct3D failed for compatibility reasons. Other than that, it should not have any significant performance differences from the former.

No matter which you choose as your default graphics driver, the player can always run the Setup program, or edit the config file, and switch to using the other driver.

### System Requirements

**Software**<br>
Software driver choses the final output method based on what's available on the user's system. It may be DirectX, OpenGL, or native graphics output if nothing else is available (for example - GDI on Windows). Therefore it will almost certainly work everywhere.

**Direct3D**<br>
Any Windows-based PC with at least DirectX 9.0 and higher, and a contemporary graphics card.

**OpenGL**<br>
Your graphics card drivers should provide support for OpenGL 3.0 or higher for the game visuals to have full functionality.

*See also:* [System.HardwareAcceleration property](System#systemhardwareacceleration)
