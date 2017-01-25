# Game FSM

The Game FSM, implemented in GameStateLib is the component in charge of controlling the game flow. Each state corresponds to a game state, and game conditions trigger the different transitions of the FSM.

Each game state is a [Hub class](general-architecture/hub-class.md), and has access to all the different managers present in Robot Devastation.