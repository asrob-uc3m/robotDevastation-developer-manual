# Data Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview

The data management system is based on the [*listener* design pattern](https://en.wikipedia.org/wiki/Observer_pattern), also called *observer pattern*. The main class of the data management system is the `MentalMap`, whose purpose is to store all the information related to the game elements, such as players, targets and weapons. When some of these elements change, for instance, after a player has been hit, it notifies all the `MentalMapEventListerners` subscribed with a new event.

{% plantuml %}
class MentalMap
interface NetworkEventListener
NetworkEventListener <|-- MentalMap

interface MentalMapEventListener
MentalMap -right- MentalMapEventListener : notifies >

package "Data Model" <<Rectangle>> {
class Player
class Target
class Weapon
}
{% endplantuml %}

