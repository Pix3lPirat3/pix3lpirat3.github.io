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