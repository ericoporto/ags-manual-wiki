## Audio in script

Quite often there is misunderstanding of how audio system works in AGS and how can you control it in script. Unfortunately it has certain design flaws and limitations to what you can do. Here we'll cover most important bits.

Let's begin with **audio channel**. Audio channels are essentially *slots* in which the sound clip is put for playback. Channel may play one *instance* of audio clip at a time.

**Audio clips** are playable resources. When you command them to play (for example, [AudioClip.Play](AudioClip#audioclipplay)) their _instance_, essentially a *copy* is inserted into one of the audio channels and is played. You may then command to play same audio clip again and another _instance_ (copy) will be inserted into second channel and played separately.

Now, it is very important to understand that audio channels are static _permanent_ objects, they are created by the engine at startup and are kept throughout the game. There's a fixed number of them, this number is 8. This cannot be changed. You cannot create new channels or remove existing ones neither in the editor nor in script. All of these channels are present and available for access at all times regardless of whether anything is played on them or not. This is done using [System.AudioChannels](System#System#systemaudiochannels) array. The size of this array is told by [System.AudioChannelCount](System#systemaudiochannelcount).

When AudioClip.Play() is called it searches for an available channel, among reserved channels for the given audio type or all of the channels, and checking clip priorities if no channel is free. When it successfully inserted a clip instance into the channel it returns AudioChannel* pointer. That pointer always points to one of the channels from System.AudioChannels array, and *does not* create a new channel (this is an often erronous assumption by users).

When audio ends playing whether on its own or by calling AudioChannel.Stop() or AudioClip.Stop(), the clip instance is removed from the channel but the channel itself remains, and *not* get deleted.

The consequence of all the above is that if you keep AudioChannel* pointer returned by AudioClip.Play, for example store it in a global variable, that pointer will always be valid, but also because same channel may end up hosting a new clip eventually, you may use same pointer to adjust new clip's playback properties.

This effect may be demonstrated by following example. Make sure that your sound type has "MaxChannels" set to "1", then add following script to first room's "after fade-in event":
<pre>
function room_AfterFadeIn() {
    AudioChannel* chan = aSound1.Play();
    aSound2.Play();
    chan.Volume = 50;
}
</pre>
Notice that `chan` is assigned to `aSound1.Play()`, and not to `aSound2.Play()`. However, because there's only 1 channel reserved for sounds, aSound2 will replace aSound1. And because `chan` pointer is already pointing to that only reserved channel, setting volume will actually change aSound2's volume, as it is the one playing on the channel now.

This effect may be either wanted or unwanted and leading to bugs depending on how you script your game, so keep it in mind.