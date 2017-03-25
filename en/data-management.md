# Data Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview
The data management system is based on the [*listener* design pattern](https://en.wikipedia.org/wiki/Observer_pattern), also called *observer pattern*. And does `<stuff>`.

{% plantuml %}
class MentalMap
interface NetworkEventListener
NetworkEventListener <|-- MentalMap

interface MentalMapEventListener
MentalMap -right- MentalMapEventListener : notifies >

package Data Model <<Rectangle>> {
class Player
class Target
class Weapon
}
{% endplantuml %}

