## `Label` functions and properties

Label is a subclass of [`GUIControl`](GUIControl) and therefore inherits all GUIControl's functions and properties in addition to its own, which are listed below.

---

### `Label.Font`

*(Formerly known as `SetLabelFont`, which is now obsolete)*

    FontType Label.Font;

Gets/sets the font used to display the label's text. This is useful if
you have a standard SCI font for your English version, but want to
change to a TTF font for foreign language versions.

Example:

    if (IsTranslationAvailable()) {
      lblStatus.Font = eFontForeign;
    }

will change label 'lblStatus' to use font "Foreign" if a game
translation is in use.

*See also:* [`IsTranslationAvailable`](Globalfunctions_General#istranslationavailable),
[`Label.Text`](Label#labeltext),
[`TextBox.Font`](TextBox#textboxfont)

---

### `Label.Text`

*(Formerly known as `SetLabelText`, which is now obsolete)*<br>
*(Formerly known as `Label.GetText`, which is now obsolete)*<br>
*(Formerly known as `Label.SetText`, which is now obsolete)*

    String Label.Text;

Gets/sets the text displayed in the specified label. This allows you to
change the text during the game, for example to create a LucasArts-style
status line.

Example:

    lblStatus.Text = Game.GetLocationName(mouse.x, mouse.y);

will display the name of the location the cursor is over on label
'lblStatus'

*See also:* [`Button.NormalGraphic`](Button#buttonnormalgraphic),
[`Button.Text`](Button#buttontext),
[`Label.TextColor`](Label#labeltextcolor),
[`Label.Font`](Label#labelfont)

---

### `Label.TextAlignment`

    HorizontalAlignment Label.TextAlignment;

Gets/sets how the text is aligned relative to the label's rectangle. Note that currently label supports only horizontal alignment which could be eAlignLeft, eAlignRight and eAlignCenter.

*See also:* [Standard Enumerated Types](StandardEnums), [`Label.Font`](Label#labelfont),
[`Label.Text`](Label#labeltext)

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

---

### `Label.TextColor`

*(Formerly known as `SetLabelColor`, which is now obsolete)*

    int Label.TextColor;

Gets/sets the text color used to display the label's text.

Example:

    lblStatus.TextColor = 14;

will change label 'lblStatus' to have yellow text.

*See also:* [`Label.Font`](Label#labelfont),
[`Label.Text`](Label#labeltext)

