# Getting Started

## Primer

First you have to grab yourself a bot token from the [Discord developer panel](https://discordapp.com/developers/applications/me). Click on **"New App"**, add a name and hit **"Create App"**. Next you have to turn this app into a bot by pressing the **"Create a Bot User"** button. And now you can see (or not really, it's revealed) your bot **Token**. Copy and save it you'll need this again later :).

## Setup isic via npm

> To install isic, simply:

```bash
npm install --save isic
```
Install the ``isic`` package via npm and import it.

> Importing the Bot class and provide the neccessary settings

```js
const {Bot} = require("isic")

let bot = new Bot({
    token: "YOUR_DISCORD_TOKEN",
    database: {
        username: "MONGODB_USERNAME",
        password: "MONGODB_PASSWORD"
    }
})
```

<aside class="notice">
You must have a running MongoDB server.
</aside>
