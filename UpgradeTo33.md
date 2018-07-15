Upgrading to AGS 3.3
--------------------

AGS 3.3 editor contains a major change to user interface that now lets
you to "unpin" visual panels, drag them to any place you want and dock
them or optionally leave them in "floating" mode. You may also have more
than one editing panel on screen at once, for example room editor and
script editor. This allows everyone to customize the panes layout in AGS
to their own taste.

You may now create folders for characters, dialogs, inventory items,
guis, rooms, scripts and views, move them up/down by context menu, and
drag&drop items to change their order. The "Sort room by number" command
now sorts within folders.

Script and header files are now combined into one group item, similar to
room settings and script.

**Proper alpha blending**

AGS now features proper alpha blending when drawing GUI Controls and
using Drawing Surfaces. This feature is enabled by two separate options
in the "Visual" section of the General Settings: "GUI alpha rendering
style" and "Sprite alpha rendering style". This is done for
compatibility with projects created in previous versions of AGS. When
importing a project in AGS 3.3 these options will retain their original
values. You may consider setting them to "Proper alpha blending", but
that may alter the appearance of your game. New projects will have
"proper blending" mode set by default.

To support alpha blending a new
[HasAlphaChannel](ags50#DialogOptionsRenderingInfo.HasAlphaChannel)
property has been added to DialogOptionsRenderingInfo class. This
property must be set it in
[dialog\_options\_get\_dimensions](ags42#CustomDialogOptions)
function, the one where you normally define size and position of the
drawing surface.

**System limits update**

The maximal number of Fonts has been increased from 15 to 30.

**New Speech class**

There's now a new Speech script class that contains several
speech-related properties. This renders a number of [global
functions](ags54#GlobalCommands) obsolete, as well as some of the
[game variables](ags39#Gamevariables). If you are using any of them
in your script you will likely get compilation errors. Simply replace
them by the corresponding Speech properties, as shown in the table
below:

---
  **obsolete function/variable**         **replace with**
  SetVoiceMode                           [Speech.VoiceMode](ags75#Speech.VoiceMode)
  SetSkipSpeech                          [Speech.SkipStyle](ags75#Speech.SkipStyle)
  SetSpeechStyle                         [Speech.Style](ags75#Speech.Style)
  game.close\_mouth\_end\_speech\_time   [Speech.AnimationStopTimeMargin](ags75#Speech.AnimationStopTimeMargin)
  game.speech\_text\_align               [Speech.TextAlignment](ags75#Speech.TextAlignment)
  game.skip\_speech\_specific\_key       [Speech.SkipKey](ags75#Speech.SkipKey)
  game.talkanim\_speed                   [Speech.GlobalSpeechAnimationDelay](ags75#Speech.GlobalSpeechAnimationDelay)
---

**Game-wide speech animation delay**

The "Old-style game-wide speech animation speed" general setting
previously found in "Backwards compatibility" section was replaced with
two settings in "Dialog" section: "Use game-wide speech animation delay"
and "Game-wide speech animation delay". The first enables the use of the
game-wide delay and the second specifies exact delay value. These
settings are accompanied by two respective properties in the Speech
class.

**Translated ListBox**

In the previous versions of AGS the ListBox items were never translated.
A new "Translated" property has been added to ListBox class, which
forces engine to translate ListBox items. Default value is True but it
is recommended to set it to False if you are using ListBox for listing
savedgames. **NOTE:** when older projects are imported, it is set to
False automatically.