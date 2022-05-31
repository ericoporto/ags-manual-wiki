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

**NOTE:** WAV, OGG and MP3 format files can be used for speech.

**NOTE:** Speech file numbers are restricted to the positive range of 1 to 2147483647 (2 billion). This is a technical limitation based on how these are handled inside the engine, but we do not think it will ever become a problem to the user.

Speech is compiled into a file called SPEECH.VOX and is separate from
the rest of your game data so that you can offer it as an optional extra
download to the player. The game will function correctly if the file is
not present.

*SeeAlso:* [`Speech.VoiceMode`](Speech#speechvoicemode)