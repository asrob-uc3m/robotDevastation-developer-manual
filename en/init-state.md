# Init State

Init State is in charge of displaying the splash screen and log in the user.

{% plantuml %}
state GameState
state InitState {
state "Show Splash Screen" as ShowSplashScreen
ShowSplashScreen --> ShowSplashScreen
ShowSplashScreen --> Login : press key
Login --> GameState
}
ShowSplashScreen --> [*] : exit game

{% endplantuml %}


## Setup
In the setup, this state shows the splash screen and starts the music, awaiting user input.

## Loop
In the loop, it checks the input and refreshes the splash screen. 

If the user presses a key, it logs in the user in the server.

## Cleanup

In the cleanup, it stops the music and removes the input handlers installed for this state.

If it arrived to this state after requesting exit, it disables all the involved managers.

## Transitions
If user is logged in, it goes to the GameState.

If exit is requested, it finishes the game.