# State Machine Library

## Main classes

The `robotDevastation` FSM is implementend in [StateMachineLib](https://asrob.uc3m.es/robotDevastation/group__StateMachineLib.html) has three main classes: [State](https://asrob.uc3m.es/robotDevastation/classrd_1_1State.html), [StateDirector](https://asrob.uc3m.es/robotDevastation/classrd_1_1StateDirector.html), and [FiniteStateMachine](https://asrob.uc3m.es/robotDevastation/classrd_1_1FiniteStateMachine.html).

<img src="/assets/StateMachine.svg" title="Class diagram" alt="Class diagram" width="800" />

### State

To create custom states, you mush inherit from the [State class](https://asrob.uc3m.es/robotDevastation/classrd_1_1State.html), and implement the corresponding members.

You must also specify an ID in the `state_id` internal string variable.

### StateDirector

Execution flow of the different states is controlled through a [StateDirector class](https://asrob.uc3m.es/robotDevastation/classrd_1_1StateDirector.html) attached to a State. It is not necessary to implement a custom StateDirector for a custom State, as the StateDirector just provides a method to control how States are executed and how transitions are performed.

When a StateDirector is started, it becomes the active StateDirector, and the associated State's setup() function is called. Then, it enters in the run loop, in which, periodically, the StateDirector executes the State's loop() method. After the loop() method is executed, the State's evaluateConditions() function is called, obtaining the id of the next state to be run. If the next state is not the current state, the current state is stopped and the next one is started.

### FiniteStateMachine

The [FiniteStateMachine class](https://asrob.uc3m.es/robotDevastation/classrd_1_1FiniteStateMachine.html) provides a nice interface to manipulate the StateMachine. States are added and configured and, then, the FiniteStateMachine is executed with the start() function. From that point, the FiniteStateMachine takes care of the execution flow and the deletion of the different states once the execution has finished.

To create a FiniteStateMachine, a [StateMachineBuilder class](https://asrob.uc3m.es/robotDevastation/classrd_1_1StateMachineBuilder.html) is typically used. More info about StateMachineBuilder in the examples section.

## Execution flow of the FiniteStateMachine

{% plantuml %}
state "setup()" as setup
state "loop()" as loop
state "cleanup()" as cleanup

[*] --> setup
setup --> loop
loop --> loop : evaluateConditions() not in transitions
loop --> cleanup : evaluateConditions() in transitions
cleanup --> [*] : (To next state / end)
{% endplantuml %}


## How to use it

This is a simple example to illustrate how to use the StateMachine.

Let us assume we are going to use the "MockState" to create a StateMachine. The fist step is to include all the required headers:

```cpp
#include "State.hpp"
#include "MockState.hpp"
#include "StateDirector.hpp"
#include "YarpStateDirector.hpp"
#include "StateMachine.hpp"
#include "StateMachineBuilder.hpp"
```

Then, we create the StateMachineBuilder that will help us configure the FSM:

```cpp
StateMachineBuilder builder;
```

We select the type of StateDirector to be "YARP", in order to use the YarpStateDirector:

```cpp
builder.setDirectorType("YARP");
```

Next step is to add the required states. When adding these states, the function will return us the id given to them. We must keep these ids in order to setup the transitions later.

```cpp
int state1_id = builder.addState(new MockState(1));
int state2_id = builder.addState(new MockState(2));
int state3_id = builder.addState(new MockState(3));
```

If the new() operator is used, the StateMachine will handle the object deletion using delete(). Otherwise we are in charge of deleting the dynamically allocated objects.

To setup the transitions, we use the ids previously obtained. The addTransition method takes three arguments: the source state, the destination state, and the value of evaluateConditions() that triggers that transition.

```cpp
builder.addTransition(state1_id, state2_id, 2);
builder.addTransition(state2_id, state1_id, 1);
builder.addTransition(state2_id, state3_id, 3);
builder.addTransition(state3_id, state1_id, 1);
```

Finally, we setup the initial state:

```cpp
builder.setInitialState(state1_id);
```

Once everything is configured, we call the buildStateMachine method to get our StateMachine:

```cpp
FiniteStateMachine * fsm = builder.buildStateMachine();
```

When we want to start the FiniteStateMachine, we use the start() method:

```cpp
fsm->start();
```

To stop the FiniteStateMachine we can call the stop method:

```cpp
fsm->stop();
```

To learn how to add an end state to finish the FSM flow, check out the next section.

## Adding an end state

An end state is equivalent to a StateDirector with a NULL state. When using the StateMachineBuilder, a special method can be used to add such state:

```cpp
int end_state_id = builder.addState(State::getEndState());
```

Then, we can use the obtained id to add a transition to this state:

```cpp
builder.addTransition(src_state_id, end_state_id, CONDITION)
```
