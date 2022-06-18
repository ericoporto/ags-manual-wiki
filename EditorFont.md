## Font Preview

You cannot exactly *edit* fonts from within the AGS itself at the time being (unless you are using a plugin that allows that), but AGS lets you to preview the imported fonts and configure their runtime display properties.

On the Explore Project panel, you can expand the Fonts node to show the fonts which are imported for your game. Right clicking on the "Fonts" node itself allows you to create a new font. When creating a new font, or double-clicking on existing font within the tree, a new preview panel will open.

When a new font is created it clones the last one in the list. To overwrite an existing font, press the "Import over this font..." button.

AGS supports two kinds of fonts: TrueType (TTF) and bitmap fonts, which are: SCI fonts (Sierra's font format) and WFN fonts (extended bitmap font format).

**NOTE:** On Windows you cannot import fonts directly from the Windows Fonts folder. Unfortunately there is nothing that can be done about this, you must manually copy the font to another folder and import it from there.

Fonts can have outlines. For LucasArts-style speech, outlines are really
a necessity since they stop the text blending into the background and
becoming un-readable. To outline a font, either set the OutlineStyle to
"Automatic" to have AGS do it for you, or you can use a specific font
slot as the outline font (it will be drawn in black behind the main font
when the main font is used).

Every font have following optional properties:

-   **LineSpacing** - defines default difference (in pixels) between two
    lines of wrapped text. Setting this to 0 will make font use its own
    height as a vertical spacing. Having line spacing lower than font's
    height will make lines partially overlap.
-   **SizeMultiplier** - an integer scale multiplier applied to this font. 
    Note that it commonly makes sense to assign this for the bitmap fonts,
    as TTF fonts may be reimported with different font size. 
    When set for a TTF font it will simply be initialized with a higher
    point-size in game.
-   **VerticalOffset** - defines additional vertical offset applied to
    every drawn line of text (when using this font). This property is
    mainly meant to override particular font's misbehavior.

