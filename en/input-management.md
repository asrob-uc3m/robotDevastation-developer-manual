# Input Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```
## System Overview

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
{% endplantuml %}

## InputManager class

