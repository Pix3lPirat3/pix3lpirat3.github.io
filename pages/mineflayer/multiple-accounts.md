### Multiple Accounts
You can control multiple accounts with mineflayer, by either sharing a thread (bad) or by multithreading (recommended)

Multithreading (**Recommended**)
You'll need two files for this, which we'll call `parent.js` and `child.js`.
The reasons for this is that the `parent.js` file will start the `child.js` file, which will be the bot.
```js
// parent.js
const child_process = require("child_process");
function spawnChild(username = 'Child', host = 'localhost', port = 25565, version = '1.18.2', skipValidation = false) {
    let args = [ username, host, port, version, skipValidation ]
    let client = child_process.fork("./child.js", args);
}

spawnChild('Child1', 'play.deptofcraft.com', 25565, '1.18.2', false)
spawnChild('Child2', 'play.deptofcraft.com', 25565, '1.18.2', false)
spawnChild('Child3', 'play.deptofcraft.com', 25565, '1.18.2', false)
```` 

```js
// child.js
var args = process.argv.slice(2) // remove [node.exe, child.js]
var mineflayer = require('mineflayer')
var bot = mineflayer.createBot({
  username: args[0],
  host: args[1],
  port: args[2],
  version: args[3],
  skipValidation: args[4],
  auth: (args[4].toString() == 'true') ? undefined : 'microsoft'
})
bot.on('spawn', function() {
  console.log(` >> ${bot.username} has spawned..`)
})
bot.on('kicked', console.log)
bot.on('error', console.log)
```

### Shared Thread (**Not Recommended**)
It is not recommended to control bots on the same thread, as once you start performing resource hogging functions, the bots *will* start to drop.
```js
var mineflayer = require('mineflayer')
let one = mineflayer.createBot({})
let two = mineflayer.createBot({})

one.on('spawn', function() {
  console.log(`Bot #1 has spawned`)
})

two.on('spawn', function() {
  console.log(`Bot #2 has spawned`)
})
```