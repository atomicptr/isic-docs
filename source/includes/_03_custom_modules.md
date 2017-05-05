# Custom Modules

This part of the documentation is dedicated to writing your own custom modules.

## Module structure

The directory structure of a module usually looks like this:

> A typical module structure

```bash
    my_module/
        module.json
        my_module.js
```

The general structure is up to you though, you only have to have:

* A directory which contains the module
* A module.json file
* At least one .js file as entry point

Which means you could technically write your modules in for instance CoffeeScript and compile that script into a file, which then serves as your entry point.

Or split the file into multiple files, whatever makes you happy.

## The module.json file

All isic modules must contain a file called ``module.json`` in their root - this file holds various information relevant to isic.

> module.json example

```json
{
    "name": "My Module",
    "identifier": "com.example.my-module",
    "main": "my_module.js",
}
```

The module.json file must contain valid JSON (No comments!).

### Name

The name of the module

### Identifier

**NOTE**: The identifier has to be unique or else your module won't be loaded, it's common practice to either use your URL like this:

* com.example.module-name
* com.google.module-name
* org.js.isic.fancy-module

or to identify them by for instance your Github username (which is what I prefer):

* github.atomicptr.fancy-module
* github.atomicptr.isic-rss
* github.isic.fancy-module2

### Main

The heart of your module, isic will load this JavaScript file which adds actions and other custom behaviour to the bot.

> An example for a JavaScript file in "main"

```js
module.export = function(bot) {
    bot.command("hello", (res, args) => res.reply("Hello, Human!"))
}
```

### Requires Permission

The ``requiresPermission`` option allows you to block your module in servers where the bot doesn't have the specified permissions, for instance
writing a module which can kick or ban people wouldn't make much sense if isic doesn't have the **KICK\_MEMBERS** or **BAN\_MEMBERS** permission.

This field accepts a JSON array with the permission names as paramters: ``"requiresPermission": ["KICK_MEMBERS", "BAN_MEMBERS"]``.

<aside class="notice">
You can find the list of permissions <a href="https://discordapp.com/developers/docs/topics/permissions" target="_blank">here</a>.
</aside>

### Ignore DM

The ``ignoredm`` option allows you to... well ignore Direct Messages if set to ``true``.

## Actions

An ``Action`` is defined as something isic can interact with/react to, there are currently 4 different types of actions:

* **Command**, a command prefixed (usually) by ``!`` for instance typing ``!hello`` into the chat will trigger the command ``hello``
* **Hear**, this action will be executed when the bot "hears" a certain keyword
* **Respond**, actions which are prefixed by mentioning the bot via ``@BotName do something for me, pal``
* **Interval**, the only interaction not caused by the user but instead by an internal timer that emits a signal every (default setting) 5 minutes.

## --- Command Action

> "hello" command

```js
bot.command("hello", (res, args) => {
    res.reply("Hello!")
})
```

> "echo" command

```js
bot.command("echo", (res, args) => {
    res.send(args.join(" "))
})
```

A **Command** is an action prefixed (usually) by an ``!``, you can trigger this action for instance by typing something like ``!hello`` into the chat.
This will run a command called ``hello``.

The callback of a **Command** equips you with 2x parameters, a **Response** object (more about this later) and an array of **Arguments**.

You can also provide arguments to a command like this: ``!echo Hello World!``, in this case the arguments given to the callback would be ``["Hello", "World!"]``



## --- Hear Action

> kappa

```js
bot.hear(/kappa/ig, res => {
    res.reply("https://img-url.to/a/kappa-image.png")
})
```

> "Hear"ing an emoji

```js
bot.hear(/👍/g, res => {
    if(res.canI("ADD_REACTIONS")) {
        res.message.react("👍")
    }
})
```

When using **Hear** actions you usually want to make the bot react to certain phrases which users might post into chat.

In contrast to commands instead of providing a string you have to supply a **Hear** action with a regular expression or RegEx in short. For instance if you want to
react to someone saying hat, cat or rat you can add ``/(h|c|r)at/i`` as parameter.

The callback will also provide you with a **Response** object (more about this later).

## --- Respond Action

...

## --- Interval Action

...

## Permissions

...

## Persistent Data

...

## The Module Interface

...

## The Response Object

...
