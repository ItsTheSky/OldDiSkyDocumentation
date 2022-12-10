# 📺 Presence & Status

As a user, your bot will be able to have a custom **online status** and **presence.**

### Presence (Activity)

The presence will define what your bot is actually doing. It can be one of the following actions:

* Listening
* Watching
* Playing
* Competing
* Streaming

When defining the presence, you'll have to provide the **text shown**, for example, what game your bot is playing or what music is it listening to.

{% hint style="warning" %}
For the **streaming** presence only, you'll have to provide a **valid YouTube or Twitch** stream URL to show it!
{% endhint %}

Here's an example of each presence, and a way to change the bots:

```applescript
set the presence of the bot named "bot-name" to listening "awesome music!"

set the presence of the bot named "bot-name" to playing "awesome games!"

set the presence of the bot named "bot-name" to competing "Arena World Champions"

set the presence of the bot named "bot-name" to watching "YouTube"

# The URL must be from YouTube or Twitch!
set the presence of the bot named "bot-name" to streaming "things" with url "stream.url"
```

Some examples of the presences:

Listening:

![Listening Presence](https://cdn.upload.systems/uploads/vRx1XhH9.png)

Playing:

![Playing Presence](https://cdn.upload.systems/uploads/LOYVm9gs.png)

Competing:

![Competing Presence](https://cdn.upload.systems/uploads/4NmNTzht.png)

Watching:

![Watching Presence](https://cdn.upload.systems/uploads/Nrmf2LEj.png)

Streaming:

![Streaming Presence](https://cdn.upload.systems/uploads/4WMVTHDd.png)

### Online Status

The online status will define the little circle at the bottom-right corner of your bot's avatar.

Here's the available online status your bot can have:

* Online (`online`, shown as :green\_circle:)
* Idle (`idle`, shown as :yellow\_circle:)
* Do not disturb (`do not disturb`, shown as :red\_circle:)
* Offline (`offline`, shown as :white\_circle:, **the bot won't be shown as online and will be hidden!**)

To change the bot's online status, simply use this syntax:

```
set the online status of bot "bot-name" to <status id>
```

{% hint style="warning" %}
The `status id` is represented by the text formatted as code above!
{% endhint %}
