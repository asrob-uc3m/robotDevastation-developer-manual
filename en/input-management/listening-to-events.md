# Listening to Events
When a class needs to receive input events, such as keypresses, it must implement the `InputEventListener` interface. Once registered in the `InputManager`, it will receive input events each time the user generates them.

{% plantuml %}
interface InputEventListener
class MockupInputEventListener
class RdKey
class RdWindowEvent
InputEventListener <|-- MockupInputEventListener
InputEventListener -- RdKey : receives
InputEventListener -- RdWindowEvent : receives
{% endplantuml %}



