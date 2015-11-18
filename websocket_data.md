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
  "name": "Sample Player",
  "score": 42,
  "connected": true
]
```

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

### Buzzer Times
````
"buzzer": [
  null,
  1337,
  42,
  null
]
```

`buzzer` contains for every player at their player index an buzzer time
relative to the start of the answer. `null` when not buzzed.

### Scores
```
"scores": [
  0,
  500,
  200
  -100
]
```

`scores` contains for every player at their player index an score value.
