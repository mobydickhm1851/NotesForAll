# Rpi 4

## _Raspbian Buster_ together with _Kinetic_ 
- Official Tutorial of [Installing ROS Kinetic on the Raspberry Pi][Offi_ROS_Pi]
  - Bug 1: __libboost version__ error and [How to Fix It!][libboostFix] (During this fix, we need to [Change gcc default compile version][gccFix])
  - Bug 2: Failed to process __package 'qt_gui_cpp'__ and the [solution][solQT]


[Offi_ROS_Pi]:https://wiki.ros.org/ROSberryPi/Installing%20ROS%20Kinetic%20on%20the%20Raspberry%20Pi
[libboostFix]:https://answers.ros.org/question/327497/compiling-ros-on-raspberry-pi-4-with-buster-problem-with-libboost158/
[gccFix]:https://askubuntu.com/questions/26498/how-to-choose-the-default-gcc-and-g-version
[solQT]:https://github.com/ros-visualization/python_qt_binding/pull/59

## Installing some packages

### aruco_detect
#### Problems
1. **tf2_geometry_msgs** not installed </br>
  Go to [github page of tf2_geometry_msgs][github_tf2]

2. while installing **tf2_geometry_msgs**, **bullet package is not found** while installing `tf2_bullet`  </br>
  `sudo apt install libbullet-dev`

[github_tf2]:https://github.com/ros/geometry2.gitf2t




