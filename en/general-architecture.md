# Robot Devastation Overview

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

SDLEventFactory  -- Key : creates
SDLEventFactory -- WindowEvent : creates
InputManager -- SDLEventFactory : uses
}

package NetworkManagement <<Rectangle>> {
interface NetworkManager
MentalMapEventListener <|-- NetworkManager
NetworkManager <|-- MockNetworkManager
NetworkManager <|-- YarpNetworkManager

interface NetworkEventListener
NetworkEventListener <|-- MockNetworkEventListener
}

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

class Hub
Hub o-- ImageManager
Hub o-- NetworkManager
Hub o-- MentalMap
Hub o-- AudioManager
Hub o-- InputManager
Hub o-- RobotManager
Hub o-- ScreenManager

Hub <|-- InitState
Hub <|-- GameState
Hub <|-- DeadState

State <|-- InitState
State <|-- GameState
State <|-- DeadState

{% endplantuml %}



## The Managers
The game functionality is encapsulated in different managers. Each manager is a [singleton](https://en.wikipedia.org/wiki/Singleton_pattern) as they are typically related to unique system or device[^1].

[^1] For a debate of wheter this was a good idea or not, see [issue #4](https://github.com/asrob-uc3m/robotDevastation/issues/4).