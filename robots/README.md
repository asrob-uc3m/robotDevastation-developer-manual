# The Robots

![The Robots](/assets/the-robot.png)

Our current trend is to promote one repository per robot design. This enables robot developers to be the administrators of their own projects, while maintaining cleaner branches on main repositories. The repository that aims to act as a centralized hub that points to all the rest is [robotDevastation-robots](https://github.com/asrob-uc3m/robotDevastation-robots). Another relevant repository which will be mentioned in this chapter is [yarp-devices](https://github.com/asrob-uc3m/yarp-devices), which contains software we often reuse.

## Raspi-based robots
Many of our robots are based on Raspi, essentially because we need to move camera and motors via IP. In general, we use: OS (Raspbian Stretch Lite), camera via YARP `opencv_grabber` device to publish images via MJPEG protocol (or default YARP protocol as a fallback), and motors via our custom YARP devices at [yarp-devices](https://github.com/asrob-uc3m/yarp-devices).

### Prepare Raspi Peripherals
- Screen (HDMI)
- Keyboard (USB type A)
- Mouse (USB type A)
- Power supply (USB type micro-B)
- Network (ethernet or wifi)

### Install Raspbian Stretch Lite on Raspi
- Download Raspbian Stretch Lite image from https://www.raspberrypi.org/downloads/raspbian/
- Unzip and use plain `dd` as a copying mechanism to SD card as explained [here](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md):
```bash
dd bs=4M if=2019-04-08-raspbian-stretch-lite.img of=/dev/sdX # rename as required, e.g. /dev/mmcblk0
```
- Boot Raspi from SD card
- For keyboard layout, some alternatives:
    1. `sudo raspi-config` ([ref](https://raspberryparatorpes.net/empezando/raspi-config-configuracion-inicial-de-raspbian/)) > `4 Localisation Options` > `I3 Change Keyboard Layout`
    1. `sudo apt install console-data` and then `sudo loadkeys --verbose es`
- There are several methods to see your OS/distribution version ([ref](https://linuxize.com/post/how-to-check-your-ubuntu-version/)). Not all the files mentioned here may exist on a specific distribution, so `cat` may fail sometimes:
    1. `lsb_release -a`
    1. `lsb_release -d`
    1. `cat /etc/issue`
    1. `cat /etc/os-release`
    1. `cat /etc/debian_version`
    1. `cat /etc/lsb-release`
    1. `hostnamectl`
- Mandatory on Raspi 3B+: `sudo raspi-config` > `4 Localisation Options` > `I4 Change Wi-fi Country` > Set and accept rebooting
- To connect to a wireless network, some alternatives:
    1. Via `sudo raspi-config` (you do not need `/etc/network/interfaces`, as explained [here](https://apps-robots.uc3m.es/asrob/wiki/Tutorial_de_Redes))
    1. On the router side: assignment of IP based on MAC address
    1. Temporal via `sudo iwconfig wlan0 essid ASROB`, append `key password` to command if required
- To see pinout you can `sudo apt install python3-gpiozero` and then use `pinout` as explained [here](https://www.raspberrypi.org/documentation/usage/gpio/README.md)
- Enable `ssh` ([https://www.raspberrypi.org/documentation/remote-access/ssh/](https://www.raspberrypi.org/documentation/remote-access/ssh/)): `sudo raspi-config` > `5 Interfacing Options` > `P2 SSH` > `Yes`

### Install YARP on Raspbian Stretch Lite on Raspi
```bash
sudo apt update
sudo apt install git cmake
sudo apt install libjpeg8-dev  # Only required for mjpeg that should improve video comms
# opencv in fact replaces by libjpeg62-dev
sudo apt install --no-install-recommends libopencv-dev  # Only required for opencv_grabber
git clone https://github.com/robotology/yarp
mkdir yarp/build && cd yarp/build
cmake .. -DSKIP_ACE=ON
cmake .. -DENABLE_yarpcar_mjpeg=ON
cmake .. -DENABLE_yarpmod_opencv_grabber=ON
make -j$(nproc) # Compile
sudo make install
```

### Install yarp-devices on Raspbian Stretch Lite on Raspi
Documentation [here](https://github.com/asrob-uc3m/yarp-devices/blob/develop/doc/yarp-devices-install.md)

### Configure YARP devices as services on Raspi
Both camera and motors are set as `services` via `daemontools`.

1. Install `daemontools` ([more here](https://github.com/roboticslab-uc3m/installation-guides/blob/master/install-daemontools.md)):
```bash
apt-get install daemontools daemontools-run csh
```

2. Activate `daemontools` in `/etc/rc.local` through the line (before exit):
```bash
/bin/csh -cf '/usr/bin/svscanboot &'
```

3. Create the folder for services if it does not exist:
```bash
sudo mkdir -p /etc/service
```

4. Install the required `daemontools` services and `.ini` files used by them:
```bash
git clone https://github.com/asrob-uc3m/robotDevastation-robots
mkdir robotDevastation-robots/build  && cd robotDevastation-robots/build
cmake ..
make -j$(nproc) # Compile
sudo make install
```

5. Review your camera `.ini` files: Camera YARP device should be fine with `opencv_grabber`, the `robotDevastation-robots/share/launch/launchCamera.ini` should be installed at `/usr/local/share/robotDevastation-robots/contexts/launch/launchCamera.ini`.

6. Review your robot motor `.ini` files: the `robotDevastation-robots/share/launch/launchRobot.ini` should be installed at `/usr/local/share/robotDevastation-robots/contexts/launch/launchRobot.ini`. At least two possibilities here:
   1. Direct PWM to servo, such as [RD1](https://github.com/asrob-uc3m/rd1) and [RD2](https://github.com/asrob-uc3m/rd2): [RaspiOnePwmMotorController device](https://github.com/asrob-uc3m/yarp-devices/tree/develop/libraries/YarpPlugins/RaspiOnePwmMotorController) ([permalink](https://github.com/asrob-uc3m/yarp-devices/tree/0586c4a9d571f9959188486ca544deebbc2ddaa2/libraries/YarpPlugins/RaspiOnePwmMotorController))
   2. H-Bridge, such as [RD Ambassador](https://github.com/asrob-uc3m/rd-ambassador): [RaspiTwoPwmMotorController device](https://github.com/asrob-uc3m/yarp-devices/tree/develop/libraries/YarpPlugins/RaspiTwoPwmMotorController) ([permalink](https://github.com/asrob-uc3m/yarp-devices/tree/0586c4a9d571f9959188486ca544deebbc2ddaa2/libraries/YarpPlugins/RaspiTwoPwmMotorController))

7. Finally, remember to reboot for changes in `/etc/rc.local` to take effect.

## Arduino-based robots
Such is the case of [Laser Tower Of Death](https://github.com/asrob-uc3m/laser-tower-of-death). Relevant software:
- Camera on PC side: via `opencv_grabber`
- Motors on PC side: [yarp-devices/LaserTowerOfDeathController](https://github.com/asrob-uc3m/yarp-devices/tree/develop/libraries/YarpPlugins/LaserTowerOfDeathController)
- Motors on Arduino side: [arduinoServer](https://github.com/asrob-uc3m/yarp-devices/tree/develop/firmware/arduinoServer)
