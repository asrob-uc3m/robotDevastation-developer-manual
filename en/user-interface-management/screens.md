# Screen class
The `ScreenManager` class defines the interface required for managing the UI system in Robot Devastation. Other classes can then define the implementation of the `ScreenManager` according to, for instance, the library selected for displaying graphics on the screen.

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


The main methods of a `ScreenManager` are:

* `bool init()`
* `bool cleanup()`
* `bool drawScreen(void *screen)`
* `bool update(string parameter, string value)`
* `bool update(string parameter, Image value)`
* `bool update(string parameter, Player value)`
* `bool update(string parameter, vector<Player> value)` 
* `bool update(string parameter, vector<Target> value)` 
* `bool update(string parameter, Weapon value)` 
