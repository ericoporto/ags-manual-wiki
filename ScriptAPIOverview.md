## Script API Overview

AGS provides a scripting system, where engine functionalities are exposed through the AGS Script API, allowing you to write a mini-program, giving you great control over your game. You can read and modify room elements by using the structs Room, Object, Hotspot, Region, and the Global functions for Room. If you need your character to say things, receive or lose an inventory item, or walk somewhere, you can find these in the Character struct. AGS camera system is available through the use of Viewport, Camera, and Screen. You can also draw directly with Dynamic Sprites, Drawing Surface and use Overlays to have these sprites shown on screen. Browse around the API topics, as there's much more available to you.

**NOTE:** API stands for "Application Programming Interface". This is a common term, it defines all the means a program (such as AGS engine) provides for user to control it programmatically.

## API switches

When new version of AGS comes with new API entries these may cause conflicts with previously made scripts. Sometimes a function gets deprecated and disabled, or replaced by a different one. Sometimes new function is added that may use name which you already used in your script. Usually it's a good idea to adjust your script and resolve these problems by hand. But if you do not want to or do not have time to do so just yet - there are API switches.

In a nutshell, API switches let you control which parts of API are active in your game.

In the editor these are found in the [General Settings](Settingupthegame#general-settings), in "Backwards Compatibility" category. Relevant ones are:

* **Script API version** - defines the *topmost level* of API. Default is "Highest" which would use topmost supported by this version of AGS. Setting it to any version will lock API at that level, disabling any additions (functions and properties) that were introduced later.
* **Script compatibility level** - defines the *lowest level* of API. Default is "Highest" which again would use only content officially suggested by current version of AGS. Setting it to lower versions would enable older functions that were since deprecated.
* **Enforce object-based scripting** - this is on by default, turning this off would bring back a huge number of obsolete global functions from before AGS 2.7 era. Most of these were replaced by introducing object structs and properties. See [Upgrading to AGS 2.7](UpgradingTo27) for more information.
* **Enforce new-style audio scripting** - this is on by default, turning this off this would reactivate old-style audio functions that were deprecated in AGS 3.2. These functions relied on passing clip numbers instead of using their script names, and support strictly 1 channel per audio type. See [Upgrading to AGS 3.2](UpgradeTo32) for more information.
* **Use old-style custom dialog options API** - this is off by default, and enabling this would switch to pre-AGS 3.4.0 custom dialog option callbacks. See [Upgrading to AGS 3.4](UpgradeTo34) for more information.

Each of above switches defines a macro or number of macros which are then used during script compilation and help detect the state of these switches. You may also use these in your script for example if you want to provide two or more variants of code for different API versions. For more information on this and actual script examples see [Constants](Constants).