### Distance Quit
If a non-whitelisted player is nearby, the bot will disconnect

```js
let whitelist = ['Pix3lPirat3', 'Pix3lSlime'];
let disconnect_radius = 15;

bot.once("spawn", function () {
  let timer = setInterval(function() {
    let nearby_players = Object.values(bot.entities).filter(e => e.type === 'player').map(e => e.username); // [Username, Username]
    let difference = nearby_players.filter(x => !whitelist.includes(x)); // [Username, Username] of nearby non-whitelisted players

    if(!difference.length) return; // There were no non-whitelisted players nearby

    clearInterval(timer);
    bot.quit();
    console.log('[DistanceQuit] non-whitelisted players nearby:', difference.join(', '));
  }, 1000)
});
```