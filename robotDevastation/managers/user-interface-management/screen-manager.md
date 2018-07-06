# ScreenManager class

The `ScreenManager` class defines the interface required for managing the UI system in Robot Devastation. Other classes can then define the implementation of the `ScreenManager` according to, for instance, the library selected for displaying graphics on the screen.

{% plantuml %}
interface ScreenManager {
-- Starting & halting --
bool start()
bool stop()
bool isStopped()       
-- Configuration --
bool configure(string parameter, string value)
-- Manager API --
void setCurrentScreen(Screen* screen)
bool show()
-- Update API --
bool update(string parameter, Image value)
bool update(string parameter, Player value)
bool update(string parameter, vector<Target> value)
bool update(string parameter, Weapon value)
}

{% endplantuml %}


The main methods of a `ScreenManager` are:

* `start()`,  `stop()` and `isStopped()`: control the manager startup and halting.

* `configure()`: configure some UI parameters (e.g. to enable fullscreen mode).

* `setCurrentScreen()`: sets a `Screen` to be displayed.
* `show()`: display the currently selected `Screen`.

* `update()`: updates some UI aspect. Currently, several signatures are used as they are required by the corresponding `Screen`. An alternative implementation could use `void *` or templates to simplify the API, leaving a single `update()` method.

## SDLScreenManager class

`SDLScreenManager` is an implementation of the `ScreenManager` interface using SDL to display graphics.

### About the SDL graphics loop

To work properly, SDL requires that all SDL calls (for input, music, graphics, etc) must be performed in the same thread. Otherwise, thread-related exceptions and error start to appear. The typical loop of a SDL program is:

```
while not exit do
   read inputs
   process inputs, compute actions / consecuences
   process actions
   display / update graphics
```

Therefore, as `SDLScreenManager` uses SDL as graphics backend, one must be careful and ensure all the calls to `show()` occur in the same thread as the input is read.
