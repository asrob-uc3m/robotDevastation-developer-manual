# Listening to Events
When a class needs to receive events related to the stored game data, such as a player being hit, or respawned, it must implement the `MentalMapEventListener` interface. Once registered in the `MentalMap`, it will receive data-related events each time a change in the game data occurs.

{% plantuml %}
interface MentalMapEventListener {
bool onTargetHit(Target target, Player player, Weapon weapon)
bool onRespawn(Player player)
}
{% endplantuml %}

## MentalMapEventListener
This interface has the following functions, that are called when the corresponding event is triggered in the `MentalMap`:

* `onTargetHit()`: this function will be called whenever a target is hit.
* `onRespawn()`: this function will be called whenever the player is respawned.