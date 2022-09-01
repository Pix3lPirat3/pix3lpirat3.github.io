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