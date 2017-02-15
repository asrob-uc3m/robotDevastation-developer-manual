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
{% endplantuml %}


## Setup
In the setup, this state shows the splash screen and starts the music, awaiting user input.

## Loop

## Cleanup

## Transitions