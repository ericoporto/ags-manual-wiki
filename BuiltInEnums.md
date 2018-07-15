Built-in enumerated types
-------------------------

AGS has several [enumerated types](enum) built in. These are
used in calls to various commands, and will usually pop up automatically
in autocomplete. However, for times where autocomplete doesn't do the
job, having a manual reference is invaluable:

    enum BlockingStyle {
      eBlock,
      eNoBlock
    };

*Used by:* [Character.Animate](Character#Animate),
[Character.FaceCharacter](Character#FaceCharacter),
[Character.FaceLocation](Character#FaceLocation),
[Character.FaceObject](Character#FaceObject),
[Character.Move](Character#Move),
[Character.Walk](Character#Walk),
[Character.WalkStraight](Character#WalkStraight),
[Object.Animate](Object#Animate),
[Object.Move](Object#Move)

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

*Used by:* [Character.ChangeRoom](Character#ChangeRoom),
[Character.FaceDirection](Character#FaceDirection)

    enum Direction {
      eForwards,
      eBackwards
    };

*Used by:* [Character.Animate](Character#Animate),
[Object.Animate](Object#Animate)

    enum WalkWhere {
      eAnywhere,
      eWalkableAreas
    };

*Used by:* [Character.Move](Character#Move),
[Character.Walk](Character#Walk),
[Object.Move](Object#Move)

    enum StopMovementStyle
    {
      eKeepMoving = 0,
      eStopMoving = 1
    };

*Used by:* [Character.LockView](Character#LockViewAligned),
[Character.LockViewFrame](Character#LockViewOffset)

    enum RepeatStyle {
      eOnce,
      eRepeat
    };

*Used by:* [Button.Animate](topic54#Button.Animate),
[Character.Animate](Character#Animate),
[Object.Animate](Object#Animate)

    enum Alignment {
      eAlignLeft,
      eAlignCentre,
      eAlignRight
    };

*Used by:*
[Character.LockViewAligned](Character#LockViewAligned)

    enum eFlipDirection {
      eFlipLeftToRight,
      eFlipUpsideDown,
      eFlipBoth
    };

*Used by:* [DynamicSprite.Flip](DynamicSprite#Flip)

    enum TransitionStyle {
      eTransitionFade,
      eTransitionInstant,
      eTransitionDissolve,
      eTransitionBoxout,
      eTransitionCrossfade
    };

*Used by:* [SetScreenTransition](topic70#SetScreenTransition),
[SetNextScreenTransition](topic70#SetNextScreenTransition)

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

*Used by:* [Mouse.IsButtonDown](topic62#Mouse.IsButtonDown)\
*Passed into:* on\_mouse\_click

    enum EventType {
      eEventLeaveRoom,
      eEventEnterRoom,
      eEventGotScore,
      eEventGUIMouseDown,
      eEventGUIMouseUp,
      eEventAddInventory,
      eEventLoseInventory,
      eEventRestoreGame
    };

*Passed into:* on\_event

    enum RoundDirection {
      eRoundDown,
      eRoundNearest,
      eRoundUp
    };

*Used by:* [FloatToInt](topic61#FloatToInt)

    enum eSpeechStyle {
      eSpeechLucasarts,
      eSpeechSierra,
      eSpeechSierraWithBackground,
      eSpeechFullScreen
    };

*Used by:* [Speech.Style](Speech#Style)

    enum SkipSpeechStyle {
      eSkipKeyMouseTime = 0,
      eSkipKeyTime      = 1,
      eSkipTime         = 2,
      eSkipKeyMouse     = 3,
      eSkipMouseTime    = 4,
      eSkipKey          = 5,
      eSkipMouse        = 6
    };

*Used by:* [Speech.SkipStyle](Speech#SkipStyle)

    enum eVoiceMode {
      eSpeechTextOnly,
      eSpeechVoiceAndText,
      eSpeechVoiceOnly
    };

*Used by:* [Speech.VoiceMode](Speech#VoiceMode)

    enum DialogOptionState {
      eOptionOff,
      eOptionOn,
      eOptionOffForever
    };

*Used by:* [Dialog.GetOptionState](topic50#Dialog.GetOptionState),
[Dialog.SetOptionState](topic50#Dialog.SetOptionState)

    enum CutsceneSkipType {
      eSkipESCOnly,
      eSkipAnyKey,
      eSkipMouseClick,
      eSkipAnyKeyOrMouseClick,
      eSkipESCOrRightButton
    };

*Used by:* [StartCutscene](Game#StartCutscene)

    enum eOperatingSystem {
      eOSDOS,
      eOSWindows,
      eOSLinux,
      eOSMacOS,
      eOSAndroid,
      eOSiOS,
      eOSPSP
    };

*Used by:* [System.OperatingSystem](topic72#System.OperatingSystem)

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

*Used by:* [CDAudio](Game#CDAudio)

    enum CursorMode {
      eModeXXXX,
      eModeXXXX,
      ...
    };

The CursorMode enumeration is generated automatically based on your
mouse cursors. The cursor mode name is taken, all its spaces are
removed, and *eMode* is added to the front.\
*Used by:* [IsInteractionAvailable](Game#IsInteractionAvailable),
[Room.ProcessClick](Room#ProcessClick),
[Mouse.ChangeModeGraphic](topic62#Mouse.ChangeModeGraphic),
[Mouse.ChangeModeHotspot](topic62#Mouse.ChangeModeHotspot),
[Mouse.DisableMode](topic62#Mouse.DisableMode),
[Mouse.EnableMode](topic62#Mouse.EnableMode),
[Mouse.IsModeEnabled](topic62#Mouse.IsModeEnabled),
[Mouse.UseModeGraphic](topic62#Mouse.UseModeGraphic),
[Mouse.Mode](topic62#Mouse.Mode),
[InventoryItem.IsInteractionAvailable](InventoryItem#IsInteractionAvailable),
[InventoryItem.RunInteraction](InventoryItem#RunInteraction),
[Hotspot.IsInteractionAvailable](Hotspot#IsInteractionAvailable),
[Hotspot.RunInteraction](Hotspot#RunInteraction),
[Object.IsInteractionAvailable](Object#IsInteractionAvailable),
[Object.RunInteraction](Object#RunInteraction),
[Character.IsInteractionAvailable](Character#IsInteractionAvailable),
[Character.RunInteraction](Character#RunInteraction)

    enum FontType {
      eFontXXXX,
      eFontXXXX,
      ...
    };

The FontType enumeration is generated automatically based on your fonts.
The font name is taken, all its spaces are removed, and *eFont* is added
to the front.\
*Used by:* [Button.Font](topic54#Button.Font),
[DrawingSurface.DrawMessageWrapped](DrawingSurfaceFunctions#DrawingSurface.DrawMessageWrapped),
[DrawingSurface.DrawString](DrawingSurfaceFunctions#DrawingSurface.DrawString),
[DrawingSurface.DrawStringWrapped](DrawingSurfaceFunctions#DrawingSurface.DrawStringWrapped),
[Game.NormalFont](Game#NormalFont),
[Game.SpeechFont](Game#SpeechFont),
[GetTextHeight](Game#GetTextHeight),
[GetTextWidth](Game#GetTextWidth),
[Label.Font](topic55#Label.Font),
[ListBox.Font](topic56#ListBox.Font),
[TextBox.Font](topic58#TextBox.Font),
[Overlay.CreateTextual](topic65#Overlay.CreateTextual),
[Overlay.SetText](topic65#Overlay.SetText)

    enum LocationType {
      eLocationNothing,
      eLocationHotspot,
      eLocationCharacter,
      eLocationObject
    };

*Returned by:* [GetLocationType](Game#GetLocationType)

    enum FileMode {
      eFileRead,
      eFileWrite,
      eFileAppend
    };

*Used by:* [File.Open](topic52#File.Open)

    enum FileSeek {
      eSeekBegin = 0,
      eSeekCurrent = 1,
      eSeekEnd = 2
    };

*Used by:* [File.Seek](topic52#File.Seek)

    enum DialogOptionSayStyle {
      eSayUseOptionSetting,
      eSayAlways,
      eSayNever
    };

*Used by:* [Dialog.DisplayOptions](topic50#Dialog.DisplayOptions)

    enum VideoSkipStyle {
      eVideoSkipNotAllowed,
      eVideoSkipEscKey,
      eVideoSkipAnyKey,
      eVideoSkipAnyKeyOrMouse
    };

*Used by:* [PlayVideo](Game#PlayVideo)

    enum AudioFileType {
      eAudioFileOGG,
      eAudioFileMP3,
      eAudioFileWAV,
      eAudioFileVOC,
      eAudioFileMIDI,
      eAudioFileMOD
    };

*Used by:* [AudioClip.FileType](AudioClip#FileType)

    enum AudioPriority {
      eAudioPriorityVeryLow = 1,
      eAudioPriorityLow = 25,
      eAudioPriorityNormal = 50,
      eAudioPriorityHigh = 75,
      eAudioPriorityVeryHigh = 100
    };

*Used by:* [AudioClip.Play](AudioClip#Play),
[AudioClip.PlayFrom](AudioClip#PlayFrom),
[AudioClip.PlayQueued](AudioClip#PlayQueued)
