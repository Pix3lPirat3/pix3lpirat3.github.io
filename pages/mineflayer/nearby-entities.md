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
