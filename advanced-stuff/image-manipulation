# 🖼️ Image Maniuplation

> ⚠️ I (Cerial) never used SkImage, so some things I may say here may not be true. I know stuff because I worked with image manipulation in JavaScript using Canvas (@napi-rs/canvas on nodejs)

## What is image manipulation?

Basically, image manipulation is making an image inside of code. Sometimes, it can be easy and can be hard to do.

In other languages like JavaScript, there are special libraries which do that like Canvas. You can check out the DiscordJS tutorial [here](https://discordjs.guide/popular-topics/canvas.html#setting-up-napi-rs-canvas) for a bit of an idea how this works, but we are using Skript, so we will be using an addon called **SkImage**.

## How to install it?

It is the same installation process like any other plugin or Skript addon.

1. Go to the latest release by clicking [here](https://github.com/SkyCraft78/SkImage/releases/latest)
2. Click on the JAR file which should be prefixed with "SkImage"
3. Wait until it finishes downloading
4. Do one of these:
    1. Restart your server by doing /stop and by starting it again
    2. (May lead to crashes and plugin instability) Reload your server with **/reload confirm**.
5. Do **/version SkImage**, and if it sends the version then you're good to go! If not, check that you restarted/reloaded your server correctly.

## Are there any other tools I can use?

I personally recommend designing your image with an image design software like Photoshop, Paint.NET, GIMP, or whatever you like.

## How to make an image?

### Making the image itself
To make an image, you need to make a new image by doing the following:
```applescript
set {_img} to new image with size 300, 100
```

What this does is it makes an image with the resolution 300x100 and stores it in {_img}. It will look something like this:

> ⚠️ The preview is from Photoshop! And also the image won't be round, it is just my screenshotting tool doing that. And also, the previews after that will be raw previews from SkImage.

> ⚠️ If you save that transparent image and use it in Discord or if you open it in your computer, nothing will appear since the image is transparent. Stuff will appear once we draw stuff on the image.

![](https://cdn.upload.systems/uploads/Vtl6vSwn.png)

### Adding some text
To add text, you need to add a font from the installed fonts on your operating systems, or you can download a font and add it to a fonts folder.

For example, we want to use the **Minecraftia** font, there are 2 ways to add it.

> ⚠️ We are showing how to add system fonts for Windows systems. It may be different for Linux / MacOS users.

1. Adding the font to the entire computer (Not recommended, only possible if you are doing this locally or if you have access to the entire system.)
   1. Download the font from [here](https://www.dafont.com/minecraftia.font)
   2. Extract the zip file you got, and double-click on the "Minecraftia-Regular.ttf"
   3. Click on "Install"
   4. It should be ready to be used! **If you can't use it, you may need to restart your computer to apply the changes.**
2. Adding the font to SkImage (Recommended, works on any host that allows you to upload any type of file such as Minehut and many more)
   1. Download the font from [here](https://www.dafont.com/minecraftia.font)
   2. Extract the zip file you got
   3. Make a new folder in the plugins folder, and name it "fonts"
   4. Put the font in there
   5. Initialize it by using `register font from folder "plugins/fonts"`
   6. It should be ready to be used!

When making the text, we will obviously need the X and Y coordinates of where to put the image. We will center the text, so we need to get the centered coordinates.

To get the coordinates in Photoshop, simply follow this GIF:

![](https://cdn.upload.systems/uploads/isoTSd2x.gif)

We can see the coordinates we got is X: 150, Y: 50. We will use those in the code.

After we initialized the font, we can now make the text. This is the code we will use:
```applescript
# Make the font style.
# We will use the font we downloaded (Minecraftia) and we will use size 10.
# NOTE: The reason why we called it as "Minecraftia-Regular" is because that's the name of the font file. You can re-name it to something else if you wish.

# Font name                                        Font name                 Font size
#    ↓                                                 ↓                         ↓
set {_font} to new font style with font name "Minecraftia-Regular" and with size 10

# Now, we will draw the text on the image.
# We will draw "Hello World!" onto the image since that's what we want.
# Also, the "with align center" keyword allows SkImage to draw the text using the center coordinates.
# To get coordinates of a spot, you can use Photoshop's Rulers, and then look at the x and y values of where the ruler is at.

#       The text             The font  Coord. of text           Color of text       The image   Centers the text
#          ↓                     ↓          ↓                          ↓                 ↓              ↓
draw "Hello World!" with font {_font} at 150, 50 with color from rgb 0, 0, 0 on image {_img} with align center
```

### Adding another image

Adding another image can be useful for 3 things:

1. You can use that image to modify it for your needs (needs to be done at the very first step instead of making it)
2. Adding it as an image for your image (can be done at any step as long as it doesn't overlap any text and/or other images)
3. Adding it as a background (needs to be done before the text)

You can add an image from:
- A URL
- A file stored on your server
- (Really advanced stuff) from the Base64 encoding

To demonstrate, we will use only the URL and file, since no one should be using Base64.

First, get the images.
```applescript
# Get an image from local files; Will not be added if the file was not found.
#                                      The image's path
#                                             ↓
set {_images::1} to image from file "plugins/images/dog.png"

# Get an image from a URL
#                                                         URL of the image
#                                                                 ↓
set {_images::2} to image from url "https://thumbs.dreamstime.com/b/golden-retriever-dog-21668976.jpg"
```

And now let's draw them.

> ⚠️ If the images you imported are bigger than the original image you're making, then you will see parts of the image instead of the whole image.

```applescript
# Draw image 1 first
draw image {_images::1} on {_img} at 0, 50

# Draw image 2
draw image {_images::2} on {_img} at 50, 50
```

Also, I am aware that there will be problems with this since the images we import are bigger than the original image's size.

### Drawing shapes

> ⚠️ You can only draw lines and rectangles (rounded/not rounded).

#### Line

This will just draw a line on the image from point A to point B we specify.

Here are the details of the line:
- Point A: 10x10
- Point B: 289x69
- Width: 5 pixels

Here is our code:
```applescript
#              Line width  From coord. To coord.                 Line color   Image
#                    ↓        ↓          ↓                           ↓          ↓
draw line with width 5 from 10, 10 to 289, 69 with color from rgb 0, 0, 0 on {_img}
```

Result:

![](https://cdn.upload.systems/uploads/hVVO5Wa3.png)

#### Rectangle

**Non-rounded**

To get the X and Y coordinate you want to place the rectangle on, you need to get a central coordinate. This means that if you want to make a border around your image, you will set the coordinates to `0, 0` for it to be centered. This works on any image.

This is an example of image border:
```applescript
#        Rect. center coord.   Image size                   Rect. color  Image
#                  ↓                ↓                            ↓         ↓
draw rectangle at 0, 0 with size 300, 100 with color from rgb 0, 0, 0 on {_img}
```

This will draw a black border around the image.

**Rounded**

If you want a **rounded** rectangle, add `rounded` before `rectangle`, but there are a few more parameters we need to add:

> ⚠️ Again, some stuff might not be correct here, so do some testing to get your desired result!
```applescript
#                Rect. center coord.   Image size                  Rect. color            Rect. radius  Image
#                          ↓                ↓                            ↓                      ↓         ↓
draw rounded rectangle at 0, 0 with size 300, 100 with color from rgb 0, 0, 0 with arc size 300, 100 on {_img}
```
### Saving & Uploading the image

To upload the image and then upload it to Discord, you need to first save the image and then upload it to a channel or use it in a reply.

#### Saving the image

> ⚠️ Make sure that saving is the last step you do before uploading the image, otherwise any other changes will **not** be counted!

It is a simple expression. As noted above, put this when you are done drawing your image:
```applescript
save image {_img} to file "plugins/images/img-1.png"
```

#### Uploading the image

There are a few factors when making an image and then uploading it:
- Server performance
- Internet connection (ping between Discord and your server)
- Image size

It is recommended that you try reducing the file size so that it would upload faster.

To upload an image, put this code:
```applescript
# Defers the reply so in case you have slow internet connection you won't get an "Unknown Interaction" error
defer the interaction and wait

# Uploads the image
#                Path to file                                 Channel ID
#                      ↓                                            ↓
upload file "plugins/images/img-1.png" to channel with id "123456789012345678"
```

### To wrap it up

You learned how to make an image using SkImage, now go make beautiful automated images using SkImage!

*Guide made by Cerial (CerialPvP on GitHub)*

> ℹ️ For any problems, ping Cerial in DiSky discord.
