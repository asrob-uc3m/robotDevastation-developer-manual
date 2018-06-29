# Overview

Robot Devastation is made of three fundamental components: 
* [**The Game**](/software.md): this component is in charge of running the game, processing the data received from the robots and commanding them with the user input. The code for the game software is in the [Main Repository (robotDevastation)](https://github.com/asrob-uc3m/robotDevastation).
* [**The Server**](/the-server.md): the main purpose of this component is sharing the information about the status of the different robots and reporting actions such as shooting a player. The code for the server software is also in the [Main Repository (robotDevastation)](https://github.com/asrob-uc3m/robotDevastation).
* [**The Robots**](/robots.md): the robots are a key element of Robot Devastation, as they act as a physical avatar for the players. Robot Devastation currently supports several robots out of the box, and more can be added. The corresponding section of this manual is intended for providing some guidelines and interfaces that the robots must implement to be able to play Robot Devastation. The sources for the robots (hardware, firmware and software) are linked from the dedicated [Robots Repository (robotDevastaion-robots)](https://github.com/asrob-uc3m/robotDevastation-robots).

These components are interconnected at different levels:
![The Robot <-> The Game <-> The Server](/assets/architecture-general.png)
