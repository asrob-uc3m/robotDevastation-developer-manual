# Robot Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview

The robot system is in charge of communicating with the robot and sending commands to control its movement.

{% plantuml %}
interface RobotManager

Class MockRobotManager
Class YarpRobotManager

RobotManager <|-- MockRobotManager
RobotManager <|-- YarpRobotManager
{% endplantuml %}

## RobotManager class

The `RobotManager` class defines the interface required for communication with a Robot Devastation robot.

{% plantuml %}
interface RobotManager {
--Robot movement --    
bool moveForward(int velocity = UNUSED)
bool turnLeft(int velocity = UNUSED)
bool stopMovement()

--Robot camera movement --
bool tiltDown(int velocity = UNUSED)
bool panLeft(int velocity = UNUSED)
bool stopCameraMovement()

}
{% endplantuml %}

The main functions of a `RobotManager` are:
* `moveForward()`: command the robot to move forward at the specified velocity.
* `turnLeft()`: command the robot to turn left at the specified velocity.
* `stopMovement()`: command the robot to stop.


* `tiltDown()`: command the robot to move the camera down at the specified velocity.
* `panLeft()` : command the robot to move the camera to the left at the specified velocity.
* `stopCameraMovement()`: command the camera to stop moving.

## YarpRobotManager class

`YarpRobotManager` is an implementation of the `RobotManager` interface using [YARP](http://www.yarp.it/)  as middleware for communications with the robot.

## MockRobotManager class

`MockRobotManager` is an implementation of the `RobotManager` for unit testing purposes.

{% plantuml %}
interface RobotManager
class MockRobotManager {

--Robot status--
bool isConnected()
bool isEnabled()
--Robot movement--
bool isMoving()
int getMovementDirection()
const int FORWARD
const int BACKWARDS
const int LEFT
const int RIGHT
const int NONE
--Camera movement --
bool isCameraMoving()
int getCameraMovementDirection()
const int CAMERA_UP
const int CAMERA_DOWN
const int CAMERA_LEFT
const int CAMERA_RIGHT
const int CAMERA_NONE
}
RobotManager <|-- MockRobotManager
{% endplantuml %}


The `MockRobotManager` adds the following methods for testing:
* `isConnected()`: checks if the game is connected to the robot.
* `isEnabled()`: checks if the robot is enabled.


* `isMoving()`: check if the robot is moving.
* `getMovementDirection()`: returns the direction in which the robot is currently moving.


* `isCameraMoving()`: check is the camera is moving.
* `getCameraMovementDirection()`: returns the direction in which the camera is currently moving.
