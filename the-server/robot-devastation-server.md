# Robot Devastation Server

The Robot Devastation server manages the communications between robots and players, keeping track of players, scores, health levels, etc.

## Main loop

The main execution loop of the Robot devastation perform two tasks:

1. Broadcast player info through broadcast channel.
2. Decrease players' belief. If any player arrives to 0 belief, the server logs that 
player out the server.

## Server API

The Robot Devastation server has a very basic API to deal with all the current game events:

* `help`: returns all the commands available.
* `login`: logs in a player in the server.
* `logout`: logs out a player in the server.
* `hit`: applies damage to the health of the hit player.
* `respawn`: restores player's health after death.
* `keepAlive`: updates the belief of a player. Prevents the server from logging out that player due to inactivity.
