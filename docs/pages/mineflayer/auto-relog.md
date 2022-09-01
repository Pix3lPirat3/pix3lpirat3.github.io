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

  // The "end" event is called when the bot is no longer connected to the server (so it is called on "kicked" too)
  bot.on("end", function() {
      setTimeout(() => {
          start()
      }, 5000) // wait 5s (Common connection-throttle: 4s)
  })
}

start()
```