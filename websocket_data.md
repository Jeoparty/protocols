# Websocket data

## Handshake
```json
{
	"event": "ready"
}
```
Has to be sent by the client after it has connected and is ready to receive messages.

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
	"scoreboard": {},
	"players": {},
	"new_player": {
		"name": "playername",
		"color": "#FF00FF",
		"connected": true
	}
}
```
* `new_player` Is either `null` or 

#### Event: Add Player
```json
{
	"event": "add_player",
	"color": "#FF00FF"
}
```

#### Event: Update Name
Updates the name of the currently edited Player
```json
{
	"event": "update_player_name",
	"name": "playername"
}
```

#### Event: Confirm
Confirms the current player data
```json
{
	"event": "confirm_player"
}
```

#### Event: Start
```json
{
    "event": "start"
}
```
Starts the game

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
	"players": {},
	"buzzorder": {
		"uuid":time,
		"uuid":delay,
		"uuid":delay,
		...
	}
}
```

#### Event: Win, Fail, Oops, Exit
```json
{
	"event": "win"
}
```
* `event` can either be `win`, `fail`, `oops` or `exit`

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
      "color": "#FF00FF",
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

### Refresh
```json
{
	"event": "refresh"
}
```
Causes the current state to be resent

## Errors
### invalid_json
```json
{
	"error": "invalid_json",
	"errors": [
		{
			"description": "stuff is fucked up",
			"context": ["error", "is located", "here"]
		},
		...
	]
}
```
### jeopardy_exception
```json
{
	"error": "jeopardy_exception",
	"message": "everyting is on fire!"
}
```
### exception
```json
{
	"error": "exception",
	"message": "this shouldn't happen anyway"
}
```