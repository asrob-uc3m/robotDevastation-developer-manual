# Tests
This section is currently under development...

## testDeadScreen
This test is not automated.

The test displays the DeadScreen with a countdown starting at 10.

## testDeadState
Automated test.

This test checks the transitions from DeadState to other states: DeadStateGoesToRespawn and DeadStateGoesToLogout. In each state it also checks the actions allowed by that state.

## testFSM
Automated test.

Checks that the FSM class works, creating an instance by hand (not using the builder) and then triggering the different conditions for each transition. Conditions are triggered using a YARP port.

## testFSMBuilder
Automated test.

Checks that the FSM class works, creating an instance using the Builder class and then triggering the different conditions for each transition. Conditions are triggered using a YARP port.

## testGameScreen
This test is not automated.

The test displays the GameScreen with different game elements (HUD, enemies, etc).

## testGameState
Automated test.

This test checks the transitions from GameState to other states. It also checks the different actions allowed in this State, such as moving the robot, shooting and dying.

## testInitScreen
This test is not automated.

The test displays the InitScreen.

## testInitState
Automated test.

This test checks the transitions from InitState to other states. It also checks the different actions allowed in this State, such as logging in and exiting the game.

## testMentalMap
Automated test.

Checks actions to be performed by the MentalMap, such as receiving and updating players from the server, shooting, reloading and respawning.

## testMockupAudioManager
Automated test.

Checks that the mock AudioMananger is able to emulate loading and playing sounds.

## testMockupInputManager
Automated test.

Checks that the mock InputMananger is able to emulate sending and receiving InputEvents from keyboard, window, etc.

## testMockupNetworkManager
Automated test.

Checks that the mock NetworkMananger is able to emulate login, logout, sending player info and sending network events. It also tests receiving updates from the MentalMap.

## testMockupScreen
This test is not automated.

The test displays the MockupScreen.

## testRdInputManager
This test is not automated.

Checks that the SDLInputMananger is able to emulate sending and receiving InputEvents from keyboard.

Usage:
 * Arrow keys control the crossing point coordinates.
 * Espace shoots, emitting a sound.
 * Escape exits the test.


## testRdYarpImageManager
This test requires an actual webcam connected to the pc in order to work.