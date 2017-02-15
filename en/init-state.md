# Init State

Init State is in charge of displaying the splash screen and log in the user.

{% plantuml %}
state GameState
state InitState {
state "Show Splash Screen"  as ShowSplashScreen
ShowSplashScreen --> ShowSplashScreen
ShowSplashScreen --> Login : press key
Login --> GameState 
}
{% end plantuml %}


## Setup


## Loop

## Cleanup

## Transitions