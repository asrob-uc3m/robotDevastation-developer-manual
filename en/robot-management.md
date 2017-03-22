# Robot Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview
The robot system is in charge of communicating with the robot and sending commands to control its movement.

{% plantuml %}
interface RdRobotManager

Class RdMockupRobotManager
Class RdYarpRobotManager

RdRobotManager <|-- RdMockupRobotManager
RdRobotManager <|-- RdYarpRobotManager
{% endplantuml %}



