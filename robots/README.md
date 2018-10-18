# The Robots

![The Robots](/assets/the-robot.png)

Our current trend is to promote one repository per robot design. This enables robot developers to be the administrators of their own projects, while maintaining cleaner branches on main repositories. The repository that aims to act as a centralized hub that points to all the rest is [robotDevastation-robots](https://github.com/asrob-uc3m/robotDevastation-robots). Another relevant repository which will be mentioned in this chapter is [yarp-devices](https://github.com/asrob-uc3m/yarp-devices), which contains software we often reuse.

## Raspi-based robots
Many of our robots are based on Raspi, essentially because we need to move camera and motors via IP. In general, we use: OS (Raspbian Stretch Lite), camera via YARP `opencv_grabber` device to publish images via MJPEG protocol (or default YARP protocol as a fallback), and motors via our custom YARP devices at [yarp-devices](https://github.com/asrob-uc3m/yarp-devices).

### Install Raspbian Stretch Lite on Raspi
- Download Raspbian Stretch Lite image from https://www.raspberrypi.org/downloads/raspbian/
- Unzip and use plain `dd` as a copying mechanism to SD card
- Boot Raspi from SD card
- For keyboard layout, `apt install console-data` for `loadkeys --verbose es` (thanks https://superuser.com/questions/659247/installing-different-keyboard-layout-on-live-debian-image )
- Activate `ssh` as indicated in https://www.raspberrypi.org/documentation/remote-access/ssh/

### Install YARP on Raspbian Stretch Lite on Raspi
```bash
sudo apt install git cmake
sudo apt install libjpeg8-dev  # Only required for mjpeg that should improve video comms
# opencv in fact replaces by libjpeg62-dev
sudo apt install --no-install-recommends libopencv-dev  # Only required for opencv_grabber
git clone https://github.com/robotology/yarp
mkdir yarp/build && cd yarp/build
cmake .. -DSKIP_ACE=ON
cmake .. -DENABLE_yarpcar_mjpeg=ON
make -j4 # raspi 3 B
sudo make install
```

### Install yarp-devices on Raspbian Stretch Lite on Raspi
Documentation [here](https://github.com/asrob-uc3m/yarp-devices/blob/develop/doc/yarp-devices-install.md)

### Notes about devices on raspi
Both camera and motors are set as `services` via `daemontools` (done at [robotDevastation-robots#29](https://github.com/asrob-uc3m/robotDevastation-robots/issues/29)).
- [See old example guide (Spanish)](http://asrob.uc3m.es/index.php/C%C3%B3mo_configurar_el_arranque_del_software_de_RD1_sobre_Raspbian_7)
- Since services go in `/etc/service`, updated samples can be found in https://github.com/asrob-uc3m/robotDevastation-robots/tree/develop/scripts/etc/service

Regarding motor devices, two possibilities here:
1. Direct PWM to servo, such as [RD1](https://github.com/asrob-uc3m/rd1) and [RD2](https://github.com/asrob-uc3m/rd2): [RaspiOnePwmMotorController device](https://github.com/asrob-uc3m/yarp-devices/tree/develop/libraries/YarpPlugins/RaspiOnePwmMotorController) ([permalink](https://github.com/asrob-uc3m/yarp-devices/tree/0586c4a9d571f9959188486ca544deebbc2ddaa2/libraries/YarpPlugins/RaspiOnePwmMotorController))
2. H-Bridge, such as [RD Ambassador](https://github.com/asrob-uc3m/rd-ambassador): [RaspiTwoPwmMotorController device](https://github.com/asrob-uc3m/yarp-devices/tree/develop/libraries/YarpPlugins/RaspiTwoPwmMotorController) ([permalink](https://github.com/asrob-uc3m/yarp-devices/tree/0586c4a9d571f9959188486ca544deebbc2ddaa2/libraries/YarpPlugins/RaspiTwoPwmMotorController))


## Arduino-based robots
Such is the case of [Laser Tower Of Death](https://github.com/asrob-uc3m/laser-tower-of-death). Relevant software:
- Camera on PC side: via `opencv_grabber`
- Motors on PC side: [yarp-devices/LaserTowerOfDeathController](https://github.com/asrob-uc3m/yarp-devices/tree/develop/libraries/YarpPlugins/LaserTowerOfDeathController)
- Motors on Arduino side: [arduinoServer](https://github.com/asrob-uc3m/yarp-devices/tree/develop/firmware/arduinoServer)
