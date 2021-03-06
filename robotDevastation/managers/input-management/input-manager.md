## InputManager class

The `InputManager` class defines the interface required for managing the input system in Robot Devastation. Other classes can then define the implementation of the InputManager according to, for instance, the library selected for reading user input.

{% plantuml %}
interface InputManager {
--Startup & Halting--
bool start()
bool stop()
bool isStopped()
-- Configuration & Listeners --
bool addInputEventListener(InputEventListener * listener)
bool removeInputEventListeners()
}
{% endplantuml %}

The main methods of an `InputManager` are: 
* `start()`, `stop()` and `isStopped()`: control the manager startup and halting.
* `addInputEventListener()`: registers a `InputEventListener` that will be notified when input events are generated by the user.
* `removeInputEventListeners()`: unsuscribes all the registered listeners, and they will not be notified until they are registered again.

## SDLInputManager class

`SDLInputManager` is an implementation of the `InputManager` interface using SDL as input backend. It sets a callback method that retrives SDL events and converts them to Robot Devastation input events. Currently only some key events and the exit cross on the game screen are supported as event generators.

## MockInputManager class

`MockInputManager` is an implementation of the `InputManager` for unit testing purposes.
It allows to generate input events from the testing code, without the need for a user. These events are generated from the following functions:
 
* `sendKeyPress()`: Generates a Key Down followed by a Key Up event of a given key.
* `sendKeyUp()`: Generates a Key Up event of a given key.
* `sendKeyDown()`: Generates a Key Down event of a given key.
* `sendWindowEvent()`: Generates a window event, such as closing the window.


{% plantuml %}
interface InputManager 
class MockInputManager {
bool sendKeyPress(const Key & key);
bool sendKeyUp(const Key & key);
bool sendKeyDown(const Key & key);
bool sendWindowEvent(const WindowEvent & event);
}

InputManager <|-- MockInputManager
{% endplantuml %}

## Dependency with other elements

As explained in the [Robot Devastation Overview](../overview.md) section, the following classes implement the `InputEventListener` interface to receive input events:
* [InitState](../init-state.md)
* [GameState](../game-state.md)
* [DeadState](../dead-state.md)
