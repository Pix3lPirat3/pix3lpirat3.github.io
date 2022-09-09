### Nearby Entities
You can get an array of nearby players
```js
Object.values(bot.entities).filter(e => e.type === 'player' && e.username !== bot.username);
```
or even nearby mobs
```js
Object.values(bot.entities).filter(e => e.type === 'mob');
```

#### Filtering by Name
Get entities by name
```js
let cows = Object.values(bot.entities).filter(e => e.name === 'cow');
```

#### Filtering by Range
Get entities within a range
```js
let nearby = Object.values(bot.entities).filter(e => bot.entitie.position.distanceTo(e.position));
```

#### Combining Filters
Get entities within a range and by name
```js
let nearbyCows = Object.values(bot.entities).filter(e => bot.entitie.position.distanceTo(e.position) && e.name === 'cow');
```

Nearby Usage case: [MinePrompt](https://github.com/Pix3lPirat3/mineprompt/blob/main/addons/commands/nearby.js)