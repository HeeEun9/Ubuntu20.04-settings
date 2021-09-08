## realsense ros wrapper install

sudo apt-get install ros-$ROS_DISTRO-realsense2-description


mkdir -p ~/realsense/src
cd ~/realsense/src

git clone https://github.com/IntelRealSense/realsense-ros.git
cd realsense-ros/
git checkout `git tag | sort -V | grep -P "^2.\d+\.\d+" | tail -1`
git clone https://github.com/pal-robotics/ddynamic_reconfigure.git 
cd ..



catkin_init_workspace
cd ..
catkin_make clean
catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release
catkin_make install


