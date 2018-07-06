# Processing the received images

As the images need to be processed to locate other players and detect them as targets, a `ProcessorImageEventListener` has been implemented.

## ProcessorImageEventListener

The `ProcessorImageEventListener` is notified each time a new image is obtained from the robot's camera, and processes the obtained image looking for targets.

Fancy methods could be used to detect other players, but to keep it simple, our current approach uses QR codes to identify players. 

After the location of targets has been obtained, the [MentalMap](data-management/mental-map.md) is notified of these changes.