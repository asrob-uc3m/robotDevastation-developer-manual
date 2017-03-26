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
NetworkManager <|-- MockNetworkManager
NetworkManager <|-- YarpNetworkManager

interface NetworkEventListener
NetworkEventListener <|-- MockNetworkEventListener
}

{% endplantuml %}



## The Managers
The game functionality is encapsulated in different managers. Each manager is a [singleton](https://en.wikipedia.org/wiki/Singleton_pattern) as they are typically related to unique system or device[^1].

[^1] For a debate of wheter this was a good idea or not, see [issue #4](https://github.com/asrob-uc3m/robotDevastation/issues/4).