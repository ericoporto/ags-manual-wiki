GUI Label functions and properties
----------------------------------

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

[Font property (label)](#Font)\
[Text property (label)](#Text)\
[TextColor property (label)](#TextColor)

---

### Font property (label)

*(Formerly known as SetLabelFont, which is now obsolete)*

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

*See Also:* [IsTranslationAvailable](Game#IsTranslationAvailable),
[Label.Text](topic55#Label.Text),
[TextBox.Font](topic58#TextBox.Font)

---

### Text property (label)

*(Formerly known as SetLabelText, which is now obsolete)*\
*(Formerly known as Label.GetText, which is now obsolete)*\
*(Formerly known as Label.SetText, which is now obsolete)*

    String Label.Text;

Gets/sets the text displayed in the specified label. This allows you to
change the text during the game, for example to create a Lucasarts-style
status line.

Example:

    lblStatus.Text = Game.GetLocationName(mouse.x, mouse.y);

will display the name of the location the cursor is over on label
'lblStatus'

*See Also:* [Button.NormalGraphic](topic54#Button.NormalGraphic),
[Button.Text](topic54#Button.Text),
[Label.TextColor](topic55#Label.TextColor),
[Label.Font](topic55#Label.Font)

---

### TextColor property (label)

*(Formerly known as SetLabelColor, which is now obsolete)*

    int Label.TextColor;

Gets/sets the text colour used to display the label's text.

Example:

    lblStatus.TextColor = 14;

will change label 'lblStatus' to have yellow text.

*See Also:* [Label.Font](topic55#Label.Font),
[Label.Text](topic55#Label.Text)

