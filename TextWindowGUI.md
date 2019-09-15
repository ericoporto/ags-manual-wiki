## TextWindowGUI functions and properties

This struct extends the GUI struct, so it has all functions and properties from [GUI](GUI), in addition to the properties below.

---

### TextColor

    attribute int TextWindowGUI.TextColor

Gets/sets the text color to be used when rendering text on this TextWindowGUI.

Example:

    // a say function with character text color
    function MySay(this Character*, const string message,  ...) {
      gTextGui.AsTextWindow.TextColor = this.SpeechColor;
      this.Say(message,  ...);
    }

    // later on, supposed gTextGui is our default TextGUI
    cEgo.MySay("My text has my colors!");

*See Also:* [TextWindowGUI.TextPadding](TextWindowGUI#textpadding)

---

### TextPadding

    attribute int TextWindowGUI.TextPadding

Gets/sets the amount of padding, in pixels, surrounding the text in the TextWindow.

Example:

    // gDisplayTextGui.ID is set in the Editor as the Display GUI in General Settings
    gDisplayTextGui.AsTextWindow.TextPadding = 8;
    Display("This text has more padding");


*See Also:* [TextWindowGUI.TextColor](TextWindowGUI#textcolor)