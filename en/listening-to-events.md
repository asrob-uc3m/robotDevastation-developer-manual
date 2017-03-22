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

## InputEventListener
This interface has the following functions, that are called when the corresponding event is triggered in the `InputManager`:

* `onKeyDown()`: called when a key is pressed, the event passed stores the key that triggered the event.
* `onKeyUp()`: called when a key is released, the event passed stores the key that triggered the event.
* `onWindowEvent()`: called when a window event happens, the event passed stores the event type and information.


## MockupInputEventListener

Implements the following functions to extract information about received input events:

* `getNumKeyDownPresses()`: returns the number of key down events received.
* `getNumKeyUpPresses()`: returns the number of key up events received.
* `getNumWindowEvents()`: returns the number of window events received.
* `clear()`: clears all events received.
* `getStoredKeyUpPresses()`: returns a vector of key down events received.
* `getStoredKeyDownPresses()`: returns a vector of key up events received.
* `getStoredWindowEvents()`: returns a vector of window events received.



