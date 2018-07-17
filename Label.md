GUI Label functions and properties
----------------------------------

[BringToFront](GUIControl#bringtofront)  
[Clickable property](GUIControl#clickable)  
[Enabled property](GUIControl#enabled)  
[Height property](GUIControl#height)  
[ID property](GUIControl#id)  
[OwningGUI property](GUIControl#owninggui)  
[SendToBack](GUIControl#sendtoback)  
[SetPosition](GUIControl#setposition)  
[SetSize](GUIControl#setsize)  
[Visible property](GUIControl#visible)  
[Width property](GUIControl#width)  
[X property](GUIControl#x)  
[Y property](GUIControl#y)  
[ZOrder property](GUIControl#zorder)

[Font property](#font)  
[Text property](#text)  
[TextColor property](#textcolor)

---

### Font

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

*See Also:* [IsTranslationAvailable](Game#istranslationavailable),
[Label.Text](Label#text),
[TextBox.Font](TextBox#font)

---

### Text

*(Formerly known as SetLabelText, which is now obsolete)*  
*(Formerly known as Label.GetText, which is now obsolete)*  
*(Formerly known as Label.SetText, which is now obsolete)*

    String Label.Text;

Gets/sets the text displayed in the specified label. This allows you to
change the text during the game, for example to create a Lucasarts-style
status line.

Example:

    lblStatus.Text = Game.GetLocationName(mouse.x, mouse.y);

will display the name of the location the cursor is over on label
'lblStatus'

*See Also:* [Button.NormalGraphic](Button#normalgraphic),
[Button.Text](Button#text),
[Label.TextColor](Label#textcolor),
[Label.Font](Label#font)

---

### TextColor

*(Formerly known as SetLabelColor, which is now obsolete)*

    int Label.TextColor;

Gets/sets the text colour used to display the label's text.

Example:

    lblStatus.TextColor = 14;

will change label 'lblStatus' to have yellow text.

*See Also:* [Label.Font](Label#font),
[Label.Text](Label#text)

