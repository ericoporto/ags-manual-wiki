## MIDI playback

MIDI files are different from other sound formats, because they do not have actual sounds encoded, but describe the track using instruments and notes. In order to play a MIDI track the engine must have a full knowledge of how to interpret these instruments, how to convert the instrument's note into the real sound. This knowledge is got from what is known as "sound banks", or "patch files".

_Prior to **AGS 3.6.0**_ the Windows version of the engine would use the system interface to play MIDI file, that's why the games did not require to contain any sound banks: they would use the ones installed in the system. Other systems (Linux, and so forth), however, required user to install such banks by hand before they are able to hear the MIDI music in games.

_Since **AGS 3.6.0**_, for technical reasons, the engine no longer supports using the Windows interface, so even on Windows you require to have the MIDI banks installed if you want to hear MIDI music from AGS games. Please continue the read to know how it can be done.

For playing MIDI files AGS engine uses a software synthesizer known as TiMidity++ (or simply "Timidity"). Timidity transcribes MIDI using Gravis Ultrasound (GUS) patch files. The synthesizer itself is built into the engine so you don't have to worry about that, but the patch files are not. To perform an actual MIDI engine needs a Timidity configuration and patch files present where it can find them.

### Where to get patch files

There are numerous Timidity patch files that may be found on the internet, each has its own differences, and in theory one can even make their custom ones.

Following is an example of a good collection based on the id Software's Doom 1 and 2 games (tested with few older AGS games):<br>
http://www.gamers.org/pub/idgames/music/dgguspat.zip

### How to install Timidity

The primary file is called "timidity.cfg" and it should be present either along with the game (or engine's) executable, or in the following system path:

**On Windows:**
* C:\Timidity\Timidity.cfg

**On Linux and MacOS**
* etc/timidity.cfg

The patch files may be located in the same directory by default. If you prefer to place them elsewhere for organizational purposes, then you have to add a "dir" command inside timidity.cfg, right at the top of the file:

    dir THE_PATH_TO_PATCH_FILES

for example:

    dir C:\timidity\patches
    dir etc/tim_patches
