# Init State

Init State is in charge of displaying the splash screen and log in the user.

{% plantuml %}
state Configuring {
  [*] --> NewValueSelection
  NewValueSelection --> NewValuePreview : EvNewValue
  NewValuePreview --> NewValueSelection : EvNewValueRejected
  NewValuePreview --> NewValueSelection : EvNewValueSaved
  
  state NewValuePreview {
     State1 -> State2
  }
{% end plantuml %}


## Setup


## Loop

## Cleanup

## Transitions