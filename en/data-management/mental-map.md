# Mental Map

{% plantuml %}
class MentalMap {
-- Getters --
std::vector<Target> getTargets()
std::vector<Player> getPlayers()
Target getTarget(int id)
Player getPlayer(int id)
Player getMyself()

-- Listener API --
bool addMentalMapEventListener(MentalMapEventListener * listener)
bool removeMentalMapEventListeners()

-- Update data --
bool updatePlayers(vector<Player> new_player_vector)
bool updateTargets(vector<Target> new_target_detections)
bool respawn()

-- Weapon interface --
void addWeapon(Weapon weapon)
Weapon getCurrentWeapon()
bool shoot()
bool reload()

-- NetworkEventListener interface --
bool onDataArrived(vector<Player> players)
}
interface NetworkEventListener
NetworkEventListener <|-- MentalMap
{% endplantuml %}

The main members of this class are:

* `getTargets()`: 
* `getPlayers()`: 
* `getTarget()`: 
* `getPlayer()`: 
* `getMyself()`: Get the player corresponding to the user

* `addWeapon(Weapon weapon)`: 
* `getCurrentWeapon()`: 
* `shoot()`:  Manage all the actions to be carried out when the user shoots (sound, update players, etc)
* `reload()`: Manage all the actions to be carried out when the user reloads (sound, update weapons, etc)

* `updatePlayers()`: The current implementation just replaces the players inside the mental map by the new players
* `updateTargets(std::vector<Target> new_target_detections)`: Update the targets stored in the `MentalMap`. If a target previously detected is no longer present in the new detections, decreases the belief value until reaching 0. Then, it deletes that target.
* `respawn()`: Restores the health of current player (and does more stuff if needed)


* `addMentalMapEventListener( MentalMapEventListener * listener)`: Adds a MentalMapEventListener to the list of observers to be notified of events
* `removeMentalMapEventListeners()`: Unregisters all the MentalMapEventListener stored

* `onDataArrived()`: