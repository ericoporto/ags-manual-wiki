GUI Text Box functions and properties
-------------------------------------

[BringToFront (inherited)](GUIControl#BringToFront)\
[Clickable property (inherited)](GUIControl#Clickable)\
[Enabled property (inherited)](GUIControl#Enabled)\
[Height property (inherited)](GUIControl#Height)\
[ID property (inherited)](GUIControl#ID)\
[OwningGUI property (inherited)](GUIControl#OwningGUI)\
[SendToBack (inherited)](GUIControl#SendToBack)\
[SetPosition (inherited)](GUIControl#SetPosition)\
[SetSize (inherited)](GUIControl#SetSize)\
[Visible property (inherited)](GUIControl#Visible)\
[Width property (inherited)](GUIControl#Width)\
[X property (inherited)](GUIControl#X)\
[Y property (inherited)](GUIControl#Y)\
[ZOrder property (inherited)](GUIControl#ZOrder)

[Font property (text box)](#Font)\
[Text property (text box)](#Text)\
[TextColor property (text box)](#TextColor)

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

