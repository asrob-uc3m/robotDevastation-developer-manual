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

