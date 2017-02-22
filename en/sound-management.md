# Sound Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## AudioManager class

The `AudioManager` class defines the interface required for managing the sound system in Robot Devastation. Other classes can then define the implementation of the AudioManager according to, for instance, the library selected for playing audio.

{% plantuml %}
Class AudioManager {
    bool load(string music_filepath, string id, int type)
    bool play(string id, int loop=1)
    bool stopMusic()
    --Startup & Halting--
    bool start()
    bool stop()
    bool isStopped()
    --Constants--
    const int MUSIC
    const int FX
}
{% endplantuml %}