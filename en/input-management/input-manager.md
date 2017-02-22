## InputManager class

{% plantuml %}
interface InputManager {
--Startup & Halting--
bool start()
bool stop()
bool isStopped()
-- Configuration & Listeners --
bool addInputEventListener(RdInputEventListener * listener)
bool removeInputEventListeners()
}
{% endplantuml %}

The Input

