# Websocket data

## States
* New Game
  * Scoreboard: Empty board
  * Admin: Select Round
* Game Setup
  * Scoreboard
    * Preview board
    * New Player
  * Admin: Manage Players
* Scoreboard
* Answer (show answer, "buzzer time highscore")
* Double Jeopardy
* Results

## Data
### Game
```
"game": {
  "state": "new",
  "scoreboard": {},
  "players": {},
  "answer": {},
  "buzzer": {}
}
```

### Scoreboard
```
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
```

`winner` contains for every answer
* the `player index` of the winner,
* `false` for nobody or
* `null` for open answers.

### Player
```
"players": [
  {
    "id": "uuid",
    "name": "Sample Player",
    "score": 42,
    "buzzed": null,
    "connected": true
  }
]
```
`buzzed` contains the buzzer time relative to the start of the answer or
`null` when not buzzed.

### Answer
```
"answer": {
  "type": "text",
  "data": "Sample answer text.",
  "score": 100,
  "double_jeopardy": false
}
```

* `text`
  * `data` is answer text.
* `img`, `audio`, `video`, `code`
    * `data` is *base64* representation of file data.

