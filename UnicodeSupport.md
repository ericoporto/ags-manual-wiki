## Unicode Support

Starting with v3.6.0 AGS has a full Unicode support, which means that it may have texts virtually in any language in the game, and even texts in multiple languages displayed simultaneously, so long as you provide appropriate fonts.

**NOTE:** AGS still has a ASCII mode for backwards compatibility, but it's recommended to not use it without a very good reason. See a [corresponding section](#using-ascii-mode) below for details.

When in Unicode mode, all game texts and text files, such as scripts, are saved in UTF-8 format (to be technically precise: it's UTF-8 without BOM).

When in Unicode mode you may type your game texts in any language whatsoever. This refers to the following:
* Human-readable texts in-game options: such as character's "real names", object descriptions, and so on;
* Values of String Custom properties and Global Variables;
* String literals in scripts (any text in double-quotes);
* Character literals in a script (a character in single quotes);
* Speech lines in dialog scripts;
* Translations.

Mixing multiple languages, *even in the same string*, is fine (but requires having fonts that can display all of these languages altogether).

Where Unicode won't work (and is not supposed to):
* Script names of game objects: characters, guis, views, and so on;
* Names of Custom properties and Global Variables;
* Variable names and function names in script.

All the above must be written strictly in the Latin alphabet.

`String` variables and related functions should work seamlessly with Unicode texts. Functions that work with characters accept Unicode characters (this refers to `AppendChar()`, `ReplaceChar()` and `String.Char[]` property). Also, `String.Format("%c", n)` kind of statement is able to print Unicode characters.

**IMPORTANT:** The `char` type in AGS script remains a 8-bit number and represents a single byte (which may have values 0-255). But Unicode characters may theoretically be of almost any positive integer value. Because of that you would require `int` variables to store and pass Unicode characters into functions. To put it simply: use `int` when you need a Unicode character, and use `char` when you know it's a ASCII character or just any small value for which a single byte is enough.

### Fonts

For your game you will have to find fonts compatible to the chosen mode. If you're using strictly standard Latin character set in your game (like with English language), then you likely won't see any difference, but the correct font choice is essential for languages that use "extended" Latin (like letters with accents) or non-Latin alphabets. With these languages, if fonts don't match then you will usually see "garbage" instead of a real text.

If you are using a Unicode mode, then the fonts should be Unicode compatible. Most of the TTF fonts around are probably that, but some of them could have been made specifically for ASCII/ANSI games, so just keep that in mind in case they display incorrectly.

WFN (bitmap) fonts in theory can support Unicode, but it's likely there were none or very little made. In order to make a Unicode bitmap font you'd have to find and use a font editor which supports making letters with index >255.

Another thing to keep in mind is that even Unicode compatible font may not include all wanted languages (alphabets) in it. In such case your options are either to find a more complete single font, or use more fonts for different languages in your game.

### Translations

The Translations are not affected by the game's setting and have an individual setting of their own. This lets to have Unicode translations in ASCII-mode games, or even ASCII translations in Unicode-mode games (if really necessary). For more information please check the [Translations](Translations) article.

### Upgrading older projects

All the new game projects start in Unicode mode by default, but if you're upgrading an older project and wish to turn to Unicode mode then you may have to go to [General Settings](GeneralSettings) and switch "Text format". But you might have to replace fonts with Unicode compatible ones after this.

### Using ASCII mode

Because of the backward compatibility there's still an option to switch back to ASCII mode, but it's not recommended without a good reason. This option is located in [General Settings](GeneralSettings) and is called "Text format". This option will let you to switch between ASCII and Unicode and back. Please be aware that when doing so the Editor will convert all the game files (scripts, etc) to a new text encoding and re-save them. Normally this should be safe, but probably a good idea to make a project backup before doing so.
