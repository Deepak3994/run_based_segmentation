
ROS
---
cmake_list
source /opt/ros/kinetic/setup.bash 
rosbag play -l example.bag 
rosrun 3D-groundplane groundplanfit
rosrun 3D-groundplane scanlinerun
rosrun rviz rviz -f velodyne
rostopic list
roscore
