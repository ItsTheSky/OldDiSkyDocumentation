# 📐 Discord Commands

Discord Commands are the old way to provide user-to-bot interaction. They use the message's content, and DiSky parses it as you request when you're defining the command.

Even if they are old and Discord does not recommend anymore to use them, DiSky will keep the support for them, and this page will describe how to create simple Discord Command.

### Creating the command

Any discord command is defined via a [Scope](../getting-started/bot-loading.md#scopes):&#x20;

```applescript
# This is outside any event!
discord command <name>:
    prefixes: <prefixes>
    trigger:
        <code>
```

Okay, here's the base structure. The placeholder you can replace now are:

* `<name>` The discord's command name.
* `<prefixes>` The discord's command prefixes, separated by `and` or `,`
* `<code>` The Skript code that will be run once the command is executed.

DiSky will fire the code once any bots receive the following message:

**`<any prefixes><name>`**

Let's take a real example, and create a discord command that replies with `Pong!`:

```applescript
discord command ping:
    prefixes: !
    trigger:
        reply with "Pong!"
```

Easy, right? Now, whenever someone type `!ping`, the bot will reply with `Pong!`.

### Arguments

Let's try to make more complicated commands now. DiSky provide a way to ask for **Arguments** inside discord commands. When defining the command, as we did above, you are able to specify, right after the name, the arguments:

* Either the argument is optional or not.
* The argument's Type (Skript's type), the specified type **MUST** be able to be parsed in the command context.
* Optionally, the default value if the argument is marked as optional and no values are provided when someone execute the command.

It basically looks like that:

| Type: Optional               |  Default Value | Result                      |   |   |
| ---------------------------- | :------------: | --------------------------- | - | - |
| Text: :x:                    |      None      | `<text>`                    |   |   |
| Member: :white\_check\_mark: | `event-member` | `[<member=%event-member%>]` |   |   |
| Numner: :white\_check\_mark: |      None      | `[<number>]`                |   |   |
| Offline Player: :x:          |      None      | `<offlineplayer>`           |   |   |

{% hint style="info" %}
As you may notice, **Optional** arguments are simply surrounded by `[ ]` while keeping the default `< >` argument delimination.
{% endhint %}

So let's make a simply `reply` command, that reply with what the first argument is set to:

```applescript
discord command reply [<text>]:
    prefixes: !
    trigger:
        if arg-1 is not set: # We check if the provided optional argument is set
            reply with "Specify what you want me to say!"
        else:
            reply with arg-1
```

### Other Features

The discord commands also comes with features that are here to make your life easier.

#### Specific Origin

You can specify where your command can be executed through the `executable in`, where the input can either be `guild` or `private message` entry:

```applescript
discord command ...:
    executable in: guild
    trigger:
        # ...
```

#### Permission & Permission Message

Instead of using Skript conditions, DiSky can do that for you. It will check if the user who's executing the command has the specified permissions. If not, then the permission message will be sent back, all that through `permissions`, and `permission message` entries:

```applescript
discord command ...:
    permissions: administrator, manage server
    permission message: ":x: You don't have the permission to do that!"
    trigger:
        # ...
```

#### Utility Entries

Some entries are just here as a placeholder and can only be managed through Skript code. For example, any command can have a `description`, `usage`, and `category` entry. However, it can only be accessed through Skript's syntax, and is not shown in Discord in any way:

```applescript
discord command ...:
    description: This is a description
    usage: !name "hello world"
    category: Moderation
    trigger:
        # ...
```
