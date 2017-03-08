# Creating Events
When a class, such as the `InputManager` needs to send input events, such as keypresses, it creates them using their constructor:

```cpp
RdKey k('A');
RdKey k2(RdKey::KEY_ARROW_UP);
``` 

Some implementations such as the SDL input backend, receive input events from SDL as SDL types (i.e. SDL_Keycode, SDL_WindowEvent). To create Robot Devastation input events from them, the `RdSDLEventFactory` can be used. It follows the [factory pattern](https://en.wikipedia.org/wiki/Factory_method_pattern).

{% plantuml %}

class RdSDLEventFactory {
RdKey makeKey(SDL_Keycode keycode)
RdWindowEvent makeWindowEvent(SDL_WindowEvent windowEvent)
}

RdSDLEventFactory -- RdKey : creates
RdSDLEventFactory -- RdWindowEvent : creates

{% endplantuml %}

must implement the `InputEventListener` interface. Once registered in the `InputManager`, it will receive input events each time the user generates them.

