# Network

## Network Protocol

YarpNetworkManager has two ports:
* A RPC Client: for login, logout and notifying the server that a robot has been hit.
* A Callback Port: for receiving updated player information from the server.

## Misc.
Configuration of the player data has to be performed **before** the network manager is started.
