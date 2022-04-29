## Multimedia functions

### `CDAudio`

    CDAudio (eCDAudioFunction, int param)

This function allows you to play and control an audio CD in your game.
Different tasks are performed, depending on the value of the
AudioFunction parameter. If there is no CD-ROM drive on the system, the
function does nothing.

The PARAM parameter is used by some of the functions for various
reasons; if it is not needed for the particular function you are
calling, pass zero instead.

The tasks performed are as follows depending on the COMMAND parameter:

    eCDIsDriverPresent - checks if there is a CD-ROM driver available on
       the system. Returns 1 if there is, and 0 if there is not.
    eCDGetPlayingStatus - checks whether the CD drive is currently playing
       an audio track. Returns 1 if it is, and 0 if it is not.
    eCDPlayTrack - starts playback from track PARAM on the CD. If the track
       does not exist, or if it is a data track, nothing happens.
    eCDPausePlayback - pauses the currently playing audio track.
    eCDResumePlayback - continues from where the track was paused.
    eCDGetNumTracks - returns the number of tracks on the CD
       currently in the drive. If the drive is empty, returns 0.
    eCDEject - ejects the drive tray if the drive has the ability. This is
       a feature you'll play with to start off because it's neat, and then
       realize that it has no real use in your game.
       Your script does not continue until the drive is fully ejected.
    eCDCloseTray - the reverse of Eject. This will pull the drive tray back
       in again. Your script does not continue until the drive has been
       fully closed.
    eCDGetCDDriveCount - returns the number of CD drives in the
       system, normally 1.
    eCDSelectActiveCDDrive - changes the current CD drive to PARAM,
       where PARAM ranges from 1 to (number of CD drives). All the other
       CD Audio functions operate on the current CD drive.

NOTE: These CD Audio functions are slow compared to all the other script
functions. This will not be noticeable if you call them from most
scripts, but using CDAudio in a repeatedly_execute script will
noticeably slow down the game.

**Cross-Platform Support**

Windows: **Yes, but supports 1 CD-ROM drive only**<br>
Linux: **Yes, but supports 1 CD-ROM drive only**<br>
MacOS: **No**

Example:

    CDAudio(eCDPlayTrack, 3);

will play track 3 of the CD that's in the CD ROM drive.

---

### `IsSpeechVoxAvailable`

    IsSpeechVoxAvailable()

Returns whether the SPEECH.VOX file is being used by the game. This
could be useful if you have an optional speech download pack, and you
want to know whether the player has it or not.

Returns 1 if the speech files are available, 0 if not.

Example:

    if (IsSpeechVoxAvailable()==0)
        Display ("You don't have the voice pack");

will display a message if the voice pack is not available.

**NOTE:** This function used to be called IsVoxAvailable, but has now
been renamed to avoid confusion.

*See also:* [`AudioClip.IsAvailable`](AudioClip#audioclipisavailable)

---

### `PlayFlic`

    PlayFlic (int flic_number, int options)

Plays a FLI or FLC animation. The game checks for FLICx.FLC and
FLICx.FLI (where X is FLIC_NUMBER) and if it finds one, plays it.

OPTIONS has these meanings:

    0  player can't skip animation
    1  player can press ESC to skip animation
    2  player can press any key or click mouse to skip animation
    +10 (i.e.10,11,12) do not stretch to full-screen, just play at flc size
    +100 do not clear the screen before starting playback

The game is paused while the animation plays.

Example:

    PlayFlic(2, 1);

will play flic2 and the player will be able to skip the flic by pressing
the ESC key.

*See also:* [`PlayVideo`](Multimedia#playvideo)

---

### `PlaySilentMIDI`

    PlaySilentMIDI (int music_number)

This command is obsolete.

Use the AudioClip.Play command and set its Volume property to 0 to
simulate this effect.

*See also:* [`AudioClip.Play`](AudioClip#audioclipplay),
[`AudioChannel.Volume`](AudioChannel#audiochannelvolume)

---

### `PlayVideo`

    PlayVideo (string filename, VideoSkipStyle, int flags)

Plays an AVI, MPG or OGG Theora file, or any other file type supported
by Media Player. The game is paused while the video plays.

*VideoSkipStyle* defines how the player can skip the video:

    eVideoSkipNotAllowed     player can't skip video
    eVideoSkipEscKey         player can press ESC to skip video
    eVideoSkipAnyKey         player can press any key to skip video
    eVideoSkipAnyKeyOrMouse  player can press any key or click mouse to skip

FLAGS can be one of the following:

    0: the video will be played at original size, with AVI audio
    1: the video will be stretched to full screen, with appropriate
       black borders to maintain its aspect ratio and AVI audio.
    10: original size, with game audio continuing (AVI audio muted)
    11: stretched to full screen, with game audio continuing (AVI audio muted)

There are two distinct type of videos that the PlayVideo function can
play.

The first is OGG Theora, which is a recently introduced video file
format. AGS has built-in support for playing these videos, so everyone
who plays your game will be able to see the video. OGG Theora videos are
also built into the game EXE file when you compile the game (just make
sure the file has a .OGV extension and is placed in your main game
folder). A good converter for theora is [ffmpeg2theora](https://v2v.cc/~j/ffmpeg2theora/).

**IMPORTANT:** Because of an old mistake in AGS, OGG Theora videos may be positioned on screen with a slight negative offset, cutting few rows or columns of pixels. Until this is fixed, as a workaround, make sure that your video's frame sizes are multipliers of 16 and actual image placed aligned to the center. For example, if you want 320x200 video then increase canvas to 320x208 and place image at offset (0, 4).

The second type of files that AGS can play is anything supported by
Windows Media Player. This includes AVI, MPG and more. However, in order
for these to work on the player's system, they will need to have the
correct codecs installed. For example, if you create your video with the
XVid codec, the player will need to have XVid installed to be able to
view it. These types of video cannot be included into the game EXE, so
you will have to place them separately in the Compiled folder for them
to work.

**NOTE:** In 256-color games, PlayVideo is not supported. Please use a
FLC/FLI video with the [`PlayFlic`](Multimedia#playflic) command instead.

Example:

    PlayVideo("Intro.ogv", eVideoSkipEscKey, 1);

will play the video Intro.ogv, allowing the player to skip with ESC if
they've seen it before.

**Cross-Platform Support**

OGG Theora: supported everywhere.
AVI / MPG: Windows only.

*Compatibility:* OGG Theora supported by **AGS 3.1.1** and later
versions.

*See also:* [`PlayFlic`](Multimedia#playflic)

---

### `SetSpeechVolume`

    SetSpeechVolume (int volume)

Sets the volume for in-game speech. VOLUME ranges from 0-255, where 255
is the loudest. The default speech volume is 255 so this function can
only be used to reduce the volume.

Example:

    SetSpeechVolume(200);

will set the speech volume to 200.

*See also:* [`Game.SetAudioTypeVolume`](Game#gamesetaudiotypevolume), 
[`Game.SetAudioTypeSpeechVolumeDrop`](Game#gamesetaudiotypespeechvolumedrop), 
[`Game.PlayVoiceClip`](Game#gameplayvoiceclip)
