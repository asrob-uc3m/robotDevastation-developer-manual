# Creating Events
When a class, such as the `InputManager` needs to send input events, such as keypresses, it creates them using their constructor:

```cpp
RdKey k('A');
RdKey k2(RdKey::KEY_ARROW_UP);
``` 
must implement the `InputEventListener` interface. Once registered in the `InputManager`, it will receive input events each time the user generates them.

