[]()

[![Contents](contents.gif)](ags) [![Up](up.gif)](ags28#topic41)
[![Previous](back.gif)](ags61#topic57)
[![Next](forward.gif)](ags63#topic59)

------------------------------------------------------------------------

GUI Text Box functions and properties
-------------------------------------

[BringToFront (inherited)](ags56#GUIControl.BringToFront)\
[Clickable property (inherited)](ags56#GUIControl.Clickable)\
[Enabled property (inherited)](ags56#GUIControl.Enabled)\
[Height property (inherited)](ags56#GUIControl.Height)\
[ID property (inherited)](ags56#GUIControl.ID)\
[OwningGUI property (inherited)](ags56#GUIControl.OwningGUI)\
[SendToBack (inherited)](ags56#GUIControl.SendToBack)\
[SetPosition (inherited)](ags56#GUIControl.SetPosition)\
[SetSize (inherited)](ags56#GUIControl.SetSize)\
[Visible property (inherited)](ags56#GUIControl.Visible)\
[Width property (inherited)](ags56#GUIControl.Width)\
[X property (inherited)](ags56#GUIControl.X)\
[Y property (inherited)](ags56#GUIControl.Y)\
[ZOrder property (inherited)](ags56#GUIControl.ZOrder)

[Font property (text box)](#TextBox.Font)\
[Text property (text box)](#TextBox.Text)\
[TextColor property (text box)](#TextBox.TextColor)\

------------------------------------------------------------------------

[]()

### Font property (text box)

*(Formerly known as SetTextBoxFont, which is now obsolete)*

    FontType TextBox.Font

Gets/sets the font used by the specified text box. This might be useful
if you need a player input text box to use a different font with foreign
language translations, for example.

Example:

    txtUserInput.Font = eFontNormal;

will change the *txtUserInput* text box to use Font "Normal".

*See Also:* [Label.Font](ags59#Label.Font),
[TextBox.Text](ags62#TextBox.Text)

------------------------------------------------------------------------

[]()

### Text property (text box)

*(Formerly known as GetTextBoxText, which is now obsolete)*\
*(Formerly known as SetTextBoxText, which is now obsolete)*\
*(Formerly known as TextBox.GetText, which is now obsolete)*\
*(Formerly known as TextBox.SetText, which is now obsolete)*

    String TextBox.Text;

Gets/sets the text box contents. This might be useful to reset the text
box to blank after the user has typed something in, or to fill in a
default value.

Example:

    txtUserInput.Text = "";

will clear the txtUserInput text box.

*See Also:* [TextBox.Font](ags62#TextBox.Font),
[String.CompareTo](ags76#String.CompareTo),
[Label.Text](ags59#Label.Text)

------------------------------------------------------------------------

[]()

### TextColor property (text box)

    int TextBox.TextColor;

Gets/sets the text colour used to draw the text box. This affects both
the text in the text box, and also the text box's border.

Example:

    txtInput.TextColor = 14;

will change text box 'txtInput' to have yellow text.

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:* [TextBox.Text](ags62#TextBox.Text)


