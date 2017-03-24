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
bool configure(string parameter, string value)
-- ImageManager API--
RdImage getImage()
}
{% endplantuml %}

The main methods of an `ImageManager` are: 
* `start()`, `stop()` and `isStopped()`: control the manager startup and halting.
* `addImageEventListener()`: registers a `ImageEventListener` that will be notified when new image events are received.
* `removeImageEventListeners()`: unsuscribes all the registered listeners, and they will not be notified until they are registered again.
* `configure()`: configures some parameters of the manager.

* `getImage()`: returns the last received image.


## YarpImageManager class
`YarpImageManager` is an implementation of the `ImageManager` interface using [YARP](http://www.yarp.it/) as communications middleware. It uses a `yarp::os::TypedReaderCallback<yarp::os::Bottle>` to receive images from the server and then notifies listeners that new images have arrived. 

## YarpLocalImageManager class
`YarpLocalImageManager` is an implementation of the `ImageManager` interface using [YARP](http://www.yarp.it/) as communications middleware. It can be used to obtain a video feed from a webcam attached to the local PC. It creates a yarp `opencv_grabber` to publish images from the webcam and uses a `yarp::os::TypedReaderCallback<yarp::os::Bottle>` to receive those images. It then notifies listeners that new images have arrived. 


## MockImageManager class
`MockImageManager` is an implementation of the `mageManager` for unit testing purposes.
It allows to emulate receiving images from the remote robot, which can be loaded from the local hard drive.


