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

### User Access
Change who can access the bot's commands by adding an array of usernames
```js
let whitelist = ['Pix3lPirat3', 'Pix3lSlime']; // CaSe SeNsItIvE
````

```js
const prefix = "!";

bot.on("chat", function (username, message) {
  if (username === bot.username) return;
  if (!whitelist.includes(username)) return; // <- We check if the player's username is in the whitelist array
  if (!message.startsWith(prefix)) return;

  var args = message.split(" ");
  const cmd = args[0].substring(prefix.length); // remove the prefix
  args = args.slice(1); // remove 'cmd' from array, return args[]

  if (cmd === "say") {
    bot.chat(args.join(" "));
  }
});
```