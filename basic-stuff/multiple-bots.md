# 🤖 Multiple Bots

DiSky allows you to run multiple bot instances on a single server; Some syntaxes will have to change, and that's what we will see here!

### Define another bot

Nothing could be easier! Copy the definition code of your first bot, then change the token and its name. Restart your server and you're done! Your two bots are now connected!

### Conflicts

Let's take a simple example; Your two bots are on the same discord server, and a user sends a message.&#x20;

**Question:** which of the two bots will be used in the `on message receive` event?

Well, both! The event will be executed twice, with each of the bots instances. If you have 4 bots, for example, it will be executed 4 times.

To solve this problem, you have two solutions:

* Check the right bot at the beginning of the event, in case each bot on your server has a particular role.
* Use slightly different syntaxes to tell which bot we will do which actions on Discord.

The first option is probably the simplest and most common. Seriously, who would want two bots exactly the same on the same server? Checking the bot is as easy as pie, here is an example using our event from earlier:

```applescript
on message receive:
    event-bot is bot "name"
    
    # </>
```

Simple, isn't it? The following code will be executed only if the bot is our bot named "`name`" is used!

For the second option, DiSky offers a special effect, called the `specific bot effect`.

You just have to specify the effect **coming from DiSky** that you want to use with the bot and the name of the bot in question. Here is an example with the `reply with` effect:

```
on message receive:
    execute reply with "Hello, world!" with bot "name"
```

The effect will be executed with the bot named `name`, no matter the situation!
