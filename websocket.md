# Websocket

## Handshake

## Events

### Buzz
Sent when a buzzer is hit.

```json
{
	"event": "buzz",
	"pool": "<pool id>",
	"buzzer": <buzzer id>
}
```

### Disconnected
Sent when one or more buzzers disconnected

```json
{
	"event": "disconnected",
	"pool": "<pool id>",
	"buzzer": <buzzer id> or null
}
```

If only a single buzzer disconnected `buzzer id` contains the id of the disconnected buzzer. If the whole buzzer pool disconnected `buzzer id` is *null*.

### Connected
Sent when a buzzer is connected to an connected pool

```json
{
	"event": "connected",
	"pool": "<pool id>",
	"buzzer": <buzzer id>
}
```


## Commands
### List buzzers
Requests a list of *connected* buzzers

```json
{
	"list": "buzzers"
}
```

The mediator will respond with

```json
{
	"response": "buzzers",
	"pools": [
		{
			"pool": "<pool id>",
			"buzzers": [<buzzer id>, <buzzer id>, ...]
		},
		...
	]
}
```

### List pools
Requests a list of *available* pools

```json
{
	"list": "pools"
}
```

The mediator will respond with

```json
{
	"response": "pools",
	"pools": ["<pool id>", "<pool id>", ...]
}
```

### Connect
Connects the specified buzzer pool.
```json
{
	"command": "connect",
	"pool": "<pool id>"
}
```

In case of success the mediator will respond with

```json
{
	"result": "connect",
	"pool": "<pool id>",
	"buzzers": [<buzzer id>, <buzzer id>, ...]
}
```

In case of an error the mediator will respond with error type *connect*

## Errors
All errors are sent in an uniform message:
```json
{
	"error": "<error type>",
	"message": "<error message>" or null,
	"cause": "<cause>" or null
}
```

| `error type` | cause | `message` | `cause` |
|-----------------|---------|-----------------|------------|
| connect | Connecting a buzzer pool failed | Error message or *null* | *null* |
| invalid_json | Parsing a message failed due to invalid json sent | *null* | The invalid message | 
| unknown_command | A unknown command was sent | *null* | The invalid message | 
| invalid_data_type | A message contained an invalid value | Error message | The invalid field |


