# Creating Events
When a class, such as the `InputManager` needs to send input events, such as keypresses, it creates them using their constructor:

```cpp
RdKey k('A'); //-- Create a printable Key
RdKey k2(RdKey::KEY_ARROW_UP); //-- Create a control key
``` 

Some implementations, such as the SDL input backend, receive input events from SDL as SDL types (i.e. SDL_Keycode, SDL_WindowEvent). To create Robot Devastation input events from them, the `RdSDLEventFactory` can be used. It follows the [factory pattern](https://en.wikipedia.org/wiki/Factory_method_pattern), owning a table to convert from SDL types to the corresponding `RdKey`. 

{% plantuml %}

class RdSDLEventFactory {
RdKey makeKey(SDL_Keycode keycode)
RdWindowEvent makeWindowEvent(SDL_WindowEvent windowEvent)
}

RdSDLEventFactory -- RdKey : creates
RdSDLEventFactory -- RdWindowEvent : creates

{% endplantuml %}


Once created, they can be sent to the corresponding listeners, either manually o through the helper methods present in the `MockupInputManager`.
