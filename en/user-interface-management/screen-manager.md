# ScreenManager

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




        bool update(string parameter, string value);
        virtual bool update(string parameter, Image value); //-- Required by GameScreen and DeadScreen
        virtual bool update(string parameter, Player value); //-- Required by GameScreen
        virtual bool update(string parameter, vector<Player> value); //-- Required by GameScreen
        virtual bool update(string parameter, vector<Target> value); //-- Required by GameScreen
        virtual bool update(std::string parameter, Weapon value); //-- Required by GameScreen


## SDLScreenManager




