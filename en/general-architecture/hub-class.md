# HUB Class
```uml
@startuml

    Class Stage
    Class Timeout {
        +constructor:function(cfg)
        +timeout:function(ctx)
        +overdue:function(ctx)
        +stage: Stage
    }
    Stage <|-- Timeout
@enduml
```

As some classes, such as the game states, require require interfacing with all the managers to access their functionallity, the Hub abstract class was created. This class simplifies the code, as by simple inheritance any class can have simple access to all the required managers.