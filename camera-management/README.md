# Camera Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview

The camera management system is in charge of retrieving a video feed from the robot and process it to obtain the different game elements. It is based on the [*listener* design pattern](https://en.wikipedia.org/wiki/Observer_pattern), also called *observer pattern*. It is composed by a `ImageManager` that retrieves the images coming from the robot and generates an image event that is sent to the corresponding  `ImageEventListener`. The `ProcessorImageEventListener` receives the image from the camera feed and extracts from it the enemies detected, whose information is sent to the [MentalMap](/data-management/mental-map.md).

{% plantuml %}
interface ImageManager
ImageManager <|-- MockImageManager
ImageManager <|-- YarpImageManager
ImageManager <|-- YarpLocalImageManager

interface ImageEventListener
ImageEventListener <|-- MockImageEventListener
ImageEventListener <|-- ProcessorImageEventListener

ImageManager -right- ImageEventListener : notifies >
{% endplantuml %}

