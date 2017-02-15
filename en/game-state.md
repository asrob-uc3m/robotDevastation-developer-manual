# Game State
Game State is where most of the game occurs. In this state you can control your robot to fight other robots.  When your health arrives to 0, you die and go to the DeadState.

{% plantuml %}
InitState -right-> GameState
state GameState {
state Setup : Connect with NetworkManager
state Setup : Connect with MentalMap
state Setup : Start video and audio
state Setup : Enable input
state Setup : Enable robot

state Loop : Get input events
state Loop : Update screen

state Cleanup: Stop managers when exit game
Setup -right-> Loop
Loop --> Loop
Loop -down-> Cleanup
}
Cleanup -right-> DeadState : health is 0
Cleanup --> [*] : exit requested
}
{% endplantuml %}

## Setup
In the Setup the game connects with the [NetworkManager](network-management.md) and the [MentalMap](data-management.md) to receive updates (e.g. your health has changed, some player has joined the game, some player died...).
It also starts the video and audio and enables both the user input and the robot controller.

## Loop

## Cleanup

## Transitions