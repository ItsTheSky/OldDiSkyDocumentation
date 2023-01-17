# 🎵 LavaPlayer

LavaPlayer is a DiSky module that allows developers to implement music loading & playing with their bots.

## Installation

{% hint style="warning" %}
LavaPlayer is a **paid** module, that you can have on my [**Patreon**](https://patreon.com/itsthesky)****
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
set {_track} to track from file "plugins/music/mytrack.mp3"
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

