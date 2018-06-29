# Dead State
When a player dies, he arrives to the DeadState. In this state a countdown is displayed. When the countdown arrives to 0 and the enter key is pressed, the player is respawned.

{% plantuml %}
GameState -down-> DeadState : health=0
state DeadState {
state Setup : Disable video
state Setup : Disable input
state Setup : Disable robot

state Loop : Display countdown

state Cleanup: Reset health
state Cleanup: OR
state Cleanup: Stop managers when exit game
Setup -right-> Loop
Loop --> Loop
Loop -down-> Cleanup
}
Cleanup -right-> GameState : respawn requested and counter=0
Cleanup --> [*] : exit requested
}
{% endplantuml %}

## Setup
The video, user input and the robot controller are disabled.

## Loop
The count is decremented from 10 to 0. When the counter arrives to 0, the user input is enabled and, if selected, the player is respawned to the GameState.

## Cleanup
If it arrived to this state after requesting exit, it disables all the involved managers.

Otherwise, it resets player's health before going back to the GameState.

## Transitions
If respawn is requested, the player is brought back to the GameState.

If exit is requested, it finishes the game.