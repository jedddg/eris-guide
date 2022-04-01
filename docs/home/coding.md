## Creating the initial files

Assuming you have your bot application set up, let's get started!

First, make a `config.json` file in the root directory. In this file we will store secret variables, like our **Bot Token**.

Here is an example of what the file can look like:

```json
{
    "token": "YOUR_BOT_TOKEN"
}
```

We want to make an `index.js` file in our root directory. This is the file we will use to run our Node.js application.

Here is the base code you can use to get your bot started:

```js
const { Client } = require("eris");
const config = require("./config.json");

const client = new Client(`Bot ${config.token}`);

client.on("ready", () => console.log("Ready"));

client.connect();
```

This is as simple as it gets. Eris is really easy to use!

To run this bot, go back to your terminal window and type

```bash
node index.js
```

## Creating Slash Commands

### Global

To make global slash commands, you can use [Client#createCommand](https://abal.moe/Eris/docs/0.16.1/Client#method-createCommand).

If you want to make global slash commands, explore this method yourself. This guide will not cover this method.

### Guild

To make guild slash commands, you can use [Client#createGuildCommand](https://abal.moe/Eris/docs/0.16.1/Client#method-createGuildCommand).

In this guide, we will be creating guild commands, as the bot we are making is in development, and does not need slash commands to be pushed to all servers (if your bot is in multiple guilds).

We must have a guildId to use. In your `config.json` file, add a new key to the object, called `"guildId"`.

Example:

```json
{
    "token": "YOUR_BOT_TOKEN",
    "guildId": "YOUR_GUILD_ID"
}
```

In our **ReadyEvent**, we can add the `createGuildCommand` method to create commands.

All slash commands must have a name and a description.

```js
const { Client, Constants } = require("eris");
const config = require("./config.json");

const client = new Client(`Bot ${config.token}`);

client.on("ready", () => {
    console.log("Ready");

    client.createGuildCommand(
        config.guildId,
        {
            name: "ping",
            description: "pong",
            defaultPermission: true,
        },
        Constants.ApplicationCommandTypes.CHAT_INPUT
    );
});

client.connect();
```

Our slash commands should now be registered.

But how can we use these slash commands to run a piece of code?

## Responding to Slash Commands

To respond to slash commands, we need to listen to the `Client#interactionCreate` event.

```js
client.on("interactionCreate", (interaction) => {});
```

_Empty interactionCreate event_

We should first check if the interaction is an instance of a slash command. If it isn't we stop the code.

We should also defer the interaction by using the [interaction#defer](https://abal.moe/Eris/docs/0.16.1/CommandInteraction#method-defer) method.

To get the command name, we can access the data property from interaction. `interaction.data` returns an object about the interaction. In there, we have a parameter called `name`. We can access this key in the object to get the slash command name.

[interaction#createFollowup](https://abal.moe/Eris/docs/0.16.1/CommandInteraction#method-createFollowup) is a method you can use to respond to deferred interactions. We will use this to respond to our ping command.

Here is an example of that:

```js
client.on("interactionCreate", (interaction) => {
    if (!(interaction instanceof CommandInteraction)) return;

    await interaction.defer();

    if (interaction.data.name === "ping") {
        return interaction.createFollowup({
            content: "pong",
        });
    }
});
```
