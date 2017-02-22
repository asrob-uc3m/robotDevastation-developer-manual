# Listening to Events
When a class needs to receive input events, such as keypresses, it must implement the `InputEventListener` interface. Once registered in the `InputManager`, it will receive input events each time the user generates them.

{% plantuml %}
interface InputEventListener {
bool onKeyDown(const RdKey & k)
bool onKeyUp(const RdKey & k)
bool onWindowEvent(const RdWindowEvent & event)
}

class MockupInputEventListener {
int getNumKeyDownPresses()
int getNumKeyUpPresses()
int getNumWindowEvents()

bool clear()

vector<RdKey> getStoredKeyUpPresses()
vector<RdKey> getStoredKeyDownPresses()
vector<RdWindowEvent> getStoredWindowEvents()
}
class RdKey
class RdWindowEvent
InputEventListener <|-- MockupInputEventListener
InputEventListener -- RdKey : receives
InputEventListener -- RdWindowEvent : receives
{% endplantuml %}

## InputEventListener
This interface has the following functions, that are called when the corresponding event is triggered in the `InputManager`:

* `onKeyDown()`: called when a key is pressed, the event passed stores the key that triggered the event.
* `onKeyUp()`: called when a key is released, the event passed stores the key that triggered the event.
* `onWindowEvent()`: called when a window event happens, the event passed stores the event type and information.


## MockupInputEventListener

Implements the following functions to extract information about received input events:

* `getNumKeyDownPresses()`: returns the number of key down events received.
* `getNumKeyUpPresses()`: returns the number of key up events received.
* `getNumWindowEvents()`: returns the number of window events received.
* `clear()`: clears all events received.
* `getStoredKeyUpPresses()`: returns a vector of key down events received.
* `getStoredKeyDownPresses()`: returns a vector of key up events received.
* `getStoredWindowEvents()`: returns a vector of window events received.



