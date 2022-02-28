FROM ros:melodic-ros-base-bionic

RUN apt update && apt install -y apt-utils curl gnupg

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'

RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

RUN apt install -y python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential

RUN apt-get update && apt-get install -y cmake git python3-flake8 python3-pip python3-pytest-cov  python3-setuptools \
  wget && rm -rf /var/lib/apt/lists/*

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && apt-get update && apt install -y ros-melodic-turtlesim"]

RUN apt update && apt install -y python3-colcon-common-extensions

RUN apt update && apt install -y libyaml-cpp-dev libboost-program-options-dev

RUN apt update && apt install -y libasio-dev libcurlpp-dev libcurl4-openssl-dev python3-sphinxcontrib.spelling doxygen && rm -rf /var/lib/apt/lists/*

RUN mkdir /root/is-workspace && cd /root/is-workspace && git clone https://github.com/eProsima/Integration-Service.git src/Integration-Service --recursive

RUN cd /root/is-workspace && git clone https://github.com/eProsima/ROS1-SH src/ROS1-SH

RUN cd /root/is-workspace && git clone https://github.com/eProsima/FIWARE-SH.git src/FIWARE-SH

RUN python3 -m pip install -U \
  pytest-repeat \
  pytest-rerunfailures \
  pytest \
  catkin_pkg \
  catkin_tools 

RUN mkdir /root/is-workspace/config

RUN ["/bin/bash", "-c", "cd /root/is-workspace && source /opt/ros/melodic/setup.bash && colcon build --cmake-args -DBIN_INSTALL_DIR=./install -Dcatkin_DIR=/opt/ros/melodic/share/catkin/cmake/  -DMIX_ROS_PACKAGES='turtlesim'"]

COPY config/config.yaml /root/is-workspace/config/config.yaml


