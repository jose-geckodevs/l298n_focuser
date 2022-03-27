# Astroberry DIY
Astroberry DIY provides the INDI drivers for Raspberry Pi devices:
* Astroberry Focuser - stepper motor driver with absolute and relative position capabilities and autofocus with INDI client such as KStars and Ekos
* Astroberry Relays - relays switch board allowing for remote switching up to 4 devices
* Astroberry System - system parameters monitoring and system control

This driver has been adapted from Astroberry Focuser to support the L298N controller. Based on the following design:
https://www.electronicshub.org/raspberry-pi-l298n-interface-tutorial-control-dc-motor-l298n-raspberry-pi/


Features:
* L298N Focuser
  - Support for L298N DC controller
  - Direct stepper or DC motor control without proprietary drivers
  - Customizable GPIO pins
  - Absolute position control
  - Relative position control
  - Forward / Reverse direction configuration
  - Customizable maximum absolute position (steps)
  - Customizable maximum focuser travel (mm)
  - Resolution control from full step to 1/32 microsteps
  - Backlash compensation
  - Speed control
  - Focuser info including: critical focus zone in μm, step size in μm, steps per critical focus zone

# Source
https://github.com/jose-geckodevs/l298n_focuser

# Requirements
* INDI available here http://indilib.org/download.html
* CMake >= 2.4.7

# Installation
You need to compile the software from sources.

Download and install required libraries before compiling. See [INDI site](http://indilib.org/download.html) for more details.
In most cases it's enough to run:
```
sudo apt-get install cmake libindi-dev libgpiod-dev
```
Then you can compile the driver:
```
git clone https://github.com/jose-geckodevs/l298n_focuser
cd l298n_focuser
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=/usr ..
make
```
You can install the drivers by running:
```
sudo make install
```
OR manually installing files by running:
```
sudo copy indi_l298n_focuser /usr/bin/
sudo copy indi_l298n_relays /usr/bin/
sudo copy indi_l298n_system /usr/bin/
sudo copy indi_l298n_focuser.xml /usr/share/indi/
sudo copy indi_l298n_relays.xml /usr/share/indi/
sudo copy indi_l298n_system.xml /usr/share/indi/

```

