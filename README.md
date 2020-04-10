# How to convert opendrive to vector map 

## Setting up the environment

### download mrt_cmake_modules
cd ~/catkin_ws/src
git clone https://github.com/KIT-MRT/mrt_cmake_modules.git

### download autoware_map & vector_map_converter
cd ~
git clone https://gitlab.com/mitsudome-r/utilities.git
cd utilities
cp -R autoware_map ~/catkin_ws/src
cp -R vector_map_converter ~/catkin_ws/src

### download geographic_info
cd ~/catkin_ws/src
git clone https://github.com/ros-geographic-info/geographic_info.git

### download autoware_msgs
cd ~/catkin_ws/src
git clone https://gitee.com/autowarefoundation/messages.git

### download unique_identifier
cd ~/catkin_ws/src
git clone https://github.com/ros-geographic-info/unique_identifier.git

### download lanelet2
cd ~/catkin_ws/src
git clone https://github.com/fzi-forschungszentrum-informatik/lanelet2.git

### copy amathutils_lib
cd /home/your_lgsvl_path/Autoware/ros/src/common/libs
cp -R amathutils_lib ~/catkin_ws/src

### copy op_planner
cd /home/your_lgsvl_path/Autoware/ros/src/computing/planning/common/lib/openplanner
cp -R op_planner ~/catkin_ws/src

### copy autoware_build_flags
cd /home/your_lgsvl_path/Autoware/ros/src/common/cmake
cp -R autoware_build_flags ~/catkin_ws/src

### copy op_utility
cd /home/your_lgsvl_path/Autoware/ros/src/computing/planning/common/lib/openplanner
cp -R op_utility ~/catkin_ws/src

### copy vector_map
cd /home/your_lgsvl_path/Autoware/ros/src/data/packages
cp -R vector_map ~/catkin_ws/src

### copy vector_map_server
cd /home/your_lgsvl_path/Autoware/ros/src/data/packages
cp -R vector_map_server ~/catkin_ws/src

### if others packages not found, please use 
sudo apt-get install ros-kinetic-xxx

## Begin build [参考](https://www.ctolib.com/fzi-forschungszentrum-informatik-Lanelet2.html)
cd ~/catkin_ws
source /opt/ros/$ROS_DISTRO/setup.bash
catkin init
catkin config --cmake-args -DCMAKE_BUILD_TYPE=RelWithDebInfo # build in release mode (or whatever you prefer)
catkin build

### Afterwhile you while get autowaremap2vectormap & opendrive2autowaremap
source ~/catkin_ws/devel/setup.bash
cp ~/catkin_ws/devel/.private/vector_map_converter/lib/vector_map_converter/autowaremap2vectormap ~/catkin_ws/src/vector_map_converter
cp ~/catkin_ws/devel/.private/vector_map_converter/lib/vector_map_converter/opendrive2autowaremap ~/catkin_ws/src/vector_map_converter

## Convert map [参考](https://gitlab.com/mitsudome-r/utilities/-/tree/feature/vector_map_converter/vector_map_converter)
roscore&

### Use opendrive2autoware_converter
rosrun vector_map_converter opendrive2autowaremap _map_file:=[xodr file] _country_codes_dir:=~/catkin_ws/src/vector_map_converter/countries/ _save_dir:=[save directory] _resolution:=0.5 _keep_right:=[True/Flase]

### Use autowaremap2vectormap
rosrun vector_map_converter autowaremap2vectormap _map_dir:=[autowaremap directory] _save_dir:=[save directory] _create_whitelines:=[True/False] _wayareas_from_lanes:=[True/False]




