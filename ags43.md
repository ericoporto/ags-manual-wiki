Built-in enumerated types
-------------------------

AGS has several [enumerated types](ags44#enum) built in. These are
used in calls to various commands, and will usually pop up automatically
in autocomplete. However, for times where autocomplete doesn't do the
job, having a manual reference is invaluable:

    enum BlockingStyle {
      eBlock,
      eNoBlock
    };

*Used by:* [Character.Animate](ags47#Character.Animate),
[Character.FaceCharacter](ags47#Character.FaceCharacter),
[Character.FaceLocation](ags47#Character.FaceLocation),
[Character.FaceObject](ags47#Character.FaceObject),
[Character.Move](ags47#Character.Move),
[Character.Walk](ags47#Character.Walk),
[Character.WalkStraight](ags47#Character.WalkStraight),
[Object.Animate](ags68#Object.Animate),
[Object.Move](ags68#Object.Move)

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

*Used by:* [Character.ChangeRoom](ags47#Character.ChangeRoom),
[Character.FaceDirection](ags47#Character.FaceDirection)

    enum Direction {
      eForwards,
      eBackwards
    };

*Used by:* [Character.Animate](ags47#Character.Animate),
[Object.Animate](ags68#Object.Animate)

    enum WalkWhere {
      eAnywhere,
      eWalkableAreas
    };

*Used by:* [Character.Move](ags47#Character.Move),
[Character.Walk](ags47#Character.Walk),
[Object.Move](ags68#Object.Move)

    enum StopMovementStyle
    {
      eKeepMoving = 0,
      eStopMoving = 1
    };

*Used by:* [Character.LockView](ags47#Character.LockViewAligned),
[Character.LockViewFrame](ags47#Character.LockViewOffset)

    enum RepeatStyle {
      eOnce,
      eRepeat
    };

*Used by:* [Button.Animate](ags57#Button.Animate),
[Character.Animate](ags47#Character.Animate),
[Object.Animate](ags68#Object.Animate)

    enum Alignment {
      eAlignLeft,
      eAlignCentre,
      eAlignRight
    };

*Used by:*
[Character.LockViewAligned](ags47#Character.LockViewAligned)

    enum eFlipDirection {
      eFlipLeftToRight,
      eFlipUpsideDown,
      eFlipBoth
    };

*Used by:* [DynamicSprite.Flip](ags52#DynamicSprite.Flip)

    enum TransitionStyle {
      eTransitionFade,
      eTransitionInstant,
      eTransitionDissolve,
      eTransitionBoxout,
      eTransitionCrossfade
    };

*Used by:* [SetScreenTransition](ags74#SetScreenTransition),
[SetNextScreenTransition](ags74#SetNextScreenTransition)

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

*Used by:* [Mouse.IsButtonDown](ags66#Mouse.IsButtonDown)\
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

*Used by:* [FloatToInt](ags65#FloatToInt)

    enum eSpeechStyle {
      eSpeechLucasarts,
      eSpeechSierra,
      eSpeechSierraWithBackground,
      eSpeechFullScreen
    };

*Used by:* [Speech.Style](ags75#Speech.Style)

    enum SkipSpeechStyle {
      eSkipKeyMouseTime = 0,
      eSkipKeyTime      = 1,
      eSkipTime         = 2,
      eSkipKeyMouse     = 3,
      eSkipMouseTime    = 4,
      eSkipKey          = 5,
      eSkipMouse        = 6
    };

*Used by:* [Speech.SkipStyle](ags75#Speech.SkipStyle)

    enum eVoiceMode {
      eSpeechTextOnly,
      eSpeechVoiceAndText,
      eSpeechVoiceOnly
    };

*Used by:* [Speech.VoiceMode](ags75#Speech.VoiceMode)

    enum DialogOptionState {
      eOptionOff,
      eOptionOn,
      eOptionOffForever
    };

*Used by:* [Dialog.GetOptionState](ags49#Dialog.GetOptionState),
[Dialog.SetOptionState](ags49#Dialog.SetOptionState)

    enum CutsceneSkipType {
      eSkipESCOnly,
      eSkipAnyKey,
      eSkipMouseClick,
      eSkipAnyKeyOrMouseClick,
      eSkipESCOrRightButton
    };

*Used by:* [StartCutscene](ags54#StartCutscene)

    enum eOperatingSystem {
      eOSDOS,
      eOSWindows,
      eOSLinux,
      eOSMacOS,
      eOSAndroid,
      eOSiOS,
      eOSPSP
    };

*Used by:* [System.OperatingSystem](ags77#System.OperatingSystem)

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

*Used by:* [CDAudio](ags67#CDAudio)

    enum CursorMode {
      eModeXXXX,
      eModeXXXX,
      ...
    };

The CursorMode enumeration is generated automatically based on your
mouse cursors. The cursor mode name is taken, all its spaces are
removed, and *eMode* is added to the front.\
*Used by:* [IsInteractionAvailable](ags54#IsInteractionAvailable),
[Room.ProcessClick](ags73#Room.ProcessClick),
[Mouse.ChangeModeGraphic](ags66#Mouse.ChangeModeGraphic),
[Mouse.ChangeModeHotspot](ags66#Mouse.ChangeModeHotspot),
[Mouse.DisableMode](ags66#Mouse.DisableMode),
[Mouse.EnableMode](ags66#Mouse.EnableMode), Mouse.IsModeEnabled (REF
NOT FOUND), [Mouse.UseModeGraphic](ags66#Mouse.UseModeGraphic),
[Mouse.Mode](ags66#Mouse.Mode),
[InventoryItem.IsInteractionAvailable](ags64#InventoryItem.IsInteractionAvailable),
[InventoryItem.RunInteraction](ags64#InventoryItem.RunInteraction),
[Hotspot.IsInteractionAvailable](ags63#Hotspot.IsInteractionAvailable),
[Hotspot.RunInteraction](ags63#Hotspot.RunInteraction),
[Object.IsInteractionAvailable](ags68#Object.IsInteractionAvailable),
[Object.RunInteraction](ags68#Object.RunInteraction),
[Character.IsInteractionAvailable](ags47#Character.IsInteractionAvailable),
[Character.RunInteraction](ags47#Character.RunInteraction)

    enum FontType {
      eFontXXXX,
      eFontXXXX,
      ...
    };

The FontType enumeration is generated automatically based on your fonts.
The font name is taken, all its spaces are removed, and *eFont* is added
to the front.\
*Used by:* [Button.Font](ags57#Button.Font),
[DrawingSurface.DrawMessageWrapped](ags51#DrawingSurface.DrawMessageWrapped),
[DrawingSurface.DrawString](ags51#DrawingSurface.DrawString),
[DrawingSurface.DrawStringWrapped](ags51#DrawingSurface.DrawStringWrapped),
[Game.NormalFont](ags54#Game.NormalFont),
[Game.SpeechFont](ags54#Game.SpeechFont),
[GetTextHeight](ags54#GetTextHeight),
[GetTextWidth](ags54#GetTextWidth),
[Label.Font](ags59#Label.Font),
[ListBox.Font](ags60#ListBox.Font),
[TextBox.Font](ags62#TextBox.Font),
[Overlay.CreateTextual](ags69#Overlay.CreateTextual),
[Overlay.SetText](ags69#Overlay.SetText)

    enum LocationType {
      eLocationNothing,
      eLocationHotspot,
      eLocationCharacter,
      eLocationObject
    };

*Returned by:* [GetLocationType](ags54#GetLocationType)

    enum FileMode {
      eFileRead,
      eFileWrite,
      eFileAppend
    };

*Used by:* [File.Open](ags53#File.Open)

    enum FileSeek {
      eSeekBegin = 0,
      eSeekCurrent = 1,
      eSeekEnd = 2
    };

*Used by:* [File.Seek](ags53#File.Seek)

    enum DialogOptionSayStyle {
      eSayUseOptionSetting,
      eSayAlways,
      eSayNever
    };

*Used by:* [Dialog.DisplayOptions](ags49#Dialog.DisplayOptions)

    enum VideoSkipStyle {
      eVideoSkipNotAllowed,
      eVideoSkipEscKey,
      eVideoSkipAnyKey,
      eVideoSkipAnyKeyOrMouse
    };

*Used by:* [PlayVideo](ags67#PlayVideo)

    enum AudioFileType {
      eAudioFileOGG,
      eAudioFileMP3,
      eAudioFileWAV,
      eAudioFileVOC,
      eAudioFileMIDI,
      eAudioFileMOD
    };

*Used by:* [AudioClip.FileType](ags46#AudioClip.FileType)

    enum AudioPriority {
      eAudioPriorityVeryLow = 1,
      eAudioPriorityLow = 25,
      eAudioPriorityNormal = 50,
      eAudioPriorityHigh = 75,
      eAudioPriorityVeryHigh = 100
    };

*Used by:* [AudioClip.Play](ags46#AudioClip.Play),
[AudioClip.PlayFrom](ags46#AudioClip.PlayFrom),
[AudioClip.PlayQueued](ags46#AudioClip.PlayQueued)
