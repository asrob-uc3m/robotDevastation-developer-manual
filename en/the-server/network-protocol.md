# Network Protocol

The Robot Devastaton server has two main communication channels:

* A broadcast channel, that periodically sends information about the logged in players to all the players.
* A [RPC server](https://en.wikipedia.org/wiki/Remote_procedure_call) that waits for commands. Players sent those commands to keep the server informed of all the game events.