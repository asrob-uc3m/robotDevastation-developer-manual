# Screen class

The `Screen` class defines the interface required for a Robot Devastation in-game screen. Inheriting from this class allows the creation of different game screens. Currently, all implementations of game screens use SDL as graphics backend.

{% plantuml %}
interface Screen {
bool init()
bool cleanup()
bool drawScreen(void *screen)
..Update API..
bool update(string parameter, string value)
bool update(string parameter, Image value)
bool update(string parameter, Player value)
bool update(string parameter, vector<Player> value) 
bool update(string parameter, vector<Target> value) 
bool update(string parameter, Weapon value) 
}

{% endplantuml %}

The main methods of a `Screen` are:

* `init()`: this method should be called before the `Screen` is set as current screen in the `ScreenManager`. It performs the resource loading and initialization.
* `cleanup()`: this method should be called to free all the resources reserved or loaded by the `Screen` before finishing the program.
* `drawScreen()`: performs all the required graphic operations to draw the screen graphical elements. A screen canvas is passed as argument to this method, whose type depends on the graphics backend being used.
* `update()`: updates the `Screen` contents after some displayed parameter has changed. Currently, several signatures are used as they are required by the corresponding `Screen`. An alternative implementation could use void * or templates to simplify the API, leaving a single `update()` method.

# Mock Screen class

Simple Screen for testing that shows a funny image with a custom message. This message can be configured through the `update()`method.

![](/assets/mockscreen.png)

# Init Screen class

`Screen` to be shown when the Robot Devastation game is started ([InitState](init-state.md)). It is just a splash screen showing the Robot Devastation logo.

![](/assets/initscreen.png)

# Game Screen class

This `Screen` is the main game screen. Shows the video stream of the robot's point of view. On top of it, the game HUD, including health, ammo and other players' info is drawn.

![](/assets/gamescreen.png)

# Dead Screen class

This `Screen is shown when the player dies. It shows the time the player has to wait until he is respawned.

![](/assets/deadscreen.png)
