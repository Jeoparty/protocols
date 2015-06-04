# Websocket

## Handshake

## Events

### Buzz
Sent when a buzzer is hit.

```json
{
	"type": "event",
	"event": "buzz",
	"group": "<port id>",
	"buzzer": <buzzer id>
}
```

### Disconnected
Sent when one or more buzzers disconnected

```json
{
	"type": "event",
	"event": "disconnected",
	"group": "<port id>",
	"buzzer": <buzzer id> or null
}
```

If only a single buzzer disconnected `buzzer id` contains the id of the disconnected buzzer. If the whole buzzer group disconnected `buzzer id` is *null*.

### Connected
Sent when a buzzer is connected to an connected group

```json
{
	"type": "event",
	"event": "connected",
	"group": "<ports id>",
	"buzzer": <buzzer id>
}
```


## Commands
### List buzzers
Requests a list of *connected* buzzers

```json
{
	"type": "request",
	"request": "list-buzzers"
}
```

The mediator will respond with

```json
{
	"type": "data",
	"data": "buzzers",
	"groups": [
		{
			"group": "<port id>",
			"buzzers": [<buzzer id>, <buzzer id>, ...]
		},
		...
	]
}
```

### List ports
Requests a list of *available* ports

```json
{
	"type": "request",
	"request": "list-ports"
}
```

The mediator will respond with

```json
{
	"type": "data",
	"data": "ports",
	"ports": ["<port id>", "<port id>", ...]
}
```

### Connect
Connects the specified buzzer group.
```json
{
	"type": "command",
	"command": "connect",
	"port": "<port id>"
}
```

In case of success the mediator will respond with

```json
{
	"type": "data",
	"data": "group",
	"group": "<Connecting id>",
	"buzzers": [<buzzer id>, <buzzer id>, ...]
}
```

In case of an error the mediator will respond with error type *connect*

## Errors
All errors are sent in an uniform message:
```json
{
	"type": "error",
	"error": "<error type>",
	"message": "<error message>" or null,
	"cause": "<cause>" or null
}
```

| `error type` | cause | `message` | `cause` |
|-----------------|---------|-----------------|------------|
| connect | Connecting a buzzer group failed | Error message or *null* | *null* |
| invalid_json | Parsing a message failed due to invalid json sent | *null* | The invalid message |
| unknown_command | A unknown command was sent | *null* | The invalid message |
| invalid_data_type | A message contained an invalid value | Error message | The invalid field |
