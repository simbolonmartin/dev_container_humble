FROM osrf/ros:humble-desktop-full


# Add vscode user with same UID and GID as your host system
# (copied from https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user)
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
# Switch from root to user
USER $USERNAME

# Add user to video group to allow access to webcam
RUN sudo usermod --append --groups video $USERNAME

# Update all packages
RUN sudo apt update && sudo apt upgrade -y

# Install Git and add user ID
RUN sudo apt install -y git \
    && git config --global user.name "Your Name" \
    && git config --global user.email youremail@yourcompany.com

# Install colcon auto-completion and colcon_cd
RUN sudo apt update \
    && sudo apt install -y python3-pip \
    && pip install -U colcon-common-extensions \
    && echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc \
    && echo "export _colcon_cd_root=/opt/ros/humble/" >> ~/.bashrc \
    && echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc \

# Install packages for navigation
RUN sudo apt install ros-humble-joint-state-publisher
RUN sudo apt install ros-humble-joint-state-publisher-gui
RUN sudo apt install ros-humble-tf2-tools
RUN sudo apt install ros-humble-rmw-cyclonedds-cpp -y
RUN sudo apt install ros-humble-slam-toolbox -y
RUN sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup -y
RUN sudo apt install python3-pip -y \
    && pip3 install pyserial

# Rosdep update
RUN sudo apt-get update
RUN export ROS_DISTRO=humble
RUN rosdep update --include-eol-distros 

# Add several commands to bashrc
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc
RUN echo "source /dev_container_humble/install/setup.bash" >> ~/.bashrc
RUN echo "export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp" >> ~/.bashrc

