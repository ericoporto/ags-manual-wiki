## Standard Enumerated Types

AGS has several [enumerated types](ScriptKeywords#enum) in its standard header.
These are
used in calls to various commands, and will usually pop up automatically
in autocomplete. However, for times where autocomplete doesn't do the
job, having a manual reference is invaluable:

### `Alignment`

    enum Alignment {
      eAlignNone          = 0,
      eAlignTopLeft       = 1,
      eAlignTopCenter     = 2,
      eAlignTopRight      = 4,
      eAlignMiddleLeft    = 8,
      eAlignMiddleCenter  = 16,
      eAlignMiddleRight   = 32,
      eAlignBottomLeft    = 64,
      eAlignBottomCenter  = 128,
      eAlignBottomRight   = 256,
      eAlignHasLeft       = 73,
      eAlignHasRight      = 292,
      eAlignHasTop        = 7,
      eAlignHasBottom     = 448,
      eAlignHasHorCenter  = 146,
      eAlignHasVerCenter  = 56
    };

The Alignment enumeration consists of values that could be summed up in one integer variable to form a more complex combination of alignments. Although that ability is not used anywhere in practice yet, but may be in future. Additionally, it provides a set of masks that could be applied bitwise to check if alignment variable contains one of the distinct directions, for example:

    if (align & eAlignHasLeft)
      // some code here

will execute some code if *align* variable contains "Left" in any combination (eAlignTopLeft, eAlignMiddleLeft or eAlignBottomLeft).

*Compatibility:* new version of Alignment enum was introduced in AGS 3.5.0. Previous Alignment was renamed into HorizontalAlignment.

*Used by:* [`Button.TextAlignment`](Button#buttontextalignment)

### `AudioFileType`

    enum AudioFileType {
      eAudioFileOGG,
      eAudioFileMP3,
      eAudioFileWAV,
      eAudioFileVOC,
      eAudioFileMIDI,
      eAudioFileMOD
    };

*Used by:* [`AudioClip.FileType`](AudioClip#audioclipfiletype)

### `AudioPriority`

    enum AudioPriority {
      eAudioPriorityVeryLow = 1,
      eAudioPriorityLow = 25,
      eAudioPriorityNormal = 50,
      eAudioPriorityHigh = 75,
      eAudioPriorityVeryHigh = 100
    };

*Used by:* [`AudioClip.Play`](AudioClip#audioclipplay),
[`AudioClip.PlayFrom`](AudioClip#audioclipplayfrom),
[`AudioClip.PlayQueued`](AudioClip#audioclipplayqueued)

### `BlockingStyle`

    enum BlockingStyle {
      eBlock,
      eNoBlock
    };

*Used by:* [`Character.Animate`](Character#characteranimate),
[`Character.FaceCharacter`](Character#characterfacecharacter),
[`Character.FaceLocation`](Character#characterfacelocation),
[`Character.FaceObject`](Character#characterfaceobject),
[`Character.Move`](Character#charactermove),
[`Character.Walk`](Character#characterwalk),
[`Character.WalkStraight`](Character#characterwalkstraight),
[`Object.Animate`](Object#objectanimate),
[`Object.Move`](Object#objectmove)

### `eCDAudioFunction`

    enum eCDAudioFunction {
      eCDIsDriverPresent,
      eCDGetPlayingStatus,
      eCDPlayTrack,
      eCDPausePlayback,
      eCDResumePlayback,
      eCDGetNumTracks,
      eCDEject,
      eCDCloseTray,
      eCDGetCDDriveCount,
      eCDSelectActiveCDDrive
    };

*Used by:* [`CDAudio`](Multimedia#cdaudio)

### `CharacterDirection`

    enum CharacterDirection {
      eDirectionDown = 0,
      eDirectionLeft,
      eDirectionRight,
      eDirectionUp,
      eDirectionDownRight,
      eDirectionUpRight,
      eDirectionDownLeft,
      eDirectionUpLeft,
      eDirectionNone = SCR_NO_VALUE
    };

*Used by:* [`Character.ChangeRoom`](Character#characterchangeroom),
[`Character.FaceDirection`](Character#characterfacedirection)

### `CursorMode`

    enum CursorMode {
      eModeXXXX,
      eModeXXXX,
      ...
    };

The CursorMode enumeration is generated automatically based on your
mouse cursors. The cursor mode name is taken, all its spaces are
removed, and *eMode* is added to the front.<br>
*Used by:* [`IsInteractionAvailable`](Globalfunctions_General#isinteractionavailable),
[`Room.ProcessClick`](Room#roomprocessclick),
[`Mouse.ChangeModeGraphic`](Mouse#mousechangemodegraphic),
[`Mouse.ChangeModeHotspot`](Mouse#mousechangemodehotspot),
[`Mouse.DisableMode`](Mouse#mousedisablemode),
[`Mouse.EnableMode`](Mouse#mouseenablemode),
[`Mouse.IsModeEnabled`](Mouse#mouseismodeenabled),
[`Mouse.UseModeGraphic`](Mouse#mouseusemodegraphic),
[`Mouse.Mode`](Mouse#mousemode),
[`InventoryItem.IsInteractionAvailable`](InventoryItem#inventoryitemisinteractionavailable),
[`InventoryItem.RunInteraction`](InventoryItem#inventoryitemruninteraction),
[`Hotspot.IsInteractionAvailable`](Hotspot#hotspotisinteractionavailable),
[`Hotspot.RunInteraction`](Hotspot#hotspotruninteraction),
[`Object.IsInteractionAvailable`](Object#objectisinteractionavailable),
[`Object.RunInteraction`](Object#objectruninteraction),
[`Character.IsInteractionAvailable`](Character#characterisinteractionavailable),
[`Character.RunInteraction`](Character#characterruninteraction)

### `CutsceneSkipType`

    enum CutsceneSkipType {
      eSkipESCOnly,
      eSkipAnyKey,
      eSkipMouseClick,
      eSkipAnyKeyOrMouseClick,
      eSkipESCOrRightButton,
      eSkipScriptOnly
    };

*Used by:* [`StartCutscene`](Globalfunctions_General#startcutscene)

### `DialogOptionSayStyle`

    enum DialogOptionSayStyle {
      eSayUseOptionSetting,
      eSayAlways,
      eSayNever
    };

*Used by:* [`Dialog.DisplayOptions`](Dialog#dialogdisplayoptions)

### `DialogOptionState`

    enum DialogOptionState {
      eOptionOff,
      eOptionOn,
      eOptionOffForever
    };

*Used by:* [`Dialog.GetOptionState`](Dialog#dialoggetoptionstate),
[`Dialog.SetOptionState`](Dialog#dialogsetoptionstate)

### `Direction`

    enum Direction {
      eForwards,
      eBackwards
    };

*Used by:* [`Character.Animate`](Character#characteranimate),
[`Object.Animate`](Object#objectanimate)

### `EventType`

    enum EventType {
      eEventLeaveRoom,
      eEventEnterRoomBeforeFadein,
      eEventGotScore,
      eEventGUIMouseDown,
      eEventGUIMouseUp,
      eEventAddInventory,
      eEventLoseInventory,
      eEventRestoreGame
    };

*Passed into:* on_event

### `FileMode`

    enum FileMode {
      eFileRead,
      eFileWrite,
      eFileAppend
    };

*Used by:* [`File.Open`](File#fileopen)

### `FileSeek`

    enum FileSeek {
      eSeekBegin = 0,
      eSeekCurrent = 1,
      eSeekEnd = 2
    };

*Used by:* [`File.Seek`](File#fileseek)

### `eFlipDirection`

    enum eFlipDirection {
      eFlipLeftToRight,
      eFlipUpsideDown,
      eFlipBoth
    };

*Used by:* [`DynamicSprite.Flip`](DynamicSprite#dynamicspriteflip)

### `FontType`

    enum FontType {
      eFontXXXX,
      eFontXXXX,
      ...
    };

The FontType enumeration is generated automatically based on your fonts.
The font name is taken, all its spaces are removed, and *eFont* is added
to the front.<br>
*Used by:* [`Button.Font`](Button#buttonfont),
[`DrawingSurface.DrawMessageWrapped`](DrawingSurface#drawingsurfacedrawmessagewrapped),
[`DrawingSurface.DrawString`](DrawingSurface#drawingsurfacedrawstring),
[`DrawingSurface.DrawStringWrapped`](DrawingSurface#drawingsurfacedrawstringwrapped),
[`Game.NormalFont`](Game#gamenormalfont),
[`Game.SpeechFont`](Game#gamespeechfont),
[`GetTextHeight`](Globalfunctions_General#gettextheight),
[`GetTextWidth`](Globalfunctions_General#gettextwidth),
[`Label.Font`](Label#labelfont),
[`ListBox.Font`](ListBox#listboxfont),
[`TextBox.Font`](TextBox#textboxfont),
[`Overlay.CreateTextual`](Overlay#overlaycreatetextual),
[`Overlay.SetText`](Overlay#overlaysettext)

### `GUIPopupStyle`

    enum GUIPopupStyle {
      eGUIPopupNormal = 0,
      eGUIPopupMouseYPos = 1,
      eGUIPopupModal = 2,
      eGUIPopupPersistent = 3
    };

*Supported by:* AGS 3.5.0 and higher.

*Used by:* [`GUI.PopupStyle`](GUI#guipopupstyle)

### `HorizontalAlignment`

    enum HorizontalAlignment {
      eAlignLeft          = 1,
      eAlignCenter        = 2,
      eAlignRight         = 4
    };

Note that HorizontalAlignment's values match the first values of Alignment enumeration (eAlignTopLeft, eAlignTopCenter, eAlignTopRight).

*Compatibility:* replaced old Alignment enumeration in AGS 3.5.0.

*Used by:*
[`Character.LockViewAligned`](Character#characterlockviewaligned), [`DrawingSurface.DrawStringWrapped`](DrawingSurface#drawingsurfacedrawstringwrapped), [`Label.TextAlignment`](Label#labeltextalignment), [`ListBox.TextAlignment`](ListBox#listboxtextalignment), [`Speech.TextAlignment`](Speech#speechtextalignment)

### `InputType`

    enum InputType
    {
        eInputNone     = 0x00000000,
        eInputKeyboard = 0x00020000,
        eInputMouse    = 0x00040000,
        eInputAny      = 0xFFFF0000
    };

The InputType enumeration consists of values that could be summed up in one integer variable to form a combination of input types. This may be used to store several "types" in one integer, pass them into a function, or return from a function. You may use bitwise operation to check if a variable contains one of the distinct types, for example:

    if (type & eInputKeyboard)
      // some code here

will execute some code if *type* variable contains *at least* "eInputKeyboard".

*Supported by:* AGS 3.6.0 and higher.

*Used by:* [Wait functions](Globalfunctions_Wait)

### `LocationType`

    enum LocationType {
      eLocationNothing,
      eLocationHotspot,
      eLocationCharacter,
      eLocationObject
    };

*Returned by:* [`GetLocationType`](Globalfunctions_General#getlocationtype)

### `LogLevel`

    enum LogLevel
    {
        eLogAlert = 1,
        eLogFatal = 2,
        eLogError = 3,
        eLogWarn = 4,
        eLogInfo = 5,
        eLogDebug = 6
    };


*Supported by:* AGS 3.6.0 and higher.

*Used by:* [`System.Log`](System#systemlog)

### `MouseButton`

    enum MouseButton {
      eMouseLeft,
      eMouseRight,
      eMouseMiddle,
      eMouseLeftInv,
      eMouseMiddleInv,
      eMouseRightInv,
      eMouseWheelNorth,
      eMouseWheelSouth
    };

*Used by:* [`Mouse.IsButtonDown`](Mouse#mouseisbuttondown)<br>
*Passed into:* on_mouse_click

### `eOperatingSystem`

    enum eOperatingSystem {
      eOSDOS,
      eOSWindows,
      eOSLinux,
      eOSMacOS,
      eOSAndroid,
      eOSiOS,
      eOSPSP,
      eOSWeb,
      eOSFreeBSD
    };

*Used by:* [`System.OperatingSystem`](System#systemoperatingsystem)

### `RepeatStyle`

    enum RepeatStyle {
      eOnce,
      eRepeat
    };

*Used by:* [`Button.Animate`](Button#buttonanimate),
[`Character.Animate`](Character#characteranimate),
[`Object.Animate`](Object#objectanimate)

### `RoundDirection`

    enum RoundDirection {
      eRoundDown,
      eRoundNearest,
      eRoundUp
    };

*Used by:* [`FloatToInt`](Maths#floattoint)

### `SkipSpeechStyle`

    enum SkipSpeechStyle {
      eSkipNone         = -1,
      eSkipKeyMouseTime = 0,
      eSkipKeyTime      = 1,
      eSkipTime         = 2,
      eSkipKeyMouse     = 3,
      eSkipMouseTime    = 4,
      eSkipKey          = 5,
      eSkipMouse        = 6
    };

*Used by:* [`Speech.SkipStyle`](Speech#speechskipstyle)

### `SortStyle`

    enum SortStyle {
      eNonSorted = 0,
      eSorted = 1
    };

*Supported by:* AGS 3.5.0 and higher.

*Used by:* [`Dictionary.Create`](Dictionary#dictionarycreate),
[`Set.Create`](Set#setcreate)

### `eSpeechStyle`

    enum eSpeechStyle {
      eSpeechLucasarts,
      eSpeechSierra,
      eSpeechSierraWithBackground,
      eSpeechFullScreen
    };

*Used by:* [`Speech.Style`](Speech#speechstyle)

### `StopMovementStyle`

    enum StopMovementStyle
    {
      eKeepMoving = 0,
      eStopMoving = 1
    };

*Used by:* [`Character.LockView`](Character#characterlockviewaligned),
[`Character.LockViewFrame`](Character#characterlockviewoffset)

### `StringCompareStyle`

    enum StringCompareStyle {
      eCaseInsensitive = 0,
      eCaseSensitive = 1
    };

*Supported by:* AGS 3.5.0 and higher.

*Used by:* [`Dictionary.Create`](Dictionary#dictionarycreate),
[`Set.Create`](Set#setcreate),
[`String.CompareTo`](String#stringcompareto),
[`String.EndsWith`](String#stringendswith),
[`String.Replace`](String#stringreplace),
[`String.StartsWith`](String#stringstartswith)

### `TransitionStyle`

    enum TransitionStyle {
      eTransitionFade,
      eTransitionInstant,
      eTransitionDissolve,
      eTransitionBoxout,
      eTransitionCrossfade
    };

*Used by:* [`SetScreenTransition`](Globalfunctions_Screen#setscreentransition),
[`SetNextScreenTransition`](Globalfunctions_Screen#setnextscreentransition)

### `VideoSkipStyle`

    enum VideoSkipStyle {
      eVideoSkipNotAllowed,
      eVideoSkipEscKey,
      eVideoSkipAnyKey,
      eVideoSkipAnyKeyOrMouse
    };

*Used by:* [`PlayVideo`](Multimedia#playvideo)

### `eVoiceMode`

    enum eVoiceMode {
      eSpeechTextOnly,
      eSpeechVoiceAndText,
      eSpeechVoiceOnly
    };

*Used by:* [`Speech.VoiceMode`](Speech#speechvoicemode)

### `WalkWhere`

    enum WalkWhere {
      eAnywhere,
      eWalkableAreas
    };

*Used by:* [`Character.Move`](Character#charactermove),
[`Character.Walk`](Character#characterwalk),
[`Object.Move`](Object#objectmove)
