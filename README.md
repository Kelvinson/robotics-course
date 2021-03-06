# MLR robotics course & practical robotics course

This repo is based on RAI code, including its python bindings. See https://github.com/MarcToussaint/rai for a README of the RAI code.

## Quick Start

This assumes a standard Ubuntu 16.04 machine.

WE DIDN'T GET TO RUN THIS WITH ANACONDA PYTHON. If you have Anaconda
installed, please remove it from the PATH in .bashrc. The setup below will
install the standard Ubuntu python3 and jupyter notebook.

In the ROBOTICS PRACTICAL course (where we use ROS), change 'ROS = 0' to '#ROS = 0' in 'config.mk' before compilation.

```
git clone https://github.com/MarcToussaint/robotics-course.git
cd robotics-course

git submodule init
git submodule update

make -j1 initUbuntuPackages  # calls sudo apt-get install; you can always interrupt
make -j4                     # builds libs and tests

source setupPython.sh

python3 -m pip install --upgrade pip
python3 -m pip install jupyter
python3 -m pip install matplotlib

jupyter-notebook docs/1-basics.ipynb 
```
After loading the pr2 and the kitchen (running first 3 cells in the notebook), the simulator window should look similar to:
![Alt text](screenshot.png?raw=true "Title")

## Updating after a pulling a new version

```
git submodule update
make -C rai dependAll
make -j4
```


## Tutorials
[Basics:](docs/1-basics.ipynb) Configurations, Features & Jacobians



# Practical Robotics information

## (Not So) Quick Start
* prerequisites: ROS, 
                 catkin_pkg/pyyaml/empy installed using 'pip install'
* generally, clone all git repos into $HOME/git
* clone
```
mkdir -p ~/git
cd ~/git
git clone https://github.com/MarcToussaint/robotics-course.git
cd robotics-course
```
* change `ROS = 0` to `#ROS = 0` in `config.mk` 
* install also baxter sources using
```
cd external
./installBaxterSources.sh
```
* then compile as described above (starting with `git submodule init...`)
* if using c++, install `qtcreator` as described here: https://github.com/MarcToussaint/rai-maintenance/blob/master/help/qtcreator.md
* when in the lab, connect to the wifi mlr-robolab (password: mlr-robolab)
* call `source bin/baxterwlansetup.sh` from ~/git/robotics-course
* source ROS and your workspace 
```
source /opt/ros/kinetic/setup.bash
source external/devel/setup.bash
```
* IF YOU'RE THE ONLY ONE USING BAXTER, turn on baxter and call `bin/baxterStart.sh`
* Try `rostopic list`
* Try
```
cd cpp/p1-baxterMini
make
./x.exe -useRos 1
```
* Before turning off baxter, run `rosrun baxter_tools tuck_arms.py -t`


## Details

### Booting

On the back of the robot near the pedestal base, there is a power button. Push it and wait for the machine to finish booting.

### Communicating with Baxter

Connect to the lab mlr-robolab WLAN (password: mlr-robolab)

Baxter runs with ROS, and you'll need to set your environment
variables to enable ROS communication. The easiest way to do this is
to connect to run one of following scripts in Terminal from the mlr
folder:

```
source bin/baxterwlansetup.sh
```

### Start-up

Call the start-up script, which enables baxter, untucks the arms,
turns off the ultrasonics (they click very loudly in any videos), and
calibrates the grippers.

```
bin/baxterStart.sh
```

### Shutdown

Always tuck the arms before shutting down, to keep the spring wear to a minimum.
```
bin/baxterTuck.sh
```
or
```
rosrun baxter_tools tuck_arms.py -t
```

Then press the power button once to turn the robot off.

Alternatively, you can ssh in to the robot (password: rethink) and run:
```
ssh ruser@thecount.local
sudo shutdown -h now
```
