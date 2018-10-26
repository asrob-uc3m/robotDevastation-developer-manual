# Overview

Robot Devastation is fundamentally programmed in C/C++, basically because we are close to hardware (wireless communications, webcams, motor drivers, etc). However, specifically for robot AI (at time of writing, see issue [robotDevastation-research#3](https://github.com/asrob-uc3m/robotDevastation-research/issues/3)), we can consider using a higher-level programming language such as Python.

For Robot Devastation development our current trend is on a native Ubuntu 16.04 partition, using Qt Creator as an IDE that can directly handle our CMake projects. For other best programming practices, [main-developer-tools](https://github.com/roboticslab-uc3m/developer-manual/blob/master/main-developer-tools.md) is a good entry point.

Robot Devastation is made of three fundamental components:
* [The Game (`robotDevastation`)](/robotDevastation/README.md): this component is in charge of running the game, processing the data received from the robots and commanding them with the user input. The code for the game software is in the [Main Repository (robotDevastation)](https://github.com/asrob-uc3m/robotDevastation).
* [The Server (`rdServer`)](/rdServer/README.md): the main purpose of this component is sharing the information about the status of the different robots and reporting actions such as shooting a player. The code for the server software is also in the [Main Repository (robotDevastation)](https://github.com/asrob-uc3m/robotDevastation).
* [The Robots (robotDevastation-robots)](/robots.md): the robots are a key element of Robot Devastation, as they act as physical avatars for the players. Robot Devastation currently supports several robots out of the box, and more can be added. The corresponding section of this manual is intended for providing some guidelines and interfaces that the robots must implement to plug into Robot Devastation. The sources for the robots (hardware, firmware and software) are linked from the dedicated [Robots Repository (robotDevastation-robots)](https://github.com/asrob-uc3m/robotDevastation-robots).

These three components are interconnected at different levels:

![The Robot <-> The Game <-> The Server](/assets/overview.png)
