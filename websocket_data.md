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
* Scoreboard (`scoreboard`)
* Answer (`answer`)
  * Show answer
  * Buzzer time
* Double Jeopardy (`double_jeopardy`)
* Results (`results`)

### New Game
```json
{
	"state": "new",
	"rounds": {
	    "round1": "First Round",
	    "round2": "Second Round"
    }
}
```

#### Event: Select Round
```json
{
	"event": "select_round",
	"round": "round1"
}
```

### Game Setup
```json
{
	"state":  "setup",
	"action":{},
	"scoreboard": {},
	"players": {}
}
```
* `action` Contains additional information about an currently performed action within this screen (e.g. add player). It may be ommited.

#### Event: Add Player
```json
{
	"event": "add_player",
	"color": <specify me>
}
```

#### Action: Edit Player
```json
{
	"type": "edit_player",
	"name": "playername",
	"color": <specify me>
}
```

##### Event: Update Name
Updates the name of the currently edited Player
```json
{
	"type": "update_player_name",
	"name": "playername"
}
```

##### Event: Confirm
Confirms the current player data
```json
{
	"type": "confirm_player"
}
```

### Scoreboard
```json
{
	"state": "scoreboard",
	"scoreboard": {},
	"players": {},
	"current_player": "uuid"
}
```

#### Event: Select answer
```json
{
	"event": "select_answer",
	"category": 0,
	"answer": 0
}
```
* `category` is the index of the category
* `answer` is the index of the answer

### Answer
```json
{
	"state": "answer",
	"answer": {},
	"players": {}
}
```

## Data
### Game
```
{
  "game": {
    "state": "new",
    "scoreboard": {},
    "players": {},
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
          "uuid-0",
          "uuid-1",
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
* the `player uuid` of the winner,
* `false` for nobody or
* `null` for open answers.

### Player
```
{
  "players": {
    "uuid": {
      "name": "Sample Player",
      "color": <specify me>,
      "score": 42,
      "active": true,
      "buzzed": null,
      "connected": true
    }
  }
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

## Global Client Events
### Connect buzzergroup
```json
{
	"event": "connect_buzzergroup",
	"type": "serial",
	"device": "/dev/serial0"
}
```
* `type` can be either `serial` or `keyboard`