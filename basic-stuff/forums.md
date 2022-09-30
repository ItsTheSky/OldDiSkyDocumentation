# 📂 Forums

This page will explain managing forums, including posts, tags, and more.

### Forum channel

There's a specific channel type in DiSky & Discord: **Forum Channel**

They act like a text channel, but you cannot write there; it only holds **threads** that represent the available posts. Therefore, if you want to get threads out of a forum channel, you can simply do:

```applescript
set {_threads::*} to threads of forum with id "000"
```

{% hint style="success" %}
`forum` can also be used in **discord command's argument!**
{% endhint %}

* The **thread's name** will represent the **post's name**. (`discord name of XXX`)
* As a thread channel, you can use the `retrieve messages` effect to get the messages
* As a member container, `members of` expression is available to get active members of the post
* You can get the tags of a thread using `tags of <thread>`. Keep in mind this will only work with **posts' threads!**

### Tags

A specific post (or thread) can have none, one or more **forum tags**. The only way to get a forum tag is by using its name:

```applescript
set {_tag} to tag named "resolved" from forum channel with id "000"
```

{% hint style="warning" %}
Since each forum channel has its own created tags, we have to specify from which channel we're getting it.
{% endhint %}

You can also create tags, add them to the forum channel and finally add them to the posts:

```applescript
set {_created} to new tag named "test" with reaction "x"
```

At this stage, the tag itself is **not yet created on Discord,** so you cannot add it to posts! You'll have to add it to the forum channel first:

```applescript
add {_created} to tags of forum channel with id "000"
```

Now, you'll be able to add it to the post for instance:

```applescript
add {_created} to tags of thread channel with id "000"
```
