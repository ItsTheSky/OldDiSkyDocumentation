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
