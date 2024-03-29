# installation guide SLAM REC-HV and dependencies on ROS Melodic and Ubuntu 18.04


## 1. ROS installation and dependencies.
```linux
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
sudo apt install ros-melodic-desktop-full
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
sudo apt install python-rosdep
sudo rosdep init
rosdep update
```

## 2. installation of python 3.6.
```linux
sudo apt update
sudo apt -y upgrade
sudo apt-get install python3-pip python3-yaml python3-dev
sudo pip3 install rospkg catkin_pkg rosdep rosinstall_generator rosinstall wstool vcstools catkin_tools
sudo apt-get install python3.6-dev
```
## 3. Virtual environment setup.
```linux
mkdir -p ~/python36_ws/src
cd ~/python36_ws
sudo apt install virtualenv
pip3 install --user virtualenv
virtualenv --python=/usr/bin/python3.6 py36env
cd
```
#### Activation virtual environment.
```linux
cd ~/python36_ws
source py36env/bin/activate
```

## 4. Setup Workspace.
```
cd
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
echo $ROS_PACKAGE_PATH
```
#### If everything is ok it should show this path “/home/youruser/catkin_ws/src:/opt/ros/melodic/share” ####

## 5. Install pip.
```linux
cd
sudo apt update
sudo apt install python3-pip
```
## 6. Install OPENNI.
```linux
sudo apt-get install ros-melodic-openni-camera
sudo apt-get install python-freenect
sudo apt-get update
```


## 7. Install OpenCV
```linux
sudo pip3 install scikit-build
sudo apt-get install python3-opencv
sudo pip3 install opencv-python
```
#### To test that the opencv was correctly installed do ####
```linux
python
import cv2 as cv
print(cv.__version__)
```
#### If it gives an error, execute the following again and try again ####
```linux
pip3 install opencv-python
```
## 8. Dependencies.
```linux
cd
pip install rospkg
pip3 install matplotlib
pip3 install openpyxl
pip3 install pandas
pip3 install seaborn
pip3 install sklearn
pip3 install scikit-learn
pip3 install open3d-python
git clone https://github.com/eric-wieser/ros_numpy.git
cd ros_numpy/
python setup.py install
cd
sudo apt-get install ros-melodic-openni-camera ros-melodic-openni-launch
```
## 9. Package installation.
#### Save what is at this address in the "src" folder of the project.
https://github.com/tjuan45/tf2

#### Then run in the terminal the following

```linux
cd
cd ~/catkin_ws
catkin_make
cd
cd ~/catkin_ws/src
git clone https://github.com/tjuan45/pointcloud_to_laserscan.git
cd
cd ~/catkin_ws
catkin_make
```

## 10. Creating a catkin Package rdslam2 for Rec-HV execution.
```linux
cd
cd ~/catkin_ws/src
catkin_create_pkg rdslam2 std_msgs rospy roscpp
cd
```
#### save and replace what is at this address in the project folder.
https://github.com/tjuan45/rdslam2

## 11. Build a catkin workspace and sourcing the setup file in ROS.
```linux
cd ~/catkin_ws
catkin_make
. ~/catkin_ws/devel/setup.bash
```
# Execution Rec_HV
#### now to run the code connect the Kinect sensors with adapter to USB type A.
#### and execute the following lines on a terminal.
```linux
cd
cd ~/python36_ws
source py36env/bin/activate
```
#### Launch Rec-HV.
```linux
cd
. ~/catkin_ws/devel/setup.bash
roslaunch rdslam2 Rec_HV_SegRec.launch
```
