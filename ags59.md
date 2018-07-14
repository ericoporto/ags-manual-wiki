GUI Label functions and properties
----------------------------------

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

[Font property (label)](#Label.Font)\
[Text property (label)](#Label.Text)\
[TextColor property (label)](#Label.TextColor)

------------------------------------------------------------------------



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

*See Also:* [IsTranslationAvailable](ags54#IsTranslationAvailable),
[Label.Text](ags59#Label.Text),
[TextBox.Font](ags62#TextBox.Font)

------------------------------------------------------------------------



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

*See Also:* [Button.NormalGraphic](ags57#Button.NormalGraphic),
[Button.Text](ags57#Button.Text),
[Label.TextColor](ags59#Label.TextColor),
[Label.Font](ags59#Label.Font)

------------------------------------------------------------------------



### TextColor property (label)

*(Formerly known as SetLabelColor, which is now obsolete)*

    int Label.TextColor;

Gets/sets the text colour used to display the label's text.

Example:

    lblStatus.TextColor = 14;

will change label 'lblStatus' to have yellow text.

*See Also:* [Label.Font](ags59#Label.Font),
[Label.Text](ags59#Label.Text)


