# User Interface Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview
The User Interface (UI) system is in charge of displaying the different game screens and menus. It is composed of a single `ScreenManager`, which owns and shows different `Screen`s according to the current game state.

{% plantuml %}
interface ScreenManager
Class SDLScreenManager

ScreenManager <|-- SDLScreenManager

interface Screen
Screen <|-- InitScreen
Screen <|-- GameScreen
Screen <|-- DeadScreen
Screen <|-- MockScreen

ScreenManager -right- Screen : shows >
{% endplantuml %}

