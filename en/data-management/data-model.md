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

## Target class

{% plantuml %}
class Target {
    int player_id;
    Vector2d pos;
    Vector2d dimensions;
    int belief;
}
{% endplantuml %}

Attributes:
* `player_id`: Id of the player that is represented by this target.
* `pos` : Center of the box that bounds this target. 
* `dimensions`: Height and Width of the box that bounds this target.
* `belief`: Quantity representing how sure we are that this target can currently be seen by the user's robot.



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