# Game FSM

The Game FSM, implemented in GameStateLib is the component in charge of controlling the game flow. Each state corresponds to a game state, and game conditions trigger the different transitions of the FSM. The implementation of the Game FSM uses the [Robot Devastion FSM class](FiniteStateMachine.md).

{% plantuml %}
[*] --> InitState
InitState -> GameState : press key
InitState --> [*] : exit game
GameState --> GameState
GameState --> DeadState : health is 0
GameState --> [*] : exit game
DeadState --> GameState :  respawn
DeadState --> [*] : exit game

note top of GameState
  Actual game occurs 
  mostly here
end note
{% endplantuml %}


There are three main states in Robot Devastation, each of them with different pre-state, state and post-state conditions:

 * [Init State](init-state.md): the game starts in this state, showing the initial splash screen. When user is ready, it logs in the player.
 * [Game State](game-state.md): main state of the game. Combats and robot movement happen in this state.
 * [Dead State](dead-state.md): you arrive to this state when you die, and remain there for a certain amount of time until you can be respawned into the game.

Each game state is a [Hub class](../general-architecture/ManagerHub.md), and has access to all the different managers present in Robot Devastation.
