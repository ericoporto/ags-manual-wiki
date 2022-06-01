## Voice speech

With AGS you can link a line of dialog to a speech file, to enable
"talkie"- style games. Suppose you have a dialog script with the
following:

    ego: "Hi! How are you?"
    michael: "I'm fine."

Normally this would display the words in the speech text above the
characters heads. However, you can add the special character '&' to
symbolize that a voice file should also be played.

The file name has format XXXXY.EXT, where XXXX is made of up to **first
four letters** of the character's script name (except the leading 'c'),
the Y is the speech file number (with no leading or trailing zeroes or
padding of any kind), and EXT is the file extension.

For example, if you have dialog script:

    ego: &10 "Hi! How are you?"
    michael: &7 "I'm fine."

or common script using Say script function:

    cEgo.Say("&10 Hi! How are you?");
    cMichael.Say("&7 I'm fine.");

Both of those examples would play EGO10.WAV with the first line, and
MICH7.WAV with the second. When a line of text has a voice linked to it,
the text on the screen will not be removed until the voice file has
finished playing. If the player interrupts it by clicking the mouse or
pressing a key, the text and voice will be stopped. Voice files must be
placed in the "Speech" sub-directory of the game folder.

**NOTE:** Speech file numbers are restricted to the positive range of 1 to 2147483647 (2 billion). This is a technical limitation based on how these are handled inside the engine, but we do not think it will ever become a problem to the user.

### Voice packs

Any sound format supported by AGS can be used for speech as well.

AGS uses separate voice packs to store the speech files. The default voice pack is compiled by placing files in the "Speech" sub-directory of the game folder, and is named "speech.vox".

Since version 3.6.0 AGS also supports multiple alternate voice packs. These are compiled from *subdirectories* nested inside the "Speech", and are named "sp_DIRNAME.vox", where DIRNAME is a name of that subdirectory.
The speech files in these alternate directories must have same names as files in the "Speech" itself. These extra packs may be used to provide voice-over for different languages.

For example, if you have this folder structure in your game project:

* Speech
* * Francais
* * MyLang

then the editor will create following voxes:
* speech.vox (with files only from the root "Speech" folder);
* sp_francais.vox (with files from "Speech/Francais");
* sp_mylang.vox (with files from "Speech/MyLang");

**NOTE:** only top-level files are included into the voice pack, any further subfolders are ignored.

Since AGS 3.6.0 engine supports switching to a different speech vox anytime. To do so, there's a new script function [Game.ChangeSpeechVox](Game#gamechangespeechvox).

Note that the voice packs are considered optional, and your game will function correctly even without them, in which case it will display speech text but play no voice. This allows to offer them as an optional download for your players.
If particular speech file is missing in the pack, that also should not cause game errors.

*SeeAlso:* [`Game.ChangeSpeechVox`](Game#gamechangespeechvox),
[`Speech.VoiceMode`](Speech#speechvoicemode)