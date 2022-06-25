# 3⃣ Bot Loading



> :warning: You should check [**Bot Creation**](bot-creation.md) before if you haven't yet!

You'll see here how to use DiSky in a Skript file, especially how to load your bot.

### 0. Introduction to Scopes <a href="#scopes" id="scopes"></a>

DiSky is using a lot of **scopes**, which are very similar to the event system. Instead of being in a trigger (such as on load or a command), a scope is the trigger itself and thus can be placed in a file without a parent.

Scopes come with two sorts of **entry** (entry looks like `name: value`):

*   Value entry (form: `name: value`), event-related literals are forbidden (only global variable & script options works here):

    ```javascript
    ```

: token: "token"

````

* Section entry (form: `name: <line break> code ...`), code that could be running.
    ```javascript
<scope name>:
		on ready:
        	send "%event-bot% has been loaded!" to console
````

It will load automatically when the code is reloaded.

### 1. Bot Scope

DiSky's bot creation scope looks like this:

```javascript
# The name specified here doesn't matter with the one used in the developer portal. 
# This one will only be used for recognize your bot in Skript code.
define new bot named "BOT NAME": 
    
    # The bot's token, small remember, it MUST be private!
    token: "BOT TOKEN"
    
    # Gateway intents enabled, others that are not listed here will be disabled.
    # If you're not sure about that, left it as 'default intents'.
    intents: default intents
    
    # Advanced bot option, defining websocket, connection and privacy parameters.
    # Here again, if you're not sure about that, left it as 'default intents'.
    policy: all
    auto reconnect: true
    compression: none
    
    # Optional section code:
    # Fired once the bot, and every guilds, are ready-to-use.
    on ready:
    	# </>
    # Fired once a guild, and every members, are ready-to-use
    on guild ready:
    	# </>
```

Reload your **script**, and wait a little. Your bot should be marked as online!

### 2. Ready Sections

You can execute codes as soon as a **bot** or a **guild** is ready to use.

> :bulb: An entity being ready-to-use mean every action or properties are loaded correctly.

#### `on ready`

This section will be run once the bot is fully loaded, all guilds included.

The only event-value here is `event-bot` to get the bot instance that's just loaded:

**Example:**

```python
<scope name>:
    on ready:
        send "&a%event-bot%&2 has been loaded!" to console
```

This section is also where **global lication commands** are registered. You can get more information about that in the **Application Commands** page of this wiki.

#### `on guild ready`

This section will be run once a guild is fully loaded by a bot. All of these members has been cached (according to the member policy) and same for other entities such as channels, roles, etc...

There's two event value here:

* `event-bot`, get the bot who loaded the guild
* `event-guild`, get the guild that has just been loaded

**Example:**

```applescript
<scope name>:
    on guild ready:
        send "&a%event-bot%&2 just loaded &a%event-guild%&2 guild!" to console
```

This section is also where **local application commands** are registered. You can get more information about that in the **Application Commands** page of this wiki.
