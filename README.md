# ROS 2 Humble Dev Container
![Build status](https://github.com/simbolonmartin/dev_container_humble/actions/workflows/docker-image.yml/badge.svg)

This dev container configuration installs the feature and packages below that are typically used for development.

## Image:  
- ROS Humble Desktop Full from the official OSRF page [here](https://hub.docker.com/layers/osrf/ros/humble-desktop-full/images/sha256-71ae08a6a0aae71a2f981e066c8a1d7dd76e956abf419c04626a0c746c3ebf4f).

## Feature:
- Light-weight Desktop from [here](https://github.com/devcontainers/features/tree/main/src/desktop-lite)

## Package installed:
- joint state publisher and joint state publisher GUI
- git user id
- pip installer, auto-complete colcon, and colcon_cd 
- python extension for vs code
- ros navigation tools (tf2-tools, slam-toolbox, nav2-bringup, navigation2)
