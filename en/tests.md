# Tests

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

## testMockAudioManager
Automated test.

Checks that the mock AudioManager is able to emulate loading and playing sounds.

## testMockInputManager
Automated test.

Checks that the mock InputManager is able to emulate sending and receiving InputEvents from keyboard, window, etc.

## testMockNetworkManager
Automated test.

Checks that the mock NetworkManager is able to emulate login, logout, sending player info and sending network events. It also tests receiving updates from the MentalMap.

## testMockScreen
This test is not automated.

The test displays the MockScreen.

## testInputManager
This test is not automated.

Checks that the SDLInputManager is able to emulate sending and receiving InputEvents from keyboard.

Usage:
 * Arrow keys control the crossing point coordinates.
 * Espace shoots, emitting a sound.
 * Escape exits the test.
 
## testMockImageManager
Automated test.

Checks that the mock ImageManager is able to emulate sending and receiving images.

## testMockRobotManager
Automated test.

Checks that the mock RobotManager is able to emulate connecting to the robot and moving it.

## testProcessorImageEventListener
Automated test.

Checks that the ImageEventListener in charge of detecting robots on the image works correctly.

## testYarpImageManager
Automated test. This test requires an actual webcam connected to the PC in order to work.

Checks that the YarpImageManager grabs images from the webcam.

## testYarpNetworkManager
Automated test.

Checks that the YarpNetworkManager is able to perform login, logout, sending player info and sending network events. It also tests disconnection when no keep alive message is sent to server.

## testRobotDevastation
Automated test.

Checks the whole game flow, similar to the different game state tests.

## testSDLAudioManager
Automated test.

Checks that the SDLAudioManager is able to load and play sounds.

## testSDLScreenManager
This test is not automated.

Checks that the SDLScreenMananger is able to load and display Screens.

## testSDLTextDisplay
This test is not automated.

Simple test displaying some bars and text in a SDL window.
