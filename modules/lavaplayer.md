# ⚠ LavaPlayer 1 (Old)

{% hint style="danger" %}
LavaPlayer 1 is not supported anymore. Use **LavaPlayer2** instead.
{% endhint %}

{% hint style="info" %}
**Download:** [**https://github.com/DiSkyOrg/LavaPlayer/releases**](https://github.com/DiSkyOrg/LavaPlayer/releases)\*\*\*\*
{% endhint %}

LavaPlayer allows you to play audio from YouTube and SoundCloud in voice channels.

## Connecting to a voice channel

Before playing any audio, you should connect the bot to a voice channel. This can be done with the connect bot effect.

```applescript
connect bot named "fancyBOT" to voice channel of event-member
```

## Fetching audio

Before playing audio you need to retrieve said audio and store it in a variable.

```applescript
search in "youtube" parsed as audio source for "never gonna give you up" and store the tracks in {_result::*}
```

{% hint style="info" %}
The `audio source` can be either "youtube" or "soundcloud". The `query` can be either text or a link, these links can also be playlists.
{% endhint %}

\##Playing audio

Finally all you need to do is play the audio stored in the variable!

```applescript
play {_result::*} in event-guild
```

## Looping audio

You can make your bot look the current audio in a specific guild using the following effect.

```applescript
set repeating state of event-guild to true
```
