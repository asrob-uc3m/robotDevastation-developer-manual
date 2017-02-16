# Dead State
When a player dies, he arrives to the DeadState. In this state a countdown is displayed. When the countdown arrives to 0 and the enter key is pressed, the player is respawned.


## Setup
In Setup, the video, user input and the robot controller are disabled.

## Loop
In the Loop, the count is decremented from 10 to 0. When the counter arrives to 0, the user input is enabled and, if selected, the player is respawned to the GameState.

## Cleanup
If it arrived to this state after requesting exit, it disables all the involved managers.

Otherwise, it resets player's health before going back to the GameState.

## Transitions
If respawn is requested, the player is brought back to the GameState.

If exit is requested, it finishes the game.