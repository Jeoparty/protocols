# Websocket data

## States
* New Game (`new`)
  * Scoreboard: Empty board
  * Admin: Select Round
* Game Setup (`setup`)
  * Scoreboard
    * Preview board
    * New Player
  * Admin
    * Manage Players
* Scoreboar (`scoreboard`)
* Answer (`answer`)
  * Show answer
  * Buzzer time
* Double Jeopardy (`double_jeopardy`)
* Results (`results`)

## Data
### Game
```
{
  "game": {
    "state": "new",
    "scoreboard": {},
    "players": [],
    "answer": {}
  }
}
```

### Scoreboard
```
{
  "scoreboard": {
    "name": "Sample round",
    "points": [100, 200, 300, 400, 500],
    "categories": [
      {
        "name": "Test Group 1",
        "winner": [
          0,
          1,
          false,
          null,
          null
        ]
      }
    ]
  }
}
```

`winner` contains for every answer
* the `player index` of the winner,
* `false` for nobody or
* `null` for open answers.

### Player
```
{
  "players": [
    {
      "id": "uuid",
      "name": "Sample Player",
      "score": 42,
      "active": true,
      "buzzed": null,
      "connected": true
    }
  ]
}
```
`buzzed` contains the buzzer time relative to the start of the answer or
`null` when not buzzed.

### Answer
```
{
  "answer": {
    "type": "text",
    "data": "Sample answer text.",
    "score": 100,
    "double_jeopardy": false
  }
}
```

* `text`
  * `data` is answer text.
* `img`, `audio`, `video`, `code`
    * `data` is *base64* representation of file data.
