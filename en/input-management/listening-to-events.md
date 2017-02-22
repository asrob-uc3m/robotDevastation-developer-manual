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

## InputEventListener



