# Network Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview
The network system is based on the [*listener* design pattern](https://en.wikipedia.org/wiki/Observer_pattern), also called *observer pattern*. The NetworkManager generates netowrk events whenever it receives new data from the server. These events store information about the data received, such as the status of the players currently in the game. Other objects, called *listeners* or *observers*, are subscribed to these events, and each time a event is generated, they receive a copy of the event.

