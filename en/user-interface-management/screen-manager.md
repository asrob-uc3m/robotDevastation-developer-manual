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


The main methods of the 

        bool update(string parameter, string value);
        virtual bool update(string parameter, Image value); //-- Required by GameScreen and DeadScreen
        virtual bool update(string parameter, Player value); //-- Required by GameScreen
        virtual bool update(string parameter, vector<Player> value); //-- Required by GameScreen
        virtual bool update(string parameter, vector<Target> value); //-- Required by GameScreen
        virtual bool update(std::string parameter, Weapon value); //-- Required by GameScreen


## SDLScreenManager




