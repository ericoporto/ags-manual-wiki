GUI Text Box functions and properties
-------------------------------------

[BringToFront (inherited)](topic53#GUIControl.BringToFront)\
[Clickable property (inherited)](topic53#GUIControl.Clickable)\
[Enabled property (inherited)](topic53#GUIControl.Enabled)\
[Height property (inherited)](topic53#GUIControl.Height)\
[ID property (inherited)](topic53#GUIControl.ID)\
[OwningGUI property (inherited)](topic53#GUIControl.OwningGUI)\
[SendToBack (inherited)](topic53#GUIControl.SendToBack)\
[SetPosition (inherited)](topic53#GUIControl.SetPosition)\
[SetSize (inherited)](topic53#GUIControl.SetSize)\
[Visible property (inherited)](topic53#GUIControl.Visible)\
[Width property (inherited)](topic53#GUIControl.Width)\
[X property (inherited)](topic53#GUIControl.X)\
[Y property (inherited)](topic53#GUIControl.Y)\
[ZOrder property (inherited)](topic53#GUIControl.ZOrder)

[Font property (text box)](#TextBox.Font)\
[Text property (text box)](#TextBox.Text)\
[TextColor property (text box)](#TextBox.TextColor)

---

### Font property (text box)

*(Formerly known as SetTextBoxFont, which is now obsolete)*

    FontType TextBox.Font

Gets/sets the font used by the specified text box. This might be useful
if you need a player input text box to use a different font with foreign
language translations, for example.

Example:

    txtUserInput.Font = eFontNormal;

will change the *txtUserInput* text box to use Font "Normal".

*See Also:* [Label.Font](topic55#Label.Font),
[TextBox.Text](topic58#TextBox.Text)

---

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

*See Also:* [TextBox.Font](topic58#TextBox.Font),
[String.CompareTo](topic71#String.CompareTo),
[Label.Text](topic55#Label.Text)

---

### TextColor property (text box)

    int TextBox.TextColor;

Gets/sets the text colour used to draw the text box. This affects both
the text in the text box, and also the text box's border.

Example:

    txtInput.TextColor = 14;

will change text box 'txtInput' to have yellow text.

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:* [TextBox.Text](topic58#TextBox.Text)

