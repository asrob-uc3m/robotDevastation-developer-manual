## ImageManager class
The `ImageManager` class defines the interface required for receiving images from the robot.

{% plantuml %}
interface ImageManager {
--Startup & Halting--
bool start()
bool stop()
bool isStopped()
-- Configuration & Listeners --
bool addImageEventListener(InputEventListener * listener)
bool removeInputEventListeners()
}
{% endplantuml %}

The main methods of an `ImageManager` are: 
* `start()`, `stop()` and `isStopped()`: control the manager startup and halting.
* `addImageEventListener()`: registers a `ImageEventListener` that will be notified when new image events are received.
* `removeImageEventListeners()`: unsuscribes all the registered listeners, and they will not be notified until they are registered again.


## YarpNetworkManager class
`YarpNetworkManager` is an implementation of the `NetworkManager` interface using [YARP](http://www.yarp.it/) as communications middleware. It uses a `yarp::os::TypedReaderCallback<yarp::os::Bottle>` to receive data from the server and then notifies listeners that new data has arrived. It also owns a `yarp::os::RpcClient` to send data for login, logout and to notify the server that a robot has been hit.

A `yarp::os::RateThread` is used to send periodically a `keepAlive()` signal to the game server to avoid being logged out.

## MockNetworkManager class
`MockNetworkManager` is an implementation of the `NetworkManager` for unit testing purposes.
It allows to emulate connections with [The Server](the-server.md) without the actual server being executed. It also allows reading / writing data to the emulated game server to check , for instance, if the player is logged in or to set the game players.


