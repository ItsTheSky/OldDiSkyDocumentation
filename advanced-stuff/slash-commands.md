# 📯 Slash Commands

**Slash Commands** are the most enhanced, optimized, and easy way to implement user interactions. Using Discord's API, you'll be able to make commands with arguments where the user will be invited to choose between different values, or maybe their own.

First of all, you must know that there is three type of "_containers_" for the slash commands:

* Slash Commands
* Slash Commands Groups (can be added to a slash command, and can contain **subcommands**)
* Subcommands (share the same properties as slash commands, although they cannot have groups)

Let's take a concrete example, and imagine I'm executing these commands:

| What does it have?                                                                                                                                                                                                    | Representation                |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| <ul><li>Root command is <code>docs</code></li><li>The <strong>root</strong> have one <code>string</code> argument called <code>name</code></li></ul>                                                                  | `/docs name:ItsTheSky`        |
| <ul><li>Root command is <code>snippets</code></li><li>Have one sub-command named <code>search</code></li><li>The <strong>subcommand</strong> has one <code>string</code> argument called <code>query</code></li></ul> | `/snippets search query:user` |

### What does a command have?

{% hint style="success" %}
We'll use the term **command** here to define both **slash** & **sub** commands!
{% endhint %}

* **Name** (used to execute the command, aka `/<name>`. Only alphanumeric chars)
* **Description** (used to recognize the command. Is shown to the client once he selected that command)
* Up to **25 options** (can be of the following type: `STRING`, `INTEGER`, `BOOLEAN`, `USER`, `CHANNEL`, `ROLE`, `MENTIONABLE`, `NUMBER`, `ATTACHMENT`)
* Possible **subcommands** or **groups**

### Getting Started

Let's create a sample command with DiSky now. We'll make a slash command named `level` with one option of `user` type, here to get the level of a user. If no user is defined, we'll simply manage it through the `event-user`.&#x20;

{% hint style="warning" %}
Options can be required or not. If they are not, then you should always think of a fallback value, here, the user who executed the command for example!
{% endhint %}

```applescript
# We highly recommend using the 'on ready' section of the bot's scope
# for registering commands!
define bot XXX:
    ...
    on ready:
    
        # We create a new slash command with a name and a description
        set {_level} to new slash command named "level" with description "Check your or other's current level"
        
        # We add a new user option to the command
        add new user option named "target" with description "The optional target user" to options of {_level}
        
        # Lastly, we update the command on Discord through the bot
        update {_level} globally in event-bot
```

If you restart your server, take a look at the slash command menu by typing a `/`, you should notice that your created command is here and can be executed. However, for now, we never handle the interaction and Discord will warn you that it failed.

```applescript
on slash command:
    # we get the command's name, representing the command's ID
    set {_name} to event-string

    # let's be sure it's the right command
    if {_name} is "level":
        
        # we get the value option. remember, it can be null since the option is optional!
        set {_target} to argument "target" as user
        if {_target} is not set:
            set {_target} to event-user
        
        # i won't make a whole level system here, it's just for the command example
        # we lastly reply with something, that will also acknowledge (= approve) the command.
        reply with "%mention tag of {_target}% is level X"
```
