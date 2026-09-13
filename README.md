# 🤖 ROS 2 Autonomous Edge-Avoiding Robot

![ROS 2](https://img.shields.io/badge/ROS_2-Humble-blue.svg)
![Python](https://img.shields.io/badge/Python-3.10-blue)
![Simulation](https://img.shields.io/badge/Simulation-Gazebo-orange)

A complete ROS 2 (Humble) simulation package for an autonomous, differential-drive mobile robot. Built from scratch using URDF and Xacro, this robot operates in a Gazebo environment and utilizes a downward-facing LiDAR sensor to detect table edges (cliffs), ensuring it never falls off its platform.

## 🎥 Demo

<!-- 
=====================================================
[VIDEO PLACEHOLDER]
Drag and drop your .mp4 video file right here in the GitHub web editor!
=====================================================
-->

## 📋 Overview

The autonomous behavior is driven by a custom Python-based state machine node that continuously processes `/edge_scan` data. When a cliff is detected, the node seamlessly overrides standard forward velocity commands, executing a precisely timed reverse-and-turn recovery maneuver to ensure the robot remains safely on the table.

### ✨ Key Features
*   **Custom URDF/Xacro Design:** Modular robot modeling, including custom collision meshes and physical inertia tuning.
*   **ROS 2 Control Integration:** Hardware abstraction and differential drive controller (`diff_drive_controller`) integration.
*   **Single-Beam LiDAR Cliff Detection:** Clever utilization of a 90-degree pitched GPU LiDAR to monitor floor distance.
*   **Reactive State Machine:** Python-based node for processing sensor streams and publishing `geometry_msgs/Twist` commands.

## 🏗️ Project Architecture

The workspace is divided into four highly modular packages:
*   `bot_description`: Houses the physical robot model (URDF/Xacro), Gazebo world environments (`empty_table.world`), and RViz configurations.
*   `bot_controller`: Manages the `ros2_control` hardware interface and differential drive parameters.
*   `bot_bringup`: The master launch package that boots the simulation, spawns the robot, and starts the controllers in a single command.
*   `bot_script`: The "brain" of the robot, containing the Python node (`edge_detection.py`) that executes the autonomous roaming and edge-avoidance logic.

## 🛠️ Prerequisites

*   **OS:** Ubuntu 22.04 LTS
*   **ROS Distribution:** ROS 2 Humble
*   **Dependencies:**
    ```bash
    sudo apt update
    sudo apt install ros-humble-ros2-control ros-humble-ros2-controllers ros-humble-gazebo-ros2-control ros-humble-xacro
    ```

