# Input Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```
## System Overview
The input system is based on the [*listener* design pattern](https://en.wikipedia.org/wiki/Observer_pattern), also called *observer pattern*. The InputManager generates input events whenever the user interacts with Robot Devastation through the keyboard or UI. These events store information about the conditions that generated that event. For instance, key presses will generate key events, that will store the value of the key that generated them. Other objects, called *listeners* or *observers*, are subscribed to these events, and each time a event is generated, they receive a copy of the event.

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

RdSDLEventFactory  -- RdKey : creates
RdSDLEventFactory -- RdWindowEvent : creates
InputManager -- RdSDLEventFactory : uses

{% endplantuml %}



