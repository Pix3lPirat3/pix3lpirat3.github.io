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

### Nearby Entities
You can get an array of nearby players
```js
Object.values(bot.entities).filter(e => e.type === 'player' && e.username !== bot.username);
```
or even nearby mobs
```js
Object.values(bot.entities).filter(e => e.type === 'mob');
```
Usage case: [MinePrompt](https://github.com/Pix3lPirat3/mineprompt/blob/main/addons/commands/nearby.js)

### Online Players
<sup>Note: You cannot access the `entity` field of a player unless the player is in your view distance</sup>

```js
let players = Object.keys(bot.players);
let list = players.map(e => e.username);
console.log(list.join(', ')); // Pix3lPirat3, Pix3lSlime, Pix3lP3nguin
```

### Block At Knees
Get the block in front of the bot's knees
```js
function getViewDirection(pitch, yaw) {
    const csPitch = Math.cos(pitch)
    const snPitch = Math.sin(pitch)
    const csYaw = Math.cos(yaw)
    const snYaw = Math.sin(yaw)
    return new Vec3(-snYaw * csPitch, snPitch, -csYaw * csPitch)
}

bot.blockAtKnees = (matcher = null) => {
    const { position, height, pitch, yaw } = bot.entity
    const viewDirection = getViewDirection(pitch, yaw)
    return bot.world.raycast(position, viewDirection, 1, matcher)
}

console.log('Block At Knees:', bot.blockAtKnees());
```

Using getViewDirection from: <https://github.com/PrismarineJS/mineflayer/blob/master/lib/plugins/ray_trace.js>
Simply removed the `eyePosition` field, since the entity.position returns the entity's knees, and filled in the fields with entity `position` instead.