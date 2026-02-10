# Unitree Z1 

---

## ① Create and Build the ROS Workspace (Correct Way)

### Workspace Layout (Must Be Exact)

```
~/unitree_ws/
├── src/
│   ├── unitree_ros/
│   └── unitree_legged_msgs/
```

### Build Workspace

```
source /opt/ros/noetic/setup.bash
mkdir -p ~/unitree_ws/src
cd ~/unitree_ws/src
```

### Place unitree_ros and unitree_legged_msgs here (clone or move folders)
#### Repositories
```
git clone https://github.com/unitreerobotics/unitree_ros.git 

git clone https://github.com/unitreerobotics/unitree_ros_to_real.git
```
unitree_legged_msgs is found under unitree_ros_to_real

```
cd ~/unitree_ws
catkin_make
❗ Do NOT modify .bashrc here
```

### Activate Workspace 
```
source ~/unitree_ws/devel/setup.bash
```
Verify
```
rospack find unitree_gazebo
```
Launch Simulation
```
roslaunch unitree_gazebo z1.launch
```
✔ If Gazebo opens and Z1 appears → ROS path is correct

## ② Configure Communication Mode (Important)
Edit File
~/unitree_ws/src/unitree_ros/z1_controller/CMakeLists.txt
Choose ONE Communication Mode
For Simulation (ROS)
set(COMMUNICATION ROS)
# set(COMMUNICATION UDP)
For Hardware / SDK Testing
set(COMMUNICATION UDP)
# set(COMMUNICATION ROS)
❗ Only one must be active

Rebuild Workspace After Changes
cd ~/unitree_ws
catkin_make
③ Build z1_controller (Standalone SDK Test)
This is NOT ROS — this is SDK-level testing.

cd ~/unitree_ws/src/unitree_ros/z1_controller
mkdir -p build
cd build
cmake ..
make
Run
./z1_ctrl
Keyboard Mode
./z1_ctrl k
Expected Warning
[WARNING] UDPPort::recv timeout
✔ Normal when no physical arm is connected

④ Build and Test Z1 SDK
cd ~/unitree_ws/src/unitree_ros/z1_sdk
mkdir -p build
cd build
cmake ..
make
Run Demo
./highcmd_basic
Keyboard Control (SDK)
Press 2 → enter labeled state

Press 0 → confirm

Type forward → execute

Press ~ → return home

Joint control mode activates automatically.

⑤ Environment Usage Rules (Non-Negotiable)
.bashrc Should Contain ONLY
source /opt/ros/noetic/setup.bash
Activate Unitree Workspace Manually When Needed
source ~/unitree_ws/devel/setup.bash
Optional Alias
alias unitree='source ~/unitree_ws/devel/setup.bash'
🔬 Validation Checklist
Run these after activation:
```
echo $ROS_DISTRO          # noetic
which roscore             # /opt/ros/noetic/bin/roscore
rospack find unitree_controller
```

