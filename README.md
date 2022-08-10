# Snippets

> Learn the basics of **JavaScript** and **Mineflayer** before attempting to use these snippets

### Introduction

Welcome to a collection of snippets collected by Pix3lPirat3

<sup>*Note: Not all of these may be created by Pix3lPirat3, just some snippets gathered into a collection, credits are given.*</sup>
<br>
<sup>*This collection may have snippets that are more written out than others, to provide easier to understand code*</sup>

### Session Login
You can login to an account by using a session, remember to set `skipValidation: true` and to **not** set an `auth` type.
<br>
<sup>Note: As for how to retrieve the "session" object, check [prismarine-auth](https://github.com/PrismarineJS/prismarine-auth) (Do not ask for support, read prismarine-auth)</sup>
```js
const bot = mineflayer.createBot({
  host: 'localhost',
  port: 25565,
  version: '1.18.2',
  session: {
    accessToken: session.accessToken,
    clientToken: session.selectedProfile.id,
    selectedProfile: {
      id: session.selectedProfile.id,
      name: session.selectedProfile.name
    }
  },
  skipValidation: true
})
```

### Auto Relog / Reconnect
The simple way to automatically reconnect once your bot has been disconnected/kicked is to listen to the `end` event, and call a function that has your `mineflayer.createBot` function inside.
<br>
<sup>Reminder: If you want your events and plugins to be persistent after reconnecting, you **must** initialize them after you call `mineflayer.createBot`</sup>

```js
function start() {
  const bot = mineflayer.createBot({
    host: 'localhost',
    username: 'Pix3lPirat3',
    auth: 'microsoft'
  })

  // bot.loadPlugin(pathfinder) // load plugins

  // bot.on('chat', console.log) // load event listeners

  bot.on("kicked", console.log)
  bot.on("end", function() {
      setTimeout(() => {
          start()
      }, 5000) // wait 5s (Common connection-throttle: 4s)
  })
}

start()
```


### Chat Commands
You can make the bot listen for commands inside the public chat, such as saying `!say hello world` and having the bot chat `hello world`
```js
const prefix = "!";

bot.on("chat", function (username, message) {
  if (username === bot.username) return;
  if (!message.startsWith(prefix)) return;

  var args = message.split(" ");
  const cmd = args[0].substring(prefix.length); // remove the prefix
  args = args.slice(1); // remove 'cmd' from array, return args[]

  if (cmd === "say") {
    bot.chat(args.join(" "));
  }
});
```