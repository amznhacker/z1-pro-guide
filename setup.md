---
layout: default
---


# Requirements 
Any version above ubuntu 18.04 
Simulation currently works on ROS melodic and noetic (Todo: Port to ROS2 for simulation)

# Testing 


| Operating System | Version|
| ------ | ----------- |
| Ubuntu | 22.04 |

# Installing dependencies 

```
sudo apt install libboost-all-dev
sudo apt install libeigen3-dev
```


libeigen3-dev/jammy,jammy 3.4.0-2ubuntu2 all
  lightweight C++ template library for linear algebra


libboost-all-dev/jammy 1.74.0.3ubuntu7 amd64
  Boost C++ Libraries development files (ALL) (default version)

# Network configuration 
The default IP address of the robotics arm is 192.168.123.110. When connecting to a computer, the computer expects a router so we must run ifconfig to find the PC port 
