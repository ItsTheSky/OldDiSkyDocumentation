# 📙 F.A.Q.

Here's the most asked question on GitHub or DiSky's discord.

<details>

<summary>My bot doesn't come online, but I have no errors!</summary>

Try these solutions:
- **Use the correct login code.** Join our Discord by clicking [here](https://discord.gg/6xqVPHE6pc) > Go to the #commands channel > Type `-s` > Select the "login" snippet > Copy the snippet and paste it into your code and edit the details accordingly, such as your bot's name and token.
 
- **Make sure all your intents are enabled.** Go to the Discord Developer Portal at https://discord.com/developers/applications > Click on your bot > Select "Bot" tab > Make sure every intent is enabled (presence intent, server members intent and message content intent, if your bot is in more than 100 servers you need to apply for intents)
  
-  **Make sure your bot token is valid.** Go to the Discord Developer Portal at https://discord.com/developers/applications > Click on your bot > Select "Bot" tab > Click on "Reset Token" > Click on "Yes, do it!" > Enter your 2FA auth code / backup code (if you don't have 2FA enabled on your account this step is not required) > Copy the token > Put the new token inside your login code

</details>

<details>

<summary><code>This interaction has already been acknowledged</code> error ?</summary>

Whenever you reply to an interaction (slash commands, buttons, dropdown, modal, ect), the bot sends the message to the Discord API which then you can see.
 
You cannot reply to an interaction twice, but you can "followup" the interaction with your message like this:
```applescript
# {_m} is a message builder
reply with {_m} and store it in {_lmsg}

# now we reference the last interaction reply and do a "followup"
reply with {_m} with reference {_lmsg}
```
  
What you can also do is "defer" the interaction.
There are 2 types of defer; The first is "update defer", which basically defers the message and basically just sends an interaction success signal. This only works on button, dropdown and modal interactions. To do it, use `defer the interaction`
  
The other one is "reply defer", which gives the user a "(bot) is thinking..." message. Keep in mind that you have up to 15 minutes to reply to your interaction, and when that time is over, you can't reply to that interaction anymore, and will count as an "unknown interaction". To do it, use `defer the interaction and wait`.

</details>

<details>

<summary>My variable is not set once the server restarts ...</summary>

A Discord snowflake entity (user, member, guild, channel, category, role, ect) is stored as an object in a variable.

Now, the stored objects are not permanent, so a solution is to store the entity's snowflake ID (usually from 18-19 characters, the length will get larger overtime) and then retrieve the entity from that ID using the retrieve effect or get expression.

</details>

<details>
  
<summary>I can't send messages with components!</summary>
  As of DiSky v4.4, advanced / rich messages has entered DiSky, therefore removing the ability of specifying components directly to the message.
  
  Read this wiki entry here: https://docs.disky.me/advanced-stuff/advanced-messages
</details>
