# mog-inspector

Debugger for multiplayer online games running locally using Socket.io.

## Expected Socket.io events

### `state`

Expects `'state'` socket.io events to be sent, with payload (`state` structure) such as:

```json
{
    "entityType1": [
        {
            "username": "Tsunemori",
            "x": 50,
            "y": 30,
            "vx": 2,
            "vy": 0,
            ...
            "id": "fu7ib7r6I&RV"
        },
        {
            "x": 36,
            "y": 876,
            "vx": 1,
            "vy": 2,
            ...
            "id": "5276894357q9"
        },
        ...
    ],
    "entityType2": [...],
    "entityType3": [...],
    ...
}
```

Only entity's:
- position (`x` and `y`)
- speed (`vx` and `vy`)
- `username`
will be taken into account.

Entity's need an `id` in order to be selectable for longer than one frame (it is needed in order to find it in the new state).

### `inspector-config` (optional)

The payload is a entityType->color map, which will be used for rendering.

server example:
```js
  socket.on('im-inspector', function () {
    console.log('inspector attached')
    socket.emit('inspector-config', {
      players: 'blue',
      enemies: 'red',
      coins: 'yellow'
    })
  })
```

## Controls

Move the camera using the WASD keys.

Use -/+ to zoom.

Click to select an entity and inspect it. (it also gets logged into the console)