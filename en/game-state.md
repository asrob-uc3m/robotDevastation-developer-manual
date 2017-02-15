# Game State

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

## Loop

## Cleanup

## Transitions