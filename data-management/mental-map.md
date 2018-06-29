# Mental Map
The `MentalMap`, stores all the information related to the game elements, such as players, targets and weapons. When some of these elements change, for instance, after a player has been hit, it notifies all the `MentalMapEventListerners` subscribed with a new event.

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

* `getTargets()`: obtain the targets stored in the `MentalMap`.
* `getPlayers()`:  obtain the players stored in the `MentalMap`.
* `getTarget()`:  obtain a certain target stored in the `MentalMap`.
* `getPlayer()`: obtain a certain player stored in the `MentalMap`.
* `getMyself()`: Get the player corresponding to the user.


* `addWeapon(Weapon weapon)`: stores a new weapon on the `MentalMap`.
* `getCurrentWeapon()`: obtain the selected weapon.
* `shoot()`:  perform all the actions to be carried out when the user shoots (sound, update players, etc).
* `reload()`: perform all the actions to be carried out when the user reloads (sound, update weapons, etc).


* `updatePlayers()`: updates the players' data stored in the `MentalMap`. The current implementation just replaces the players inside the `MentalMap` by the new players received from the server.
* `updateTargets()`: update the targets stored in the `MentalMap`. If a target previously detected is no longer present in the new detections, decreases the belief value until reaching 0. Then, it deletes that target.
* `respawn()`: restores the health of current player (and does more stuff if needed).


* `addMentalMapEventListener()`: registers a `MentalMapEventListener` that will be notified when new image events are received.
* `removeMentalMapEventListeners()`: unsuscribes all the registered listeners, and they will not be notified until they are registered again.


* `onDataArrived()`: this function is called to notify the `MentalMap` that new data has arrived from the server and the stored data has to be updated.