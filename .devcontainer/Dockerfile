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
    && git config --global user.email youremail@email.com

# Install colcon auto-completion
RUN sudo apt update \
    && sudo apt install -y python3-pip \
    && pip install -U colcon-common-extensions \
    && echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc

# Install joint state publisher package for ROS
RUN sudo apt install ros-humble-joint-state-publisher
RUN sudo apt install ros-humble-joint-state-publisher-gui

# Rosdep update
RUN rosdep update

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc
RUN echo "source /ros2_ws/install/setup.bash" >> ~/.bashrc


ADD rosdep_pf_install.sh /
RUN sudo chmod +x /rosdep_pf_install.sh
CMD ["/rosdep_pf_install.sh"]

# RUN chmod +x /dev_container_humble/rosdep_pf_install.sh
# RUN /rosdep_pf_install.sh

# ENTRYPOINT ["bash", "rosdep_pf_install.sh"]
