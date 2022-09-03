# 📙 F.A.Q.

Here's the most asked question on GitHub or DiSky's discord.

<details>

<summary>My bot doesn't come online, but I have no errors!</summary>

First of all, be sure your bot is loaded using the `/disky bots` commands. The name used in your code should appear with the username on Discord of your bot.

If it's been loaded, then try to **change its online status** to something else than `offline`.

</details>

<details>

<summary><code>This interaction has already been acknowledged</code> error ?</summary>

An interaction, such as a button click or slash command, can only be **acknowledged** (= we say to Discord that we've received the interaction) one time.

Outside the `defer interaction` the effect, **replying** to interaction will automatically **defer it**. It's the same for **opening modals**!

</details>

<details>

<summary>My variable is not set once the server restarts ...</summary>

If you're storing Discord values such as message, role, user, or member, then it will not **persists** after a server restarts. Thanks to Discord, each of these entity have a specific **unique ID** that we can use to **retrieve the entity** once the server restarts;

Simple store the **entity's** **ID** and **retrieve it back** once the server restarts!

</details>
