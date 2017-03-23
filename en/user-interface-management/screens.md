# Screen class
The `Screen` class defines the interface required for a Robot Devastation in-game screen. Inheriting from this class allows the creation of different game screens. Currently, all implementations of game screens use SDL as graphics backend.

{% plantuml %}
interface Screen {
bool init()
bool cleanup()
bool drawScreen(void *screen)
bool update(string parameter, string value)
bool update(string parameter, Image value)
bool update(string parameter, Player value)
bool update(string parameter, vector<Player> value) 
bool update(string parameter, vector<Target> value) 
bool update(string parameter, Weapon value) 
}

{% endplantuml %}


The main methods of a `Screen` are:

* `init()`
* `cleanup()`
* `drawScreen(void *screen)`
* `update()`
* `bool update(string parameter, string value)`
* `bool update(string parameter, Image value)`
* `bool update(string parameter, Player value)`
* `bool update(string parameter, vector<Player> value)` 
* `bool update(string parameter, vector<Target> value)` 
* `bool update(string parameter, Weapon value)` 
