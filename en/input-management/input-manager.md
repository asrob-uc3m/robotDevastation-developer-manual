## InputManager class
The `InputManager` class defines the interface required for managing the sound system in Robot Devastation. Other classes can then define the implementation of the AudioManager according to, for instance, the library selected for playing audio.

{% plantuml %}
interface InputManager {
--Startup & Halting--
bool start()
bool stop()
bool isStopped()
-- Configuration & Listeners --
bool addInputEventListener(RdInputEventListener * listener)
bool removeInputEventListeners()
}
{% endplantuml %}

The main methods of an `InputManager` are: 
* `start()`, `stop()` and `isStopped()`: control the manager startup and halting


## SDLInputManager class
`SDLAudioManager` is an implementation of the `InputManager` interface using SDL as input backend. 

## MockupInputManager class
`MockupInputManager` is an implementation of the `InputManager` for unit testing purposes.
It adds the method `isSoundPlaying()` to check whether or not a sound is currently being played. Note that this class mocks a real `InputManager`, so it does not produce any actual sound.



