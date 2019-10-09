## `GUI` functions and properties

### `GUI.Centre`

*(Formerly known as CentreGUI, which is now obsolete)*

    GUI.Centre()

Centers the specified GUI in the middle of the screen. Useful if you've
been moving it around with SetPosition and just want to return it to the
center.

Example:

    gControlpanel.Centre();

will center the CONTROLPANEL GUI in the middle of the screen.

*See Also:* [GUI.SetPosition](GUI#guisetposition)

---

### `GUI.Click`

    GUI.Click()

Forces GUI's OnClick event. If there is a script function bound to that
event it will be run, otherwise nothing happens.

**NOTE:** GUI.Click should not to be confused with **static** function
GUI.ProcessClick. GUI.Click is called for specific GUI and does not
impose any other conditions, while GUI.ProcessClick is called for "any
GUI element that happen to be at the given coordinates".

Example:

    gMainMenu.Click();

triggers OnClick event for gMainMenu.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Button.Click](Button#buttonclick),
[GUI.ProcessClick](GUI#guiprocessclick)

---

### `GUI.GetAtScreenXY`

*(Formerly known as GetGUIAt, which is now obsolete)*

    static GUI* GUI.GetAtScreenXY(int x, int y)

Checks whether there is currently a GUI at screen co-ordinates (X,Y). If
there is, returns its GUI. If two GUIs overlap, the front-most one will
be returned - this can be changed with the GUI.ZOrder property.

If there is not currently a displayed, clickable GUI at the location
then *null* is returned. If null is returned, do NOT attempt to call any
methods or use any properties of the GUI (since it does not actually
exist).

**NOTE:** This command will not find any GUIs that are set as
Non-Clickable (i.e. the "Clickable" checkbox not checked).

Example:

    GUI *theGui = GUI.GetAtScreenXY(mouse.x, mouse.y);
    if (theGui == gInventory) {
      Display("Inventory GUI at mouse location.");
    }
    else if (theGui == null) {
      Display("No GUI at mouse location");
    }
    else {
      Display("GUI %d at mouse location.", theGui.ID);
    }

will display the number of the GUI that the mouse is over.

*See Also:*
[GUIControl.GetAtScreenXY](GUIControl#guicontrolgetatscreenxy),
[GUI.ID](GUI#guiid), [GUI.ZOrder](GUI#guizorder)

---

### `GUI.ProcessClick`

    static void GUI.ProcessClick(int x, int y, CursorMode)

Simulates clicking the mouse on the location (X,Y) on the screen, in the
specified cursor mode. This "click" has special behavior in that it
**only affects GUI and GUI controls** under given coordinates. Any
conditions attached to the first interface elements on given coordinates
will be executed. Other game elements (room objects, hotspots,
characters) will be **ignored**.

The available cursor modes are the ones you define on your Cursors tab
(but with eMode prepended to them). Usually these are eModeWalkto,
eModeLookat, etc.

Example:

    ProcessClick(100, 50, eModePointer);

will simulate clicking the mouse on co-ordinates (100, 50) in the
Pointer mode, which will ignore anything but interface.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Mouse.Click](Mouse#mouseclick),
[Room.ProcessClick](Room#roomprocessclick)

---

### `GUI.SetPosition`

*(Formerly known as SetGUIPosition, which is now obsolete)*

    GUI.SetPosition(int x, int y)

Moves the top-left corner of GUI to the new location (X,Y) on the
screen. This allows you to dynamically move GUIs around on the screen
while the game is running. The co-ordinates are screen co-ordinates, not
room co-ordinates, and use the same scale as in the editor.

Example:

    gMyGui.SetPosition(mouse.x, mouse.y);

will move the GUI to the position where the cursor is.

*See Also:* [GUI.Centre](GUI#guicentre),
[GUI.BackgroundGraphic](GUI#guibackgroundgraphic),
[GUIControl.SetPosition](GUIControl#guicontrolsetposition),
[GUI.SetSize](GUI#guisetsize), [GUI.X](GUI#guix),
[GUI.Y](GUI#guiy)

---

### `GUI.SetSize`

*(Formerly known as SetGUISize, which is now obsolete)*

    GUI.SetSize(int width, int height)

Changes the GUI to have the new size WIDTH x HEIGHT

This could be useful for initially hiding an 'Advanced' part of an
options screen and such like.

The size is in the normal 320x200-resolution pixels. Setting the size to
320, 200 will cause the GUI to take up the entire screen.

Example:

    gIconbar.SetSize(160, 100);

changes the ICONBAR GUI to be the size of half the screen

*See Also:* [GUI.Centre](GUI#guicentre),
[GUI.Height](GUI#guiheight),
[GUIControl.SetPosition](GUIControl#guicontrolsetposition),
[GUI.SetPosition](GUI#guisetposition),
[GUI.Width](GUI#guiwidth)

---

### `GUI.AsTextWindow`

    readonly TextWindowGUI* GUI.AsTextWindow

If this GUI is of TextWindow type then returns the TextWindowGUI interface which could be used to access specific properties; otherwise returns null.

Example:

    TextWindowGUI *tw = gMyTextGui.AsTextWindow;
    tw.TextColor = Game.GetColorFromRGB(255, 0, 0);

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [TextWindowGUI](TextWindowGUI)

---

### `GUI.BackgroundColor`

    int GUI.BackgroundColor

Gets/sets the background color.

Setting BackgroundColor to 0 will make GUI background fully transparent.

This property is ignored if the GUI.BackgroundGraphic is assigned a sprite number (other than 0).

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [GUI.BackgroundGraphic](GUI#guibackgroundgraphic), [GUI.BorderColor](GUI#guibordercolor)

---

### `GUI.BackgroundGraphic`

*(Formerly known as SetGUIBackgroundPic, which is now obsolete)*

    int GUI.BackgroundGraphic

Gets/sets the background image of the GUI.

You can set this to 0 to remove the background image from the GUI.

When this property is assigned a sprite number other than 0 GUI.BackgroundColor and GUI.BorderColor are ignored.

*See Also:* [GUI.SetPosition](GUI#guisetposition),
[Button.NormalGraphic](Button#buttonnormalgraphic)

---

### `GUI.BorderColor`

    int GUI.BorderColor

Gets/sets the border color.

Setting BorderColor to 0 will make GUI border fully transparent.

Not applicable to TextWindow GUIs. This property is ignored if the GUI.BackgroundGraphic is assigned a sprite number (other than 0).

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [GUI.BackgroundColor](GUI#guibackgroundcolor), [GUI.BackgroundGraphic](GUI#guibackgroundgraphic)

---

### `GUI.Clickable`

*(Formerly known as SetGUIClickable, which is now obsolete)*

    bool GUI.Clickable

Gets/sets whether the GUI is clickable or not. This allows you to modify
the "Clickable" checkbox from the GUI Editor.

If this is set to 1, then the GUI will respond to mouse clicks as
normal.

If this is set to 0, then this GUI cannot be clicked on by the mouse.
This might be useful for a transparent overlay GUI which displays
information, and you want the player to be able to click on whatever is
underneath.

Example:

    gStatusline.Clickable = false;

sets the STATUSLINE GUI to no longer respond to mouse clicks.

*See Also:* [GUI.GetAtScreenXY](GUI#guigetatscreenxy)

---

### `GUI.ControlCount`

    readonly int GUI.ControlCount;

Gets the number of controls on the GUI. You won't normally need to use
this property, but in some circumstances you may wish to iterate through
all the GUI's controls, and this allows you to determine where to stop.

Example:

    int i = 0;
    while (i < gInventory.ControlCount) {
      gInventory.Controls[i].Enabled = false;
      i++;
    }

disables all controls on the INVENTORY GUI.

*See Also:* [GUI.Controls](GUI#guicontrols)

---

### `GUI.Controls`

    GUIControl* GUI.Controls[index]

Provides an array which allows you to access controls on the GUI by
their index. You should not normally need to do this, since accessing
the controls by their name is far easier; however, if you need to
interoperate with legacy code that uses the control number, this can
come in useful.

Returns the GUIControl object for the specified control index, or *null*
if you give an invalid control index.

You can cast the GUIControl to the appropriate type using the AsButton,
AsListBox, etc methods on it.

Example:

    GUIControl *control = gInventory.Controls[4];
    if (control == null) {
      Display("The inventory GUI doesn't have a control number 4.");
    }
    else {
      control.Enabled = true;
      control.AsListBox.AddItem("New item!!");
    }

gets list box number 4 from the INVENTORY GUI, and then adds an item to
it. If control 4 isn't a listbox, you will get a Null Reference error.

*See Also:* [GUIControl.As\*](GUIControl#guicontrolastype),
[GUI.ControlCount](GUI#guicontrolcount)

---

### `GUI.Height`

    int GUI.Height

Gets/sets the height of the GUI. This allows you to dynamically change
the size of the GUI on the screen.

The height is specified in the normal 320-resolution style.

Example:

    Display("The icon bar GUI is %d pixels high.", gIconbar.Height);

displays the height of the ICONBAR GUI.

*See Also:* [GUI.SetSize](GUI#guisetsize),
[GUI.Width](GUI#guiwidth)

---

### `GUI.ID`

    readonly int GUI.ID

Gets the GUI's ID number. This is the GUI's number from the editor, and
is useful if you need to interoperate with legacy code that uses the
GUI's number rather than object name.

Example:

    SetGUIClickable(gIconbar.ID, 1);
    gIconbar.Clickable = false;

uses the obsolete SetGUIClickable function to make the ICONBAR GUI
clickable, and then uses the equivalent modern property to stop it being
clickable.

*See Also:* [GUIControl.ID](GUIControl#guicontrolid)

---

### `GUI.PopupStyle`

    readonly GUIPopupStyle GUI.PopupStyle

Gets the style of GUI behavior on screen. Possible values are:

    eGUIPopupNormal       no special behavior
    eGUIPopupMouseYPos    shown when the mouse cursor moves to the top of the screen, past GUI.PopupYPos, and hidden all other time.
    eGUIPopupModal        like normal, but pauses game when shown
    eGUIPopupPersistent   like normal, but not removed when all interface is disabled

**NOTE:** for MouseYPos style GUI.Visible property does not control visibility directly. The GUI will become visible only when both conditions match:
- GUI.Visible property set to TRUE;
- mouse cursor is closer to the screen top than GUI.PopupYPos value.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [GUI.PopupYPos](GUI#guipopupypos), [GUI.Visible](GUI#guivisible)

---

### `GUI.PopupYPos`

    int GUI.PopupYPos

Gets/sets the Y co-ordinate at which the GUI will appear when using MouseYPos popup style. The GUI will be automatically shown when the mouse cursor's Y coordinate is *equal or lower* than GUI.PopupYPos (closer to the screen top) and hidden when it is *greater*.

This property is ignored if GUI has a different style.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [GUI.PopupStyle](GUI#guipopupstyle), [GUI.Visible](GUI#guivisible)

---

### `GUI.Transparency`

*(Formerly known as SetGUITransparency, which is now obsolete)*

    int GUI.Transparency

Gets/sets the GUI translucency, in percent.

Setting this to 100 means the GUI is totally invisible, and lower values
represent varying levels of translucency. Set it to 0 to stop the GUI
being translucent.

**NOTE:** Transparency only works in 16-bit and 32-bit color games.

**NOTE:** When using the DirectX 5 driver, a large transparent GUI can
significantly slow down AGS.

Some rounding is done internally when the transparency is stored --
therefore, if you get the transparency after setting it, the value you
get back might be one out. Therefore, using a loop with
`gInventory.Transparency++;` is not recommended as it will probably end
too quickly.

In order to fade a GUI in/out, the best approach is shown in the example
below:

Example:

    int trans = gInventory.Transparency;
    while (trans < 100) {
      trans++;
      gInventory.Transparency = trans;
      Wait(1);
    }

will gradually fade the INVENTORY GUI out until it is invisible.

*See Also:* [Object.Transparency](Object#objecttransparency)

---

### `GUI.Visible`

*(Formerly known as GUIOff, which is now obsolete)*<br>
*(Formerly known as GUIOn, which is now obsolete)*<br>
*(Formerly known as InterfaceOff, which is now obsolete)*<br>
*(Formerly known as InterfaceOn, which is now obsolete)*<br>
*(Formerly known as IsGUIOn, which is now obsolete)*

    bool GUI.Visible

Gets/sets whether the GUI is visible or not. This property has behaves
differently depending on the GUI popup style.

For "Normal" and "Persistent" GUIs, this property simply switches the
GUI on and off, and has no further effects.

For "Popup modal" GUIs, setting Visible to true causes the game to
become paused until the GUI is removed by setting Visible back to false
(eg. when the user presses an OK button or something similar).

For "Mouse Ypos" GUIs, the Visible property does not actually determine
whether the GUI can be seen, but instead it controls whether the GUI
**is allowed to** pop up. If Visible is *false*, then moving the mouse
to the top of the screen will not activate the GUI; if it is *true*,
then the GUI will be allowed to be popped up.

Example:

    gSettings.Visible = true;

will turn on the SETTINGS GUI.

*See Also:* [IsGamePaused](Globalfunctions_General#isgamepaused)

---

### `GUI.Width`

    int GUI.Width

Gets/sets the width of the GUI. This allows you to dynamically change
the size of the GUI on the screen.

The width is specified in the normal 320-resolution style.

Example:

    gInventory.Width += 5;

makes the INVENTORY GUI 5 pixels wider.

*See Also:* [GUI.Height](GUI#guiheight),
[GUI.SetSize](GUI#guisetsize)

---

### `GUI.X`

    int GUI.X

Gets/sets the X position of the GUI. This allows you to dynamically
change the position of the GUI on the screen.

The X position is the left-hand side of the GUI, and can be between 0
and 320. The co-ordinates used are screen co-ordinates, not room
co-ordinates, and are in the normal 320-resolution style.

Example:

    gMyGui.X += 5;

moves the GUI right 5 pixels.

*See Also:* [GUI.SetPosition](GUI#guisetposition),
[GUI.Y](GUI#guiy)

---

### `GUI.Y`

    int GUI.Y

Gets/sets the Y position of the GUI. This allows you to dynamically
change the position of the GUI on the screen.

The Y position is the top edge of the GUI, and can be between 0 and 200
(or 240, depending on room height). The co-ordinates used are screen
co-ordinates, not room co-ordinates, and are in the normal
320x200-resolution style.

Example:

    gMyGui.Y += 5;

moves the GUI down 5 pixels.

*See Also:* [GUI.SetPosition](GUI#guisetposition),
[GUI.X](GUI#guix)

---

### `GUI.ZOrder`

*(Formerly known as SetGUIZOrder, which is now obsolete)*

    int GUI.ZOrder

Gets/sets the z-order of the GUI. This allows you to dynamically change
the ordering of GUIs on the screen.

The Z-order setting is an arbitrary number between 0 and 1000. AGS draws
the GUIs in order, from the lowest numbered at the back to the highest
numbered at the front.

Example:

    gStatusline.ZOrder = 0;

sets the STATUSLINE GUI to be behind all other GUIs.

*See Also:* [GUI.GetAtScreenXY](GUI#guigetatscreenxy)

