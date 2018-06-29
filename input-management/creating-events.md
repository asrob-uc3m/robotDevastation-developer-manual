# Creating Events

When a class, such as the `InputManager` needs to send input events, such as keypresses, it creates them using their constructor:

```cpp
Key k('A'); //-- Create a printable Key
Key k2(Key::KEY_ARROW_UP); //-- Create a control key
``` 

Some implementations, such as the SDL input backend, receive input events from SDL as SDL types (i.e. SDL_Keycode, SDL_WindowEvent). To create Robot Devastation input events from them, the `SDLEventFactory` can be used. It follows the [factory pattern](https://en.wikipedia.org/wiki/Factory_method_pattern), owning a table to convert from SDL types to the corresponding `Key`. 

{% plantuml %}

class SDLEventFactory {
Key makeKey(SDL_Keycode keycode)
WindowEvent makeWindowEvent(SDL_WindowEvent windowEvent)
}

SDLEventFactory -- Key : creates
SDLEventFactory -- WindowEvent : creates

{% endplantuml %}

Once created, they can be sent to the corresponding listeners, either manually o through the helper methods present in the `MockInputManager`.
