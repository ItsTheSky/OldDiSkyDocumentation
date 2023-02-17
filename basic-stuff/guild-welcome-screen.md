# 🔱 Guild Welcome Screen

You can change the screen displayed to new users through DiSky! Keep in mind that your server must have this feature enabled, otherwise it must be a community server!

## Model

The welcome screen is made out of two-part:

* The server's description
* A list of channels with an emoji and a small description of their utility

You'll be able to add **up to 5 channels** on this screen, and emojis are optional.

## Code

In order to pack all the changes in one request, you'll have to use the `modify welcome screen` section available since DiSky **v4.10.0**:

```applescript
set {_g} to guild with id "000" # or any other guild.

# the changes will be applied after the section's execution
modify welcome screen of {_guild}:
    
    # change the description to something else.
    # if not specified, then it'll be left untouched
    change the screen description to "Welcome to the server! Please read the rules and get roles before chatting."
    
    # add one or more channels info on the screen
    # up to 5 channels!
    add channel with id "000" named "Read our rules" with reaction "📜" to the screen
    add channel with id "000" named "Get roles" with reaction "🎟️" to the screen
```
