# 2⃣ Bot Creation

First, we need to create the application then the Discord bot itself

1. Go to [discord's application dashboard](https://discordapp.com/developers/applications/me) and click on `New Application`. You may have to log in!
2. Give the application a name under `App Name` then in the bottom right click `Create Application`.
3. You should now see your new application. Next, under `App Details` click on `Create a bot user`.
4. Click `Yes, do it` on the confirmation screen.
5. Under `App Bot User` find "Token" and copy it.

> :warning: This token is **private**, and if you lose it you'll have to **regenerate** another one. Keep in mind anyone who has it can do **whatever he or she wants** with your bot!

Now that it's created, let's invite it to our guild:

1. Find the `Client ID` at the top of the page.
2. Replace the `X`'s with the client ID in this URL: `https://discord.com/api/oauth2/authorize?client_id=XXXXXXXXXXXXXXXXXX&permissions=8scope=bot%20applications.commands`

> :bulb: You can give this link to anyone, so he or she can invite your bot to their server!

1. Simply click the changed link, follow the information, and your bot should join your server in the next seconds!

**Go to the next page, where you'll see how to load it through DiSky & Skript!**
