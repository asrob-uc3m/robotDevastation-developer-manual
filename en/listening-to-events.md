# Listening to Events
When a class needs to receive network events, such as be notified of data arrival, it must implement the `NetworkEventListener` interface. Once registered in the `NetworkManager`, it will receive network events each time the server generates them.

{% plantuml %}
interface NetworkEventListener {
bool onDataArrived(vector<RdPlayer> players)
}

class MockupNetworkEventListener {
int getDataArrived()
void resetDataArrived()
vector<RdPlayer> getStoredPlayers()
}

NetworkEventListener <|-- MockupNetworkEventListener
{% endplantuml %}

## NetworkEventListener
This interface has the following function, that is called when the corresponding event is triggered in the `NetworkManager`:

* `onDataArrived()`: called when the server sends player data.


## MockupNetworkEventListener
Implements the following functions to extract information about received network events:

* `getDataArrived()`: returns the amount of network events received.
* `resetDataArrived()`: resets the counter of network events received.
* `getStoredPlayers()`: returns the player data received in the most recent network event.




