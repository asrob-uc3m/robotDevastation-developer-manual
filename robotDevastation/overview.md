# Overview

{% plantuml %}
package FSM <<Rectangle>> {
FiniteStateMachine o-- StateDirector
StateDirector *-- State
}

package SoundManagement <<Rectangle>> {
interface AudioManager
AudioManager <|-- SDLAudioManager
AudioManager <|-- MockAudioManager
}

package InputManagement <<Rectangle>> {
interface InputManager 
InputManager <|-- MockInputManager
InputManager <|-- SDLInputManager 

interface InputEventListener
InputEventListener <|-- MockInputEventListener

class Key
class WindowEvent
class SDLEventFactory

SDLEventFactory  -- Key : creates >
SDLEventFactory -- WindowEvent : creates >
InputManager -- SDLEventFactory : uses >
InputManager -- InputEventListener : notifies >
}

package NetworkManagement <<Rectangle>> {
interface NetworkManager
NetworkManager <|-- MockNetworkManager
NetworkManager <|-- YarpNetworkManager

interface NetworkEventListener
NetworkEventListener <|-- MockNetworkEventListener
NetworkManager -- NetworkEventListener : notifies >
}
MentalMapEventListener <|-- NetworkManager


package RobotManagement <<Rectangle>> {
interface RobotManager
RobotManager <|-- MockRobotManager
RobotManager <|-- YarpRobotManager
}

package "User Interface Management" <<Rectangle>> {
interface ScreenManager
ScreenManager <|-- SDLScreenManager

interface Screen
Screen <|-- InitScreen
Screen <|-- GameScreen
Screen <|-- DeadScreen
Screen <|-- MockScreen

ScreenManager -right- Screen : shows >
}

package "Camera Management" <<Rectangle>> {
interface ImageManager
ImageManager <|-- MockImageManager
ImageManager <|-- YarpImageManager
ImageManager <|-- YarpLocalImageManager

interface ImageEventListener
ImageEventListener <|-- MockImageEventListener
ImageEventListener <|-- ProcessorImageEventListener

ImageManager -right- ImageEventListener : notifies >
}

package "Data Management" <<Rectangle>> {
class MentalMap
interface NetworkEventListener
NetworkEventListener <|-- MentalMap

interface MentalMapEventListener
MentalMap -right- MentalMapEventListener : notifies >

package "Data Model" <<Rectangle>> {
class Player
class Target
class Weapon
}
}

class ManagerHub
ManagerHub-- ImageManager
ManagerHub o-- NetworkManager
ManagerHub o-- MentalMap
ManagerHub o-- AudioManager
ManagerHub o-- InputManager
ManagerHub o-- RobotManager
ManagerHub o-- ScreenManager

ManagerHub <|-- InitState
ManagerHub <|-- GameState
ManagerHub <|-- DeadState

State <|-- InitState
State <|-- GameState
State <|-- DeadState

ProcessorImageEventListener -- MentalMap : notifies >

InputEventListener <|-- InitState
InputEventListener <|-- GameState
InputEventListener <|-- DeadState

{% endplantuml %}

## The Game FSM
The game functionality is implemented as a [Finite State Machine (FSM)](../game-fsm/README.md). Each state of the FSM represents a game state. Each state is implemented as a [ManagerHub](ManagerHub.md), which allows the state to act upon the different game subsystems (user input, user interface, robot, etc).

The game first configures all the different managers. Then, all the different states are constructed and set in the FSM, which is started to run the game.

## The Game Managers
The game functionality is encapsulated in different managers. Each manager is currently implemented as a [singleton](https://en.wikipedia.org/wiki/Singleton_pattern), as they are typically related to unique system or device (for a debate of whether this was a good idea or not, see [robotDevastation#4](https://github.com/asrob-uc3m/robotDevastation/issues/4)).
