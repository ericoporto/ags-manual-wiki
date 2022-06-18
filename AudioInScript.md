## Audio in script

Quite often there is misunderstanding of how the audio system works in AGS and how can you control it in script. Unfortunately it has certain design flaws and limitations to what you can do. Here we'll cover the most important bits.

Let's begin with **audio channel**. Audio channels are essentially *slots* in which the sound clip is put for playback. A channel may play one *instance* of one audio clip at a time.

**Audio clips** are playable resources. When you command them to play (for example, [`AudioClip.Play`](AudioClip#audioclipplay)) their _instance_, essentially a *copy* is inserted into one of the audio channels and is played. You may then use a command to play the same audio clip again and another _instance_ (copy) will be inserted into the second channel and will be played separately.

Now, it is very important to understand that audio channels are static _permanent_ objects, they are created by the engine at startup and are kept throughout the game. There's a fixed number of 16 audio channels (8 before AGS 3.6.0). This cannot be changed. You cannot create new channels or remove existing ones neither in the editor nor in script. All of these channels are present and available for access at all times regardless of whether anything is played on them or not. This is done using the [`System.AudioChannels`](System#systemaudiochannels) array. You can find out the size of this array with [`System.AudioChannelCount`](System#systemaudiochannelcount).

When AudioClip.Play() is called it searches for an available channel, among reserved channels for the given audio type or among all of the channels, and checks audio clip priorities if no channel is free. When it successfully inserted a clip instance into a channel it returns an AudioChannel* pointer. That pointer always points to one of the channels from the System.AudioChannels array, and *does not* create a new channel (this is an often erroneous assumption by users).

When audio ends playing whether on its own or by calling AudioChannel.Stop() or AudioClip.Stop(), the clip instance is removed from the channel but the channel itself remains and does *not* get deleted.

The consequence of all the above is that if you keep the AudioChannel* pointer returned by AudioClip.Play, for example store it in a global variable, that pointer will always be valid, but because the same channel can be used to play a new and different clip, you can use the same stored pointer to adjust the new clip's playback properties.

This effect can be demonstrated by the following example. Make sure that your sound type has "MaxChannels" set to "1", then add the following script to the first room's "after fade-in event":

```
function room_AfterFadeIn() {
    AudioChannel* chan = aSound1.Play();
    aSound2.Play();
    chan.Volume = 50;
}
```

Notice that `chan` is assigned to `aSound1.Play()`, and not to `aSound2.Play()`. But because we set "MaxChannels" of the sound type to "1" there is only 1 channel reserved for sounds, so aSound2 will replace aSound1. And because the `chan` pointer is already pointing to the only reserved channel, setting the volume will actually change aSound2's volume, as it is the audio clip playing on the channel now.

This effect may either be wanted or unwanted and can lead to bugs depending on how you script your game, so keep this in mind.


*See also:* [Music and Sound](MusicAndSound), [Audio Channel](AudioChannel), [Audio Clip](AudioClip)
