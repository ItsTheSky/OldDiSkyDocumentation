# 🗂 SelectMenu/Dropdown

This page will describe how to create and use dropdown/select menus introduced in Discord as a component.

### The basics

First, what is a dropdown? It's a component of a message or a Discord modal where the user has a choice between several options. Recently, Discord also offers access to the choice of entities such as rooms, roles, or users.

DiSky provides two types of dropdowns: one for predefined values (string dropdown, the user has the choice between fixed values) and one for entities, it will then be up to the user to choose the roles, rooms, or users he wants to select.

### Creating a String Dropdown

To create a simple dropdown with predefined choices, use this syntax:

```applescript
set {_dp} to new dropdown with id "test"
```

{% hint style="warning" %}
Like any other component, the ID must be unique in the message.
{% endhint %}

### Creating an Entity Dropdown

You can specify the types of entities that the user will be able to provide among the following 3:

* User
* Channel
* Role

Note that you can mix up **roles & users**, but **CAN NOT** mix channels with any other!

```applescript
set {_dp} to new entity dropdown with id "test" targeting "users" and "roles"
# OR
set {_dp} to new entity dropdown with id "test" targeting "channels"
```

### Changing properties

We can modify some properties of our dropdown, regardless of its type, such as:

* Minimum values (`set min range of {_dp} to 1`)
* Maximum values (`set max range of {_dp} to 2`)
* Placeholder (`set placeholder of {_dp} to "Select a role ..."`)

{% hint style="success" %}
The placeholder is what is shown before opening the dropdown itself!

It tells what the user is asked for.
{% endhint %}

### Adding choices (String Dropdown)

If your dropdown is a string dropdown, then you can add **options** that the user will be able to select. Each option comes with a:

* Name, what is shown on Discord. <mark style="color:red;">Required.</mark>
* Value, is not shown on Discord, but will be returned once the user completes the interaction. <mark style="color:red;">Required</mark>
* Emoji, also shown on Discord. <mark style="color:green;">Optional.</mark>
* Description, also shown on Discord. <mark style="color:green;">Optional.</mark>

Here's an example code to add an option:

{% code overflow="wrap" %}
```applescript
add new option with value "value" named "A choice .." with description "Chose wisely!" with reaction "joy" to options of {_dp}
```
{% endcode %}

{% hint style="warning" %}
The value specified in an option **cannot be found in another option**, they are unique, like IDs!
{% endhint %}

### Retrieve values

Now out dropdown is sent, users can interact with them. There are two separate events for the two types of dropdowns (string and entity). In both cases, however, you can use `event-dropdown` to retrieve the identifier of the dropdown used.

#### String dropdown

```applescript
on dropdown click:
```

> You can use `selected values` to get the values the user selected inside of this event.

#### Entity dropdown

```applescript
on entity dropdown click:
```

> You can use `selected entities` to get the roles, channels and/or users selected inside of this event.

{% hint style="warning" %}
Don't forget to **reply or defer** this interaction!
{% endhint %}
