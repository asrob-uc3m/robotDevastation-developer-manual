# Data Model

Robot Devastation's data model has three main elements:

* `Player`: represents each one of the human (or AI) players currently participating in the game. 
* `Target`: if a player's robot has been detected by our robot, it has a `Target` assigned. This `Target` stores information about the location and volume of the detected robot.
* `Weapon`: each player has (virtual) weapons installed on their robots. The `Weapon` stores the characteristics of each weapon.

## Player class

{% plantuml %}
class Player {
string name
int id
int health
int max_health
int team_id
int score
}
{% endplantuml %}

Attributes:
* `name`: Name of the player.
* `id`: Number identifying that player in the game.
* `health`: Current health of the player's robot.
* `max_health`: Maximum health of the player's robot.
* `team_id`: Number identifying the team the player's belongs to. (Note that team play has not been implemented yet).
* `score`: Current score of the player. (Note that currently the scoring system is not implemented).


## Target class
The `Target`class represents the location and perceived size of a enemy robot, and it is related to the player that controls that robot.

{% plantuml %}
class Target {
int player_id
Vector2d pos
Vector2d dimensions
int belief
}
{% endplantuml %}

Attributes:
* `player_id`: Id of the player that is represented by this target.
* `pos` : Center of the box that bounds this target. 
* `dimensions`: Height and Width of the box that bounds this target.
* `belief`: Quantity representing how sure we are that this target can currently be seen by the user's robot.

## Weapon class

The `Weapon` class represents a virtual weapon installed in the robot.

{% plantuml %}
class Weapon {
string name
int damage
int current_ammo
int max_ammo
}
{% endplantuml %}

Attributes:
* `name`: Weapon's name.
* `damage`: Damage that this weapon can inflict in one shot.
* `current_ammo`: Current ammount of ammo.
* `max_ammo`: Maximum ammount of ammo.

