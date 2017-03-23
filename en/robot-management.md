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

## RdRobotManager class

The `RdRobotManager` class defines the interface required for communication with a Robot Devastation robot.

{% plantuml %}
interface RdRobotManager {
-- Robot movement  --    
bool moveForward(int velocity = UNUSED)
bool moveBackwards(int velocity = UNUSED)
bool turnLeft(int velocity = UNUSED)
bool turnRight(int velocity = UNUSED)
bool stopMovement()

-- Robot camera movement --
bool tiltUp(int velocity = UNUSED)
bool tiltDown(int velocity = UNUSED)
bool panLeft(int velocity = UNUSED)
bool panRight(int velocity = UNUSED)
bool stopCameraMovement()

-- Robot connection --
bool connect()
bool disconnect()
bool test()
void setEnabled(bool enabled)

}
{% endplantuml %}

The main functions of a `RdRobotManager` are:
* `moveForward()` 
* `moveBackwards()`
* `turnLeft()`
* `turnRight()`
* `stopMovement()`

* ``tiltUp()`
* tiltDown()`
* `panLeft()` 
* `panRight)`
* `stopCameraMovement()`

* `connect()`
* `disconnect()`
* `test()`
* `setEnabled()`


## RdYarpRobotManager class
`RdYarpRobotManager` is an implementation of the `RdRobotManager` interface using [YARP](http://www.yarp.it/)  as middleware for communications with the robot.

## RdMockupRobotManager class
`RdMockupRobotManager` is an implementation of the `RdRobotManager` for unit testing purposes.




