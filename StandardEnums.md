## Standard Enumerated Types

AGS has several [enumerated types](ScriptKeywords#enum) in it's standard header. 
These are
used in calls to various commands, and will usually pop up automatically
in autocomplete. However, for times where autocomplete doesn't do the
job, having a manual reference is invaluable:

    enum BlockingStyle {
      eBlock,
      eNoBlock
    };

*Used by:* [Character.Animate](Character#animate),
[Character.FaceCharacter](Character#facecharacter),
[Character.FaceLocation](Character#facelocation),
[Character.FaceObject](Character#faceobject),
[Character.Move](Character#move),
[Character.Walk](Character#walk),
[Character.WalkStraight](Character#walkstraight),
[Object.Animate](Object#animate),
[Object.Move](Object#move)

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

*Used by:* [Character.ChangeRoom](Character#changeroom),
[Character.FaceDirection](Character#facedirection)

    enum Direction {
      eForwards,
      eBackwards
    };

*Used by:* [Character.Animate](Character#animate),
[Object.Animate](Object#animate)

    enum WalkWhere {
      eAnywhere,
      eWalkableAreas
    };

*Used by:* [Character.Move](Character#move),
[Character.Walk](Character#walk),
[Object.Move](Object#move)

    enum StopMovementStyle
    {
      eKeepMoving = 0,
      eStopMoving = 1
    };

*Used by:* [Character.LockView](Character#lockviewaligned),
[Character.LockViewFrame](Character#lockviewoffset)

    enum RepeatStyle {
      eOnce,
      eRepeat
    };

*Used by:* [Button.Animate](Button#animate),
[Character.Animate](Character#animate),
[Object.Animate](Object#animate)

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

The Alignment enumeration consists of values that could be sumed up in one integer variable to form a more complex combination of alignments. Although that ability is not used anywhere in practice yet, but may be in future. Additionally, it provides a set of masks that could be applied bitwise to check if alignment variable contains one of the distinct directions, for example:

    if (align & eAlignHasLeft)
      // some code here

will execute some code if *align* variable contains "Left" in any combination (eAlignTopLeft, eAlignMiddleLeft or eAlignBottomLeft).

*Compatibility:* new version of Alignment enum was introduced in AGS 3.5.0. Previous Alignment was renamed into HorizontalAlignment.

*Used by:* [Button.TextAlignment](Button#textalignment)

    enum HorizontalAlignment {
      eAlignLeft          = 1,
      eAlignCenter        = 2,
      eAlignRight         = 4
    };

Note that HorizontalAlignment's values match first values of Alignment enumeration (eAlignTopLeft, eAlignTopCenter, eAlignTopRight).

*Compatibility:* replaced old Alignment enumeration in AGS 3.5.0.

*Used by:*
[Character.LockViewAligned](Character#lockviewaligned), [DrawingSurface.DrawStringWrapped](DrawingSurface#drawstringwrapped), [Label.TextAlignment](Label#textalignment), [ListBox.TextAlignment](ListBox#textalignment), [Speech.TextAlignment](Speech#textalignment)

    enum eFlipDirection {
      eFlipLeftToRight,
      eFlipUpsideDown,
      eFlipBoth
    };

*Used by:* [DynamicSprite.Flip](DynamicSprite#flip)

    enum TransitionStyle {
      eTransitionFade,
      eTransitionInstant,
      eTransitionDissolve,
      eTransitionBoxout,
      eTransitionCrossfade
    };

*Used by:* [SetScreenTransition](Globalfunctions_Screen#setscreentransition),
[SetNextScreenTransition](Globalfunctions_Screen#setnextscreentransition)

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

*Used by:* [Mouse.IsButtonDown](Mouse#isbuttondown)<br>
*Passed into:* on_mouse_click

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

    enum RoundDirection {
      eRoundDown,
      eRoundNearest,
      eRoundUp
    };

*Used by:* [FloatToInt](Maths#floattoint)

    enum eSpeechStyle {
      eSpeechLucasarts,
      eSpeechSierra,
      eSpeechSierraWithBackground,
      eSpeechFullScreen
    };

*Used by:* [Speech.Style](Speech#style)

    enum SkipSpeechStyle {
      eSkipKeyMouseTime = 0,
      eSkipKeyTime      = 1,
      eSkipTime         = 2,
      eSkipKeyMouse     = 3,
      eSkipMouseTime    = 4,
      eSkipKey          = 5,
      eSkipMouse        = 6
    };

*Used by:* [Speech.SkipStyle](Speech#skipstyle)

    enum eVoiceMode {
      eSpeechTextOnly,
      eSpeechVoiceAndText,
      eSpeechVoiceOnly
    };

*Used by:* [Speech.VoiceMode](Speech#voicemode)

    enum DialogOptionState {
      eOptionOff,
      eOptionOn,
      eOptionOffForever
    };

*Used by:* [Dialog.GetOptionState](Dialog#getoptionstate),
[Dialog.SetOptionState](Dialog#setoptionstate)

    enum CutsceneSkipType {
      eSkipESCOnly,
      eSkipAnyKey,
      eSkipMouseClick,
      eSkipAnyKeyOrMouseClick,
      eSkipESCOrRightButton
    };

*Used by:* [StartCutscene](Globalfunctions_General#startcutscene)

    enum eOperatingSystem {
      eOSDOS,
      eOSWindows,
      eOSLinux,
      eOSMacOS,
      eOSAndroid,
      eOSiOS,
      eOSPSP
    };

*Used by:* [System.OperatingSystem](System#operatingsystem)

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

*Used by:* [CDAudio](Multimedia#cdaudio)

    enum CursorMode {
      eModeXXXX,
      eModeXXXX,
      ...
    };

The CursorMode enumeration is generated automatically based on your
mouse cursors. The cursor mode name is taken, all its spaces are
removed, and *eMode* is added to the front.<br>
*Used by:* [IsInteractionAvailable](Globalfunctions_General#isinteractionavailable),
[Room.ProcessClick](Room#processclick),
[Mouse.ChangeModeGraphic](Mouse#changemodegraphic),
[Mouse.ChangeModeHotspot](Mouse#changemodehotspot),
[Mouse.DisableMode](Mouse#disablemode),
[Mouse.EnableMode](Mouse#enablemode),
[Mouse.IsModeEnabled](Mouse#ismodeenabled),
[Mouse.UseModeGraphic](Mouse#usemodegraphic),
[Mouse.Mode](Mouse#mode),
[InventoryItem.IsInteractionAvailable](InventoryItem#isinteractionavailable),
[InventoryItem.RunInteraction](InventoryItem#runinteraction),
[Hotspot.IsInteractionAvailable](Hotspot#isinteractionavailable),
[Hotspot.RunInteraction](Hotspot#runinteraction),
[Object.IsInteractionAvailable](Object#isinteractionavailable),
[Object.RunInteraction](Object#runinteraction),
[Character.IsInteractionAvailable](Character#isinteractionavailable),
[Character.RunInteraction](Character#runinteraction)

    enum FontType {
      eFontXXXX,
      eFontXXXX,
      ...
    };

The FontType enumeration is generated automatically based on your fonts.
The font name is taken, all its spaces are removed, and *eFont* is added
to the front.<br>
*Used by:* [Button.Font](Button#font),
[DrawingSurface.DrawMessageWrapped](DrawingSurfaceFunctions#drawmessagewrapped),
[DrawingSurface.DrawString](DrawingSurfaceFunctions#drawstring),
[DrawingSurface.DrawStringWrapped](DrawingSurfaceFunctions#drawstringwrapped),
[Game.NormalFont](Game#normalfont),
[Game.SpeechFont](Game#speechfont),
[GetTextHeight](Globalfunctions_General#gettextheight),
[GetTextWidth](Globalfunctions_General#gettextwidth),
[Label.Font](Label#font),
[ListBox.Font](ListBox#font),
[TextBox.Font](TextBox#font),
[Overlay.CreateTextual](Overlay#createtextual),
[Overlay.SetText](Overlay#settext)

    enum LocationType {
      eLocationNothing,
      eLocationHotspot,
      eLocationCharacter,
      eLocationObject
    };

*Returned by:* [GetLocationType](Globalfunctions_General#getlocationtype)

    enum FileMode {
      eFileRead,
      eFileWrite,
      eFileAppend
    };

*Used by:* [File.Open](File#open)

    enum FileSeek {
      eSeekBegin = 0,
      eSeekCurrent = 1,
      eSeekEnd = 2
    };

*Used by:* [File.Seek](File#seek)

    enum DialogOptionSayStyle {
      eSayUseOptionSetting,
      eSayAlways,
      eSayNever
    };

*Used by:* [Dialog.DisplayOptions](Dialog#displayoptions)

    enum VideoSkipStyle {
      eVideoSkipNotAllowed,
      eVideoSkipEscKey,
      eVideoSkipAnyKey,
      eVideoSkipAnyKeyOrMouse
    };

*Used by:* [PlayVideo](Multimedia#playvideo)

    enum AudioFileType {
      eAudioFileOGG,
      eAudioFileMP3,
      eAudioFileWAV,
      eAudioFileVOC,
      eAudioFileMIDI,
      eAudioFileMOD
    };

*Used by:* [AudioClip.FileType](AudioClip#filetype)

    enum AudioPriority {
      eAudioPriorityVeryLow = 1,
      eAudioPriorityLow = 25,
      eAudioPriorityNormal = 50,
      eAudioPriorityHigh = 75,
      eAudioPriorityVeryHigh = 100
    };

*Used by:* [AudioClip.Play](AudioClip#play),
[AudioClip.PlayFrom](AudioClip#playfrom),
[AudioClip.PlayQueued](AudioClip#playqueued)

    enum GUIPopupStyle {
      eGUIPopupNormal = 0,
      eGUIPopupMouseYPos = 1,
      eGUIPopupModal = 2,
      eGUIPopupPersistent = 3
    };

*Supported by:* AGS 3.5.0 and higher.

*Used by:* [GUI.PopupStyle](GUI#popupstyle)

    enum StringCompareStyle {
      eCaseInsensitive = 0,
      eCaseSensitive = 1
    };

*Supported by:* AGS 3.5.0 and higher.

*Used by:* [Dictionary.Create](Dictionary#create),
[Set.Create](Set#create),
[String.CompareTo](String#compareto),
[String.EndsWith](String#endswith),
[String.Replace](String#replace),
[String.StartsWith](String#startswith)

    enum SortStyle {
      eNonSorted = 0,
      eSorted = 1
    };

*Supported by:* AGS 3.5.0 and higher.

*Used by:* [Dictionary.Create](Dictionary#create),
[Set.Create](Set#create)
