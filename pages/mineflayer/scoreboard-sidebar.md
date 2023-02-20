### Accessing Scoreboard
You can access the scoreboard object through
```js
bot.scoreboard
````

### Scoreboard to Array
You can convert the contents of the sidebar to an Array
```js
Object.values(bot.scoreboard.sidebar.itemsMap)
```

### Scoreboard Array to ChatMessage Text Array
The array consists of ChatMessage items, which has functions such as `getText()`, `toMotd()`, and others. If you want to strip the colors from the scoreboard then you can use `getText()`
```js
Object.values(bot.scoreboard.sidebar.itemsMap).map(e => e.displayName.getText())
````
