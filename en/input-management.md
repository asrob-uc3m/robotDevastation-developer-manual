# Input Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```
## System Overview
The input system is based on the [listener design pattern](https://en.wikipedia.org/wiki/Observer_pattern), also called *observer pattern*. The InputManager generates input events whenever the user interacts with Robot Devastation through the keyboard or UI. These events store information about th e conditions that generated that event. For instance, key presses will store the value of the key that generated them.

{% plantuml %}
interface InputManager

Class MockupInputManager

InputManager <|-- MockupInputManager

InputManager <|-- SDLInputManager

interface InputEventListener

class MockupInputEventListener

InputEventListener <|-- MockupInputEventListener

class RdKey

class RdWindowEvent

class RdSDLEventFactory

RdSDLEventFactory -- RdKey : creates
RdSDLEventFactory -- RdWindowEvent : creates
{% endplantuml %}



