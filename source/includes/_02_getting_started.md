# Getting Started

## Primer

First you have to grab yourself a bot token from the [Discord developer panel](https://discordapp.com/developers/applications/me). Click on **"New App"**, add a name and hit **"Create App"**. Next you have to turn this app into a bot by pressing the **"Create a Bot User"** button. And now you can see (or not really, it's revealed) your bot **Token**. Copy and save it you'll need this again later :).

<aside class="notice">
You must have a running MongoDB server.
</aside>

## Setup isic via npm

> To install isic, simply:

```bash
npm install --save isic
```
Install the ``isic`` package via npm and import it.

> Import the Bot class and provide the neccessary settings

```js
const {Bot} = require("isic")

let bot = new Bot({
    token: "YOUR_DISCORD_TOKEN",
    database: {
        // you can also change host: and port: here...
        username: "MONGODB_USERNAME",
        password: "MONGODB_PASSWORD"
    }
})
```

Running this script starts the Bot with the minimal setup, as in not loading 3rd party modules and using a few builtin modules like ``@BotName ping``.


## Setup directly

To run isic directly simply [download the newest release](https://github.com/atomicptr/isic/releases) or clone the repository via:

``git clone git@github.com:atomicptr/isic.git``.

You have to rename the ``config.template.json`` file to ``config.json`` and edit it:

1. Add your Discord token to this line ``"token": "YOUR_DISCORD_TOKEN",``
1. Change ``"username": ...`` and ``"password": ...`` to the appropriate authentication details of your MongoDB installation.
1. Start the bot via ``npm start``

Done. You should have a running Bot, which loads modules from ``./node_modules/`` and ``./modules/``.
