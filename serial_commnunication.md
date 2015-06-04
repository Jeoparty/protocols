# Serial communication

## Handshake
The Arduino will reset itself upon establishing a serial connection. After the successfull reset the arduino will sent `00 42` followed by one byte indicating the protocol version (currently `00`). The mediator responds with `13 37`. The arduino should now send one byte containing the number of connected buzzers followed by a list of the ids of the connected buzzer (each one byte long).

## Opcodes

### 00 - Serial ready
**Sender** *arduino*  
**Payload length** *2*
Sent by the arduino after booting. It must be followed by `42` and one byte indicating the protocol version.

### 01 - Reset
**Sender** *both*  
TODO


### 02 - Ping
**Sender** *both*  
**Payload length** *0*  
The *ping* command can be sent at any time. A party receiving a ping must respond with a *pong* (03) within 100ms. If they fail to do so the party which sent the ping may disconnect or reset the connection.

**Payload** This command has no payload.

### 03 - Pong
**Sender** *both*  
**Payload length** *0*  
Upon receiving a *ping* (02) the receiving party must respond with a *pong* within 100ms.

**Payload** This command has no payload.

### 04 - Buzz
**Sender** *arduino*  
**Payload length** *1*  
This command is sent when one of the buzzers is hit.

**Payload** The ID of the buzzer hit

### 05 - Set color
**Sender** *mediator*  
**Payload length** *4*  
This command is sent to change the color of the buzzer LEDs.

**Payload** Payload contains of 4 bytes.

| field        | length | 
| ----------- | --------:|
| buzzerID |         1 |
| red          |         1 |
| green      |         1 |
| blue        |         1 |

### 06 - Connected
**Sender** *arduino*
**Payload length** *1*
Sent when a buzzer is connected

**Payload** The ID of the connected buzzer

### 06 - Disconnected
**Sender** *arduino*
**Payload length** *1*
Sent when a buzzer is disconnected

**Payload** The ID of the disconnected buzzer