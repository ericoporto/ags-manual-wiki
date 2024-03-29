## Obsolete Script API

As new versions of AGS are released this sometimes bring changes to the script commands. Following table lists the functions and variables removed from the Script API, their replacements (when available) and the version in which the change took place.

| Obsolete API | Superseded by | Obsoleted in Version |
|-|-|-|
| `AddInventory` | [`Character.AddInventory`](Character#characteraddinventory) | |
| `AddInventoryToCharacter` | [`Character.AddInventory`](Character#characteraddinventory) | |
| `AnimateCharacter` | [`Character.Animate`](Character#characteranimate) | |
| `AnimateCharacterEx` | [`Character.Animate`](Character#characteranimate) | |
| `AnimateObject` | [`Object.Animate`](Object#objectanimate) | |
| `AnimateObjectEx` | [`Object.Animate`](Object#objectanimate) | |
| `AreCharactersColliding` | [`Character.IsCollidingWithChar`](Character#characteriscollidingwithchar) | |
| `AreCharObjColliding` | [`Character.IsCollidingWithObject`](Character#characteriscollidingwithobject) | |
| `AreObjectsColliding` | [`Object.IsCollidingWithObject`](Object#objectiscollidingwithobject) | |
| `Button.GetText` | [`Button.Text`](Button#buttontext) | |
| `Button.SetText` | [`Button.Text`](Button#buttontext) | |
| `CDAudio` | [`Use AudioClips`](Multimedia#cdaudio) | |
| `CentreGUI` | [`GUI.Centre`](GUI#guicentre) | |
| `ChangeCharacterView` | [`Character.ChangeView`](Character#characterchangeview) | |
| `ChangeCursorGraphic` | [`Mouse.ChangeModeGraphic`](Mouse#mousechangemodegraphic) | |
| `ChangeCursorHotspot` | [`Mouse.ChangeModeHotspot`](Mouse#mousechangemodehotspot) | |
| `Character.GetPropertyText` | [`Character.GetTextProperty`](Character#charactergettextproperty) | |
| [`Character.IgnoreWalkbehinds`](Character#characterignorewalkbehinds) | design your rooms without it and rely on [`Character.Baseline`](Character#characterbaseline) instead | 3.5.0 |
| `Character.IgnoreScaling` | [`Character.ManualScaling`](Character#charactermanualscaling)  | |
| `character[].activeinv` | [`Character.ActiveInventory`](Character#characteractiveinventory) | |
| `character[].animating` | [`Character.Animating`](Character#characteranimating) | |
| `character[].animspeed` | [`Character.AnimationSpeed`](Character#characteranimationspeed) | |
| `character[].defview` | [`Character.NormalView`](Character#characternormalview) | |
| `character[].frame` | [`Character.Frame`](Character#characterframe) | |
| `character[].inv` | [`Character.InventoryQuantity[]`](Character#characterinventoryquantity) | |
| `character[].loop` | [`Character.Loop`](Character#characterloop) | |
| `character[].name` | [`Character.Name`](Character#charactername) | |
| `character[].prevroom` | [`Character.PreviousRoom`](Character#characterpreviousroom) | |
| `character[].room` | [`Character.Room`](Character#characterroom) | |
| `character[].talkview` | [`Character.SpeechView`](Character#characterspeechview) | |
| `character[].thinkview` | [`Character.ThinkView`](Character#characterthinkview) | |
| `character[].walking` | [`Character.Moving`](Character#charactermoving) | |
| `CreateGraphicOverlay` | [`Overlay.CreateGraphical`](Overlay#overlaycreategraphical) | |
| `CreateTextOverlay` | [`Overlay.CreateTextual`](Overlay#overlaycreatetextual) | |
| `DeleteSprite` | [`DynamicSprite.Delete`](DynamicSprite#dynamicspritedelete) | |
| `DisableCursorMode` | [`Mouse.DisableMode`](Mouse#mousedisablemode) | |
| `DisableHotspot` | [`Hotspot.Enabled`](Hotspot#hotspotenabled) | |
| `DisableRegion` | [`Region.Enabled`](Region#regionenabled) | |
| `DisplaySpeech` | [`Character.Say`](Character#charactersay) | |
| `DisplaySpeechAt` | [`Character.SayAt`](Character#charactersayat) | |
| `DisplaySpeechBackground` | [`Character.SayBackground`](Character#charactersaybackground) | |
| `DisplayThought` | [`Character.Think`](Character#characterstopmoving) | |
| [`DrawingSurface.UseHighResCoordinates`](DrawingSurface#drawingsurfaceusehighrescoordinates) | This property was used to multiply the coordinates by 2 in 640x400/480 resolution games. | 3.5.0 |
| `EnableCursorMode` | [`Mouse.EnableMode`](Mouse#mouseenablemode) | |
| `EnableHotspot` | [`Hotspot.Enabled`](Hotspot#hotspotenabled) | |
| `EnableRegion` | [`Region.Enabled`](Region#regionenabled) | |
| `FaceCharacter` | [`Character.FaceCharacter`](Character#characterfacecharacter) | |
| `FaceLocation` | [`Character.FaceLocation`](Character#characterfacelocation) | |
| `File.ReadRawLine` | [`File.ReadRawLineBack`](File#filereadrawlineback) | |
| `File.ReadString` | [`File.ReadStringBack`](File#filereadstringback) | |
| `FileClose` | [`File.Close`](File#fileclose) | |
| `FileIsEOF` | [`File.EOF`](File#fileeof) | |
| `FileOpen` | [`File.Open`](File#fileopen) | |
| `FileRead` | [`File.ReadStringBack`](File#filereadstringback) | |
| `FileReadInt` | [`File.ReadInt`](File#filereadint) | |
| `FileReadRawChar` | [`File.ReadRawChar`](File#filereadrawchar) | |
| `FileReadRawInt` | [`File.ReadRawInt`](File#filereadrawint) | |
| `FileWrite` | [`File.WriteString`](File#filewritestring) | |
| `FileWriteInt` | [`File.WriteInt`](File#filewriteint) | |
| `FileWriteRawChar` | [`File.WriteRawChar`](File#filewriterawchar) | |
| `FileWriteRawLine` | [`File.WriteRawLine`](File#filewriterawline) | |
| `FollowCharacter` | [`Character.FollowCharacter`](Character#characterfollowcharacter) | |
| `FollowCharacterEx` | [`Character.FollowCharacter`](Character#characterfollowcharacter) | |
| `game.close_mouth_end_speech_time` | [`Speech.AnimationStopTimeMargin`](Speech#speechanimationstoptimemargin) | |
| `game.in_cutscene` | [`Game.InSkippableCutscene`](Game#gameinskippablecutscene) | |
| `game.items_per_line` | [`InvWindow.ItemsPerRow`](InvWindow#invwindowitemsperrow) | |
| `game.num_inv_items` | [`InvWindow.ItemCount`](InvWindow#invwindowitemcount) | |
| `game.room_height` | [`Room.Height`](Room#roomheight) | |
| `game.room_width` | [`Room.Width`](Room#roomwidth) | |
| `game.skip_speech_specific_key` | [`Speech.SkipKey`](Speech#speechskipkey) | |
| `game.skipping_cutscene` | [`Game.SkippingCutscene`](Game#gameskippingcutscene) | |
| `game.speech_music_drop` | [`Game.SetAudioTypeSpeechVolumeDrop`](Game#gamesetaudiotypespeechvolumedrop) | |
| `game.speech_text_align` | [`Speech.TextAlignment`](Speech#speechtextalignment) | |
| `Game.StopSound` | [`Game.StopAudio`](Game#gamestopaudio) | |
| `game.talkanim_speed` | [`Speech.GlobalSpeechAnimationDelay`](Speech#speechglobalspeechanimationdelay) | |
| `game.text_speed` | [`Game.TextReadingSpeed`](Game#gametextreadingspeed) | |
| `game.top_inv_item` | [`InvWindow.TopItem`](InvWindow#invwindowtopitem) | |
| [`Game.GlobalMessage`](Game#gameglobalmessages) | Create a [global](ScriptKeywords#export) [array](ScriptKeywords#arrays) of [strings](String). | 3.X |
| `GetButtonPic` | [`Button.Graphic`](Button#buttongraphic) | |
| `GetCharacterAt` | [`Character.GetAtScreenXY`](Character#charactergetatscreenxy) | |
| `GetCharacterProperty` | [`Character.GetProperty`](Character#charactergetproperty) | |
| `GetCharacterPropertyText` | [`Character.GetTextProperty`](Character#charactergettextproperty) | |
| `GetCurrentMusic` | [`AudioChannel.PlayingClip`](AudioChannel#audiochannelplayingclip) | |
| `GetCursorMode` | [`Mouse.Mode`](Mouse#mousemode) | |
| `GetDialogOption` | [`Dialog.GetOptionState`](Dialog#dialoggetoptionstate) | |
| `GetGameParameter(GP_FRAMExxx)` | [`Game.GetViewFrame`](Game#gamegetviewframe) | |
| `GetGameParameter(GP_ISFRAMEFLIPPED)` | [`Game.GetViewFrame`](Game#gamegetviewframe) | |
| `GetGameParameter(GP_NUMCHARACTERS)` | [`Game.CharacterCount`](Game#gamecharactercount) | |
| `GetGameParameter(GP_NUMFRAMES)` | [`Game.GetFrameCountForLoop`](Game#gamegetframecountforloop) | |
| `GetGameParameter(gp_numguis)` | [`Game.GUICount`](Game#gameguicount) | |
| `GetGameParameter(GP_NUMINVITEMS)` | [`Game.InventoryItemCount`](Game#gameinventoryitemcount) | |
| `GetGameParameter(GP_NUMLOOPS)` | [`Game.GetLoopCountForView`](Game#gamegetloopcountforview) | |
| `GetGameParameter(gp_numobjects)` | [`Room.ObjectCount`](Room#roomobjectcount) | |
| `GetGameParameter(gp_spriteheight)` | [`Game.SpriteHeight`](Game#gamespriteheight) | |
| `GetGameParameter(gp_spritewidth)` | [`Game.SpriteWidth`](Game#gamespritewidth) | |
| `GetGlobalInt` | [`Global Variables`](GlobalVariables) | |
| `GetGlobalString` | [`Global Variables`](GlobalVariables) | |
| `GetGraphicalVariable` | [`Global Variables`](GlobalVariables) | |
| `GetGUIAt` | [`GUI.GetAtScreenXY`](GUI#guigetatscreenxy) | |
| `GetGUIObjectAt` | [`GUIControl.GetAtScreenXY`](GUIControl#guicontrolgetatscreenxy) | |
| `GetHotspotAt` | [`Hotspot.GetAtScreenXY`](Hotspot#hotspotgetatscreenxy) | |
| `GetHotspotName` | [`Hotspot.Name`](Hotspot#hotspotname) | |
| `GetHotspotPointX` | [`Hotspot.WalkToX`](Hotspot#hotspotwalktox) | |
| `GetHotspotPointY` | [`Hotspot.WalkToY`](Hotspot#hotspotwalktoy) | |
| `GetHotspotProperty` | [`Hotspot.GetProperty`](Hotspot#hotspotgetproperty) | |
| `GetHotspotPropertyText` | [`Hotspot.GetTextProperty`](Hotspot#hotspotgettextproperty) | |
| `GetInvAt` | [`InventoryItem.GetAtScreenXY`](InventoryItem#inventoryitemgetatscreenxy) | |
| `GetInvGraphic` | [`InventoryItem.Graphic`](InventoryItem#inventoryitemgraphic) | |
| `GetInvName` | [`InventoryItem.Name`](InventoryItem#inventoryitemname) | |
| `GetInvProperty` | [`InventoryItem.GetProperty`](InventoryItem#inventoryitemgetproperty) | |
| `GetInvPropertyText` | [`InventoryItem.GetTextProperty`](InventoryItem#inventoryitemgettextproperty) | |
| `GetLocationName` | [`Game.GetLocationName`](Game#gamegetlocationname) | |
| [`GetMessageText`](Game#gameglobalmessages) | Create a [global](ScriptKeywords#export) [array](ScriptKeywords#arrays) of [strings](String). | 3.X |
| `GetMIDIPosition` | [`AudioChannel.Position`](AudioChannel#audiochannelposition) | |
| `GetMODPattern` | [`AudioChannel.Position`](AudioChannel#audiochannelposition) | |
| `GetMP3PosMillis` | [`AudioChannel.Position`](AudioChannel#audiochannelposition) | |
| `GetObjectAt` | [`Object.GetAtScreenXY`](Object#objectgetatscreenxy) | |
| `GetObjectBaseline` | [`Object.Baseline`](Object#objectbaseline) | |
| `GetObjectGraphic` | [`Object.Graphic`](Object#objectgraphic) | |
| `GetObjectName` | [`Object.Name`](Object#objectname) | |
| `GetObjectProperty` | [`Object.GetProperty`](Object#objectgetproperty) | |
| `GetObjectPropertyText` | [`Object.GetTextProperty`](Object#objectgettextproperty) | |
| `GetObjectX` | [`Object.X`](Object#objectx) | |
| `GetObjectY` | [`Object.Y`](Object#objecty) | |
| `GetPlayerCharacter` | Use `player` pointer | |
| `GetRawTime` | [`DateTime.RawTime`](DateTime#datetimerawtime) | |
| `GetRegionAt` | [`Region.GetAtRoomXY`](Region#regiongetatroomxy) | |
| `GetRoomProperty` | [`Room.GetProperty`](Room#roomgetproperty) | |
| `GetRoomPropertyText` | [`Room.GetTextProperty`](Room#roomgettextproperty) | |
| `GetSaveSlotDescription` | [`Game.GetSaveSlotDescription`](Game#gamegetsaveslotdescription) | |
| `GetSliderValue` | [`Slider.Value`](Slider#slidervalue) | |
| `GetTextBoxText` | [`TextBox.Text`](TextBox#textboxtext) | |
| `GetTime` | [`DateTime.Now`](DateTime#datetimenow) | |
| `GetTranslationName` | [`Game.TranslationFilename`](Game#gametranslationfilename) | |
| `GetViewportX` | [`Game.Camera.X`](Camera#camerax) | |
| `GetViewportY` | [`Game.Camera.Y`](Camera#cameray) | |
| `GetWalkableAreaAt` | [`GetWalkableAreaAtScreen`](Globalfunctions_Room#getwalkableareaatscreen) | |
| `GUIOff` | [`GUI.Visible`](GUI#guivisible) | |
| `GUIOn` | [`GUI.Visible`](GUI#guivisible) | |
| `HideMouseCursor` | [`Mouse.Visible`](Mouse#mousevisible) | |
| `Hotspot.GetName` | [`Hotspot.Name`](Hotspot#hotspotname) | |
| `Hotspot.GetPropertyText` | [`Hotspot.GetTextProperty`](Hotspot#hotspotgettextproperty) | |
| `InputBox` | [`Game.InputBox`](Game#gameinputbox) | |
| `InterfaceOff` | [`GUI.Visible`](GUI#guivisible) | |
| `InterfaceOn` | [`GUI.Visible`](GUI#guivisible) | |
| `InventoryItem.GetName` | [`InventoryItem.Name`](InventoryItem#inventoryitemname) | |
| `InventoryItem.GetPropertyText` | [`InventoryItem.GetTextProperty`](InventoryItem#inventoryitemgettextproperty) | |
| `InventoryItem.SetName` | [`InventoryItem.Name`](InventoryItem#inventoryitemname) | |
| `InventoryScreen` | [create your own Inventory GUI](EditorGUI) | |
| `IsButtonDown` | [`Mouse.IsButtonDown`](Mouse#mouseisbuttondown) | |
| `IsChannelPlaying` | [`AudioChannel.IsPlaying`](AudioChannel#audiochannelisplaying) | |
| `IsGUIOn` | [`GUI.Visible`](GUI#guivisible) | |
| `IsInventoryInteractionAvailable` | [`InventoryItem.IsInteractionAvailable`](InventoryItem#inventoryitemisinteractionavailable) | |
| `IsMusicVoxAvailable` | [`AudioClip.IsAvailable`](AudioClip#audioclipisavailable) | |
| `IsObjectAnimating` | [`Object.Animating`](Object#objectanimating) | |
| `IsObjectMoving` | [`Object.Moving`](Object#objectmoving) | |
| `IsObjectOn` | [`Object.Visible`](Object#objectvisible) | |
| `IsOverlayValid` | [`Overlay.Valid`](Overlay#overlayvalid) | |
| `Label.GetText` | [`Label.Text`](Label#labeltext) | |
| `Label.SetText` | [`Label.Text`](Label#labeltext) | |
| `ListBox.GetItemText` | [`ListBox.Items[]`](ListBox#listboxitems) | |
| `ListBox.HideBorder` | [`ListBox.ShowBorder`](ListBox#listboxshowborder) | |
| `ListBox.HideScrollArrows` | [`ListBox.ShowScrollArrows`](ListBox#listboxshowscrollarrows) | |
| `ListBox.SetItemText` | [`ListBox.Items[]`](ListBox#listboxitems) | |
| `ListBoxAdd` | [`ListBox.AddItem`](ListBox#listboxadditem) | |
| `ListBoxClear` | [`ListBox.Clear`](ListBox#listboxclear) | |
| `ListBoxDirList` | [`ListBox.FillDirList`](ListBox#listboxfilldirlist) | |
| `ListBoxGetItemText` | [`ListBox.Items[]`](ListBox#listboxitems) | |
| `ListBoxGetNumItems` | [`ListBox.ItemCount`](ListBox#listboxitemcount) | |
| `ListBoxGetSelected` | [`ListBox.SelectedIndex`](ListBox#listboxselectedindex) | |
| `ListBoxRemove` | [`ListBox.RemoveItem`](ListBox#listboxremoveitem) | |
| `ListBoxSaveGameList` | [`ListBox.FillSaveGameList`](ListBox#listboxfillsavegamelist) | |
| `ListBoxSetSelected` | [`ListBox.SelectedIndex`](ListBox#listboxselectedindex) | |
| `ListBoxSetTopItem` | [`ListBox.TopItem`](ListBox#listboxtopitem) | |
| `LoadImageFile` | [`DynamicSprite.CreateFromFile`](DynamicSprite#dynamicspritecreatefromfile) | |
| `LoadSaveSlotScreenshot` | [`DynamicSprite.CreateFromSaveGame`](DynamicSprite#dynamicspritecreatefromsavegame) | |
| `LoseInventory` | [`Character.LoseInventory`](Character#characterloseinventory) | |
| `LoseInventoryFromCharacter` | [`Character.LoseInventory`](Character#characterloseinventory) | |
| `MergeObject` | [`Object.MergeIntoBackground`](Object#objectmergeintobackground) | |
| `MoveCharacter` | [`Character.Walk`](Character#characterwalk) | |
| `MoveCharacterBlocking` | [`Character.Walk`](Character#characterwalk) | |
| `MoveCharacterDirect` | [`Character.Walk`](Character#characterwalk) | |
| `MoveCharacterPath` | [`Character.AddWaypoint`](Character#characteraddwaypoint) | |
| `MoveCharacterStraight` | [`Character.WalkStraight`](Character#characterwalkstraight) | |
| `MoveCharacterToHotspot` | [`Character.Walk`](Character#characterwalk) and [`Hotspot.WalkToX/Y`](Hotspot#hotspotwalktox) | |
| `MoveCharacterToObject` | [`Character.Walk`](Character#characterwalk) and [`Object.X/Y`](Object#objectx) | |
| `MoveObject` | [`Object.Move`](Object#objectmove) | |
| `MoveObjectDirect` | [`Object.Move`](Object#objectmove) | |
| `MoveOverlay` | [`Overlay.X`](Overlay#overlayx) | |
| `MoveToWalkableArea` | [`Character.PlaceOnWalkableArea`](Character#characterplaceonwalkablearea) | |
| `NewRoom` | [`Character.ChangeRoom`](Character#characterchangeroom) | |
| `NewRoomEx` | [`Character.ChangeRoom`](Character#characterchangeroom) | |
| `NewRoomNPC` | [`Character.ChangeRoom`](Character#characterchangeroom) | |
| `Object.GetName` | [`Object.Name`](Object#objectname) | |
| `Object.GetPropertyText` | [`Object.GetTextProperty`](Object#objectgettextproperty) | |
| [`Object.IgnoreWalkbehinds`](Object#objectignorewalkbehinds) | design your rooms without it and rely on [`Object.Baseline`](Object#objectbaseline) instead | 3.5.0 |
| `ObjectOff` | [`Object.Visible`](Object#objectvisible) | |
| `ObjectOn` | [`Object.Visible`](Object#objectvisible) | |
| `PlayAmbientSound` | [`AudioChannel.SetRoomLocation`](AudioChannel#audiochannelsetroomlocation) | |
| `PlayAmbientSound` | [`AudioClip.Play`](AudioClip#audioclipplay) | |
| `PlayMP3File` | [`AudioClip.Play`](AudioClip#audioclipplay) | |
| `PlayMusic` | [`AudioClip.Play`](AudioClip#audioclipplay) | |
| `PlayMusicQueued` | [`AudioClip.PlayQueued`](AudioClip#audioclipplayqueued) | |
| [`PlaySilentMIDI`](Multimedia#playsilentmidi) | use [`AudioClip.Play`](AudioClip#audioclipplay) command and set its [`Volume`](AudioChannel#audiochannelvolume) property to 0 | |
| `PlaySound` | [`AudioClip.Play`](AudioClip#audioclipplay) | |
| `PlaySoundEx` | [`AudioClip.Play`](AudioClip#audioclipplay) | |
| `ProcessClick` | [`Room.ProcessClick`](Room#roomprocessclick) | |
| `RawClearScreen` | [`DrawingSurface.Clear`](DrawingSurface#drawingsurfaceclear) | |
| `RawDrawCircle` | [`DrawingSurface.DrawCircle`](DrawingSurface#drawingsurfacedrawcircle) | |
| `RawDrawFrameTransparent` | [`DrawingSurface.DrawSurface`](DrawingSurface#drawingsurfacedrawsurface) | |
| `RawDrawImage` | [`DrawingSurface.DrawImage`](DrawingSurface#drawingsurfacedrawimage) | |
| `RawDrawImageResized` | [`DrawingSurface.DrawImage`](DrawingSurface#drawingsurfacedrawimage) | |
| `RawDrawImageTransparent` | [`DrawingSurface.DrawImage`](DrawingSurface#drawingsurfacedrawimage) | |
| `RawDrawLine` | [`DrawingSurface.DrawLine`](DrawingSurface#drawingsurfacedrawline) | |
| `RawDrawRectangle` | [`DrawingSurface.DrawRectangle`](DrawingSurface#drawingsurfacedrawrectangle) | |
| `RawDrawTriangle` | [`DrawingSurface.DrawTriangle`](DrawingSurface#drawingsurfacedrawtriangle) | |
| `RawPrint` | [`DrawingSurface.DrawString`](DrawingSurface#drawingsurfacedrawstring) | |
| `RawPrintMessageWrapped` | [`DrawingSurface.DrawMessageWrapped`](DrawingSurface#drawingsurfacedrawmessagewrapped) | |
| `RawRestoreScreen` | [`DrawingSurface.DrawSurface`](DrawingSurface#drawingsurfacedrawsurface) | |
| `RawSaveScreen` | [`DrawingSurface.CreateCopy`](DrawingSurface#drawingsurfacecreatecopy) | |
| `RawSetColor` | [`DrawingSurface.DrawingColor`](DrawingSurface#drawingsurfacedrawingcolor) | |
| `RawSetColorRGB` | [`Game.GetColorFromRGB`](Game#gamegetcolorfromrgb) | |
| `RefreshMouse` | [`Mouse.Update`](Mouse#mouseupdate) | |
| `ReleaseCharacterView` | [`Character.UnlockView`](Character#characterunlockview) | |
| `ReleaseViewport` | [`Game.Camera.AutoTracking`](Camera#cameraautotracking) | |
| `RemoveObjectTint` | [`Object.RemoveTint`](Object#objectremovetint) | |
| `RemoveOverlay` | [`Overlay.Remove`](Overlay#overlayremove) | |
| [`Room.MusicOnLoad`](Room#roommusiconload) | Use [`AudioClip.Play`](AudioClip#audioclipplay) on the room Load event | |
| `RunCharacterInteraction` | [`Character.RunInteraction`](Character#characterruninteraction) | |
| `RunDialog` | [`Dialog.Start`](Dialog#dialogstart) | |
| `RunHotspotInteraction` | [`Hotspot.RunInteraction`](Hotspot#hotspotruninteraction) | |
| `RunInventoryInteraction` | [`InventoryItem.RunInteraction`](InventoryItem#inventoryitemruninteraction) | |
| `RunObjectInteraction` | [`Object.RunInteraction`](Object#objectruninteraction) | |
| `RunRegionInteraction` | [`RunRegionInteraction`](Region#regionruninteraction) | |
| `SaveCursorForLocationChange` | [`Mouse.SaveCursorUntilItLeaves`](Mouse#mousesavecursoruntilitleaves) | |
| `savegameindex[]` | [`ListBox.SaveGameSlots[]`](ListBox#listboxsavegameslots) | |
| `SeekMIDIPosition` | [`AudioChannel.Seek`](AudioChannel#audiochannelseek) | |
| `SeekMODPattern` | [`AudioChannel.Seek`](AudioChannel#audiochannelseek) | |
| `SeekMP3PosMillis` | [`AudioChannel.Seek`](AudioChannel#audiochannelseek) | |
| `SetActiveInventory` | [`Character.ActiveInventory`](Character#characteractiveinventory) | |
| `SetAreaLightLevel` | [`Region.LightLevel`](Region#regionlightlevel) | |
| `SetButtonPic` | [`Button.NormalGraphic`](Button#buttonnormalgraphic) | |
| `SetButtonText` | [`Button.Text`](Button#buttontext) | |
| `SetChannelVolume` | [`AudioChannel.Volume`](AudioChannel#audiochannelvolume) | |
| `SetCharacterBaseline` | [`Character.Baseline`](Character#characterbaseline) | |
| `SetCharacterBlinkView` | [`Character.BlinkInterval`](Character#characterblinkinterval) | |
| `SetCharacterBlinkView` | [`Character.BlinkView`](Character#characterblinkview) | |
| `SetCharacterClickable` | [`Character.Clickable`](Character#characterclickable) | |
| `SetCharacterFrame` | [`Character.LockViewFrame`](Character#characterlockviewframe) | |
| `SetCharacterIdle` | [`Character.SetIdleView`](Character#charactersetidleview) | |
| `SetCharacterIgnoreLight` | [`Character.IgnoreLighting`](Character#characterignorelighting) | |
| [`SetCharacterIgnoreWalkbehinds`](Character#characterignorewalkbehinds) | design your rooms without it and rely on [`Character.Baseline`](Character#characterbaseline) instead | 3.5.0  |
| `SetCharacterProperty` | [`Character.ManualScaling`](Character#charactermanualscaling)  | |
| `SetCharacterProperty` | [`Character.DiagonalLoops`](Character#characterdiagonalloops) | |
| `SetCharacterProperty` | [`Character.ScaleMoveSpeed`](Character#characterscalemovespeed) | |
| `SetCharacterProperty` | [`Character.Solid`](Character#charactersolid) | |
| `SetCharacterProperty` | [`Character.TurnBeforeWalking`](Character#characterturnbeforewalking) | |
| `SetCharacterSpeechView` | [`Character.SpeechView`](Character#characterspeechview) | |
| `SetCharacterSpeed` | [`Character.SetWalkSpeed`](Character#charactersetwalkspeed) | |
| `SetCharacterSpeedEx` | [`Character.SetWalkSpeed`](Character#charactersetwalkspeed) | |
| `SetCharacterTransparency` | [`Character.Transparency`](Character#charactertransparency) | |
| `SetCharacterView` | [`Character.LockView`](Character#characterlockview) | |
| `SetCharacterViewEx` | [`Character.LockViewAligned`](Character#characterlockviewaligned) | |
| `SetCharacterViewOffset` | [`Character.LockViewOffset`](Character#characterlockviewoffset) | |
| `SetCursorMode` | [`Mouse.Mode`](Mouse#mousemode) | |
| `SetDefaultCursor` | [`Mouse.UseDefaultGraphic`](Mouse#mouseusedefaultgraphic) | |
| `SetDialogOption` | [`Dialog.SetOptionState`](Dialog#dialogsetoptionstate) | |
| `SetDigitalMasterVolume` | [`System.Volume`](System#systemvolume) | |
| `SetFrameSound` | [`ViewFrame.LinkedAudio`](ViewFrame#viewframelinkedaudio) | |
| `SetGlobalInt` | [`Global Variables`](GlobalVariables) | |
| `SetGlobalString` | [`Global Variables`](GlobalVariables) | |
| `SetGraphicalVariable` | [`Global Variables`](GlobalVariables) | |
| `SetGUIBackgroundPic` | [`GUI.BackgroundGraphic`](GUI#guibackgroundgraphic) | |
| `SetGUIClickable` | [`GUI.Clickable`](GUI#guiclickable) | |
| `SetGUIObjectEnabled` | [`GUIControl.Enabled`](GUIControl#guicontrolenabled) | |
| `SetGUIObjectPosition` | [`GUIControl.SetPosition`](GUIControl#guicontrolsetposition) | |
| `SetGUIObjectSize` | [`GUIControl.SetSize`](GUIControl#guicontrolsetsize) | |
| `SetGUIPosition` | [`GUI.SetPosition`](GUI#guisetposition) | |
| `SetGUISize` | [`GUI.SetSize`](GUI#guisetsize) | |
| `SetGUITransparency` | [`GUI.Transparency`](GUI#guitransparency) | |
| `SetGUIZOrder` | [`GUI.ZOrder `](GUI#guizorder) | |
| `SetInvDimensions` | [`InvWindow.ItemHeight`](InvWindow#invwindowitemheight) | |
| `SetInvItemName` | [`InventoryItem.Name`](InventoryItem#inventoryitemname) | |
| `SetInvItemPic` | [`InventoryItem.Graphic`](InventoryItem#inventoryitemgraphic) | |
| `SetLabelColor` | [`Label.TextColor`](Label#labeltextcolor) | |
| `SetLabelFont` | [`Label.Font`](Label#labelfont) | |
| `SetLabelText` | [`Label.Text`](Label#labeltext) | |
| `SetMouseBounds` | [`Mouse.SetBounds`](Mouse#mousesetbounds) | |
| `SetMouseCursor` | [`Mouse.UseModeGraphic`](Mouse#mouseusemodegraphic) | |
| `SetMousePosition` | [`Mouse.SetPosition`](Mouse#mousesetposition) | |
| `SetMusicMasterVolume` | [`System.Volume`](System#systemvolume) | |
| `SetMusicRepeat` | [`AudioClip.Play`](AudioClip#audioclipplay) | |
| `SetMusicVolume` | [`AudioChannel.Volume`](AudioChannel#audiochannelvolume) | |
| `SetNextCursorMode` | [`Mouse.SelectNextMode`](Mouse#mouseselectnextmode) | |
| `SetNormalFont` | [`Game.NormalFont`](Game#gamenormalfont) | |
| `SetObjectBaseline` | [`Object.Baseline`](Object#objectbaseline) | |
| `SetObjectClickable` | [`Object.Clickable`](Object#objectclickable) | |
| `SetObjectFrame` | [`Object.SetView`](Object#objectsetview) | |
| `SetObjectGraphic` | [`Object.Graphic`](Object#objectgraphic) | |
| [`SetObjectIgnoreWalkbehinds`](Object#objectignorewalkbehinds) | design your rooms without it and rely on [`Object.Baseline`](Object#objectbaseline) instead | 3.5.0 |
| `SetObjectPosition` | [`Object.SetPosition`](Object#objectsetposition) | |
| `SetObjectTint` | [`Object.Tint`](Object#objecttint) | |
| `SetObjectTransparency` | [`Object.Transparency`](Object#objecttransparency) | |
| `SetObjectView` | [`Object.SetView`](Object#objectsetview) | |
| `SetPlayerCharacter` | [`Character.SetAsPlayer`](Character#charactersetasplayer) | |
| `SetRegionTint` | [`Region.Tint`](Region#regiontint) | |
| `SetSkipSpeech` | [`Speech.SkipStyle`](Speech#speechskipstyle) | |
| `SetSliderValue` | [`Slider.Value`](Slider#slidervalue) | |
| `SetSoundVolume` | [`Game.SetAudioTypeVolume`](Game#gamesetaudiotypevolume) | |
| `SetSpeechFont` | [`Game.SpeechFont`](Game#gamespeechfont) | |
| `SetSpeechStyle` | [`Speech.Style`](Speech#speechstyle) | |
| `SetTalkingColor` | [`Character.SpeechColor`](Character#characterspeechcolor) | |
| `SetTextBoxFont` | [`TextBox.Font`](TextBox#textboxfont) | |
| `SetTextBoxText` | [`TextBox.Text`](TextBox#textboxtext) | |
| `SetTextOverlay` | [`Overlay.SetText`](Overlay#overlaysettext) | |
| [`SetViewport`](Globalfunctions_Room#setviewport) | [`Game.Camera.SetAt`](Camera#camerasetat) | 3.5.0 |
| `SetVoiceMode` | [`Speech.VoiceMode`](Speech#speechvoicemode) | |
| `ShowMouseCursor` | [`Mouse.Visible`](Mouse#mousevisible) | |
| `StopAmbientSound` | [`AudioChannel.Stop`](AudioChannel#audiochannelstop) | |
| `StopChannel` | [`AudioChannel.Stop`](AudioChannel#audiochannelstop) | |
| `StopMoving` | [`Character.StopMoving`](Character#characterstopmoving) | |
| `StopMusic` | [`Game.StopAudio`](Game#gamestopaudio) | |
| `StopObjectMoving` | [`Object.StopMoving`](Object#objectstopmoving) | |
| `StrCaseComp` | [`String.CompareTo`](String#stringcompareto) | |
| `StrCat` | [`String.Append`](String#stringappend) | |
| `StrComp` | [`String.CompareTo`](String#stringcompareto) | |
| `StrContains` | [`String.IndexOf`](String#stringindexof) | |
| `StrCopy` | [`String.Copy`](String#stringcopy) | |
| `StrFormat` | [`String.Format`](String#stringformat) | |
| `StrGetCharAt` | [`String.Chars[]`](String#stringchars) | |
| `String.Contains` | [`String.IndexOf`](String#stringindexof) | |
| `StringToInt` | [`String.AsInt`](String#stringasint) | |
| `StrLen` | [`String.Length`](String#stringlength) | |
| `StrSetCharAt` | [`String.ReplaceCharAt`](String#stringreplacecharat) | |
| `StrToLowerCase` | [`String.LowerCase`](String#stringlowercase) | |
| `StrToUpperCase` | [`String.UpperCase`](String#stringuppercase) | |
| `system.color_depth` | [`System.ColorDepth`](System#systemcolordepth) | |
| `system.os` | [`System.OperatingSystem`](System#systemoperatingsystem) | |
| [`System.ScreenHeight`](System#systemscreenheight) | [`Screen.Height`](Screen#screenheight) | 3.5.0 |
| [`System.ScreenWidth`](System#systemscreenwidth) | [`Screen.Width`](Screen#screenwidth) | 3.5.0 |
| `system.version` | [`System.Version`](System#systemversion) | |
| [`System.ViewportHeight`](System#systemviewportheight) | [`Screen.Height`](Screen#screenheight) | 3.5.0 |
| [`System.ViewportWidth`](System#systemviewportwidth) | [`Screen.Width`](Screen#screenwidth) | 3.5.0 |
| `system.vsync` | [`System.Vsync`](System#systemvsync) | |
| `system.windowed` | [`System.Windowed`](System#systemwindowed) | |
| `TextBox.GetText` | [`TextBox.Text`](TextBox#textboxtext) | |
| `TextBox.SetText` | [`TextBox.Text`](TextBox#textboxtext) | |
| `ViewFrame.Sound` | [`ViewFrame.LinkedAudio`](ViewFrame#viewframelinkedaudio) | |
