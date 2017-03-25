# Listening to Events
When a class needs to receive image events, such as be notified of the arrival of a new image frame, it must implement the `ImageEventListener` interface. Once registered in the `ImageManager`, it will receive network events each time a new image is received.

{% plantuml %}
interface ImageEventListener {
bool onImageArrived(ImageManager * manager)
}

class MockImageEventListener {
int getImagesArrived()
void resetImagesArrived()
Image getStoredImage()
}

ImageEventListener <|-- MockImageEventListener
ImageEventListener <|-- ProcessImageEventListener

{% endplantuml %}

## ImageEventListener
This interface has the following function, that is called when the corresponding event is triggered in the `ImageManager`:

* `onImageArrived()`: called when a new image has arrived. The argument passed is not the new image, but the `ImageManager`that triggered the event. This way, the received image can be protected from being corrupted, as it cannot be overwritten while it is being read.


## MockImageEventListener
Implements the following functions to extract information about received network events:

* `getDataArrived()`: returns the amount of image events received.
* `resetDataArrived()`: resets the counter of image events received.
* `getStoredImage()`: returns the image received in the most recent image event.


## ProcessorImageEventListener 
