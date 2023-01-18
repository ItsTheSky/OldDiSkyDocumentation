# 🎵 LavaPlayer

LavaPlayer is a DiSky module that allows developers to implement music loading & playing with their bots.

## Installation

{% hint style="warning" %}
LavaPlayer is a **premium** module, that you can have on my [**Patreon**](https://patreon.com/itsthesky)****
{% endhint %}

* Download the latest version from the [**Patreon**](https://patreon.com/itsthesky) page.
* Put the downloaded file in `/plugins/DiSky/modules/`
* Restarts your server

And here we go! You can now use the syntax of LavaPlayer in your scripts!

## Basic Operation

Before doing anything, it's better to understand how LavaPlayer manages tracks and audio players:

### Tracks

An **audio track** can be played by a bot. It holds some info such as its title, author, identifier (YouTube/SoundCloud ID, or local file path).

You can load tracks through 3 different ways:

#### Via local files

LP supports some file format such as MP3, WAV or FLAC. For a full list, check [**here**](https://github.com/sedmelluq/lavaplayer#supported-formats).

```applescript
load track from file "plugins/music/mytrack.mp3" and store it in {_track}
```

`{_track}` now holds your local track!

#### Via external (Youtube/Soundcloud) specific URL

This is only for exact video or playlist URL, that must starts with `https://youtube` (or `https://soundcloud` if you want to load a sound cloud audio).

LavaPlayer uses **section** to chunk your code, and execute the corrects one once the section is fired:

```applescript
load items from url "https://www.youtube.com/watch?v=nQnZlD4dgPE":
    
    # Used if it loads a single track.
    on single load:
        set {_track} to loaded track
    
    # Used if it loads a whole playlist.
    # Besides the playerlist's tracks, it also holds the playlist's name.
    on playlist load:
        set {_track} to first element of tracks of loaded playlist
    
    # If any failure happened, like no connection, 404 errors, etc...
    on load failure:
        reply with "An exception occured: %the exception%"
```

{% hint style="info" %}
You can use the **variables** from the sub-section **outsides**! For example here, you can continue your code outside the sections with `{_track}`
{% endhint %}

#### Via Youtube search

This will search for the provided input and loads tracks accordindly. Actually, `on single load` should never be called as it must found more than one video here:

```applescript
search items from input "KDA more":
    
    # Should not be called there.
    on single load:
        reply with "Oh no, something went wrong ..."
    
    # The playlist will contains the loaded tracks for the search.
    # Here again we'll just keep the first loaded track.
    on playlist load:
        set {_track} to first element of tracks of loaded playlist
    
    # If any failure happened, like no connection, 404 errors, etc...
    on load failure:
        reply with "An exception occured: %the exception%"
    
    # If no video matched the input at all.
    on no matches:
        reply with "Nothing found for your query!"
```

### Guild Players

LavaPlayer makes your life better: it comes with a built-in guild player system.

Each guild **and bot** will have a specific Guild player (if you have 2 bot in 1 guild, you'll have 2 players for each bot). It holds informations such as the playing track, the volume, the queue, and much more.

However, a player is not created once the bot loads; only when you play a track, the player will be got (if it exists) or created. Therefore, you **cannot change the volume** (for example) of a player before playing any track!

#### Queue

```applescript
set {_queue::*} to queue of event-guild
```

If you want to specify a bot, simply append `... with bot "name"` at the end of the syntax.

#### Volume

```applescript
set {_current} to playing track of event-guild
```

The volume **must** be between 0 and 1000 (both inclusive). Any negative or bigger than 1000 values will be rounded to the closer valid value.

#### Manage Player

| Action                                                                                  | Example                                        |
| --------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Make the player play the specified track. It won't be removed from the queue by itself. | `play {_track} in event-guild`                 |
| Skip the current track, by returning and removing the next track from the queue.        | `skip in event-guild and store it in {_track}` |
| Pause the player, without changing the queue nor the playing track.                     | `pause in event-guild`                         |
| Resume the paused track, without changing the queue nor the playing track               | `resume in event-guild`                        |

## Full example

Okay. We saw the basics things until now, here's a small commented example of LavaPlayer2:

```applescript
discord command play <string>:
    prefixes: !
    trigger:

        set {_channel} to voice channel of event-member
        # Check if the user is in a voice channel
        if {_channel} is not set:
            reply with "You are not in a voice channel!"
            stop
        
        set {_willHaveToConnect} to true
        
        set {_botChannel} to voice channel of (self member of event-bot in event-guild)
        if {_botChannel} is set:
            # Check if the bot is in the same channel than the member
            if {_botChannel} is not {_channel}:
                reply with "I am already connected to a different voice channel!"
                stop
            else:
                set {_willHaveToConnect} to false
        
        # Let's search for the provided input.
        search items with input arg-1:
            on playlist load:
                set {_track} to first element of tracks of loaded playlist
            
            on no matches:
                reply with "No matches found!"
            
            on load error:
                reply with "An error occurred while loading the track: %the exception%"
        
        {_track} is set
        
        # We'll check if the bot is currently playing or not.
        # (either the queue is not empty or the bot is playing a track)
        set {_isPlaying} to false
        if size of queue of event-guild is bigger than 0:
            set {_isPlaying} to true
        if playing track of event-guild is set:
            set {_isPlaying} to true
        
        # If the bot is not playing, no need to queue the track
        # (as we'll plays it right away)
        if {_isPlaying} is false:
            force play {_track} in event-guild
            reply with "**Now playing:** `%{_track}%`"
        # If not, we simply queue it and inform the user about this.
        else:
            add {_track} to queue of event-guild
            
            reply with "**Track queued:** `%{_track}%` (position: `%size of queue of event-guild%`)"
        
        # We connect the bot if it's not already connected
        if {_willHaveToConnect} is true:
            connect event-bot to {_channel}

discord command skip:
    prefixes: !
    trigger:
        if size of queue of event-guild is 0:
            reply with "There is nothing after the current track!"
            stop
        # Don't forget 'skip' only skip the track in the queue (removes & returns it)
        skip track in event-guild and store it in {_track}
        # We must play the new one to actually skip it.
        force play {_track} in event-guild

        reply with "**Skipped track! Now playing:** `%{_track}%`"

discord command pause:
    prefixes: !
    trigger:
        pause track in event-guild
        reply with "Paused track!"

discord command resume:
    prefixes: !
    trigger:
        resume track in event-guild
        reply with "Resumed track!"

discord command queue:
    prefixes: !
    trigger:
        set {_queue::*} to queue of event-guild
        if size of {_queue::*} is 0:
            reply with "There is nothing in the queue!"
            stop
        set {_l::*} to "`>` **Audio Queue of __%event-guild%__:** (%size of {_queue::*}% items)"
        add "" to {_l::*}
        add "`0` - Currently playing: `%playing track of event-guild%`" to {_l::*}
        add "" to {_l::*}
        loop {_queue::*}:
            add "`%loop-index%` - `%loop-value%`" to {_l::*}
        reply with join {_l::*} with nl
```
