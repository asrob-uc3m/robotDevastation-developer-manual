# Data Model

Robot Devastation's data model has three main elements:

* `Player`: represents each one of the human (or AI) players currently participating in the game. 
* `Target`: if a player's robot has been detected by our robot, it has a `Target` assigned. This `Target` stores information about the location and volume of the detected robot.