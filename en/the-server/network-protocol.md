# Network Protocol

The Robot Devastation server has a very basic API to deal with all the current game events:

* `help`: returns all the commands available.
* `login`: logs in a player in the server.
* `logout`: logs out a player in the server.
* `hit`: applies damage to the health of the hit player.
* `respawn`: restores player's health after death.
* `keepAlive`: updates the belief of a player. Prevents the server from logging out that player due to inactivity.
