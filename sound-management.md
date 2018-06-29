# Sound Management

```
This guide is focused on explaining the purpose behind each game module. 
For a detailed documentation of the methods and attributes of the classes, 
check the doxygen documentation.  
```

## System Overview
{% plantuml %}
interface AudioManager 

Class MockAudioManager {
 bool isPlaying(string id)
}

AudioManager <|-- MockAudioManager

AudioManager <|-- SDLAudioManager
{% endplantuml %}



## AudioManager class

The `AudioManager` class defines the interface required for managing the sound system in Robot Devastation. Other classes can then define the implementation of the AudioManager according to, for instance, the library selected for playing audio.

{% plantuml %}
interface AudioManager {
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

The main methods of an `AudioManager` are: 
* `start()`, `stop()` and `isStopped()`: control the manager startup and halting
* `load()`: loads a music file from a path and assigns it an id. The type, which can be either `MUSIC` or `FX` represents whether the sound is a long sound supposed to be game music or a short sound supposed to be a sound effect.
* `play()`: plays a loaded sound. The sound is selected by its id, and the number of loops it will be played can be specified.
* `stopMusic()`: stops all sounds being played.

## SDLAudioManager class
`SDLAudioManager` is an implementation of the `AudioManager` interface using SDL as audio backend. 

## MockAudioManager class
`MockAudioManager` is an implementation of the `AudioManager` for unit testing purposes.
It adds the method `isSoundPlaying()` to check whether or not a sound is currently being played. Note that this class mocks a real `AudioManager`, so it does not produce any actual sound.

{% plantuml %}
interface AudioManager 

Class MockAudioManager {
 bool isPlaying(string id)
}

AudioManager <|-- MockAudioManager
{% endplantuml %}
