# Unitree Z1

---

## 0. System Prerequisites (Mandatory)

### Supported ROS Versions
- ROS Noetic (Ubuntu 20.04)
- ROS Melodic (Ubuntu 18.04)

### Install ros_control stack (Noetic)
```bash
sudo apt install \
  ros-noetic-controller-manager \
  ros-noetic-gazebo-ros-control \
  ros-noetic-joint-state-controller \
  ros-noetic-effort-controllers \
  ros-noetic-joint-trajectory-controller
```

## 1. Create and Build the ROS Workspace (Correct Way)

### Workspace Layout (Must Be Exact)
```
~/unitree_ws/
├── src/
│   ├── unitree_ros/
│   └── unitree_legged_msgs/
```

### Build Workspace
```bash
source /opt/ros/noetic/setup.bash
mkdir -p ~/unitree_ws/src
cd ~/unitree_ws/src
```

Place `unitree_ros` and `unitree_legged_msgs` here (clone or move folders).

#### Repositories
```bash
git clone https://github.com/unitreerobotics/unitree_ros.git
git clone https://github.com/unitreerobotics/unitree_ros_to_real.git
```

`unitree_legged_msgs` is found under `unitree_ros_to_real`.

```bash
cd ~/unitree_ws
catkin_make
```

❗ Do NOT modify `.bashrc` here.

### Activate Workspace
```bash
source ~/unitree_ws/devel/setup.bash
```

Verify:
```bash
rospack find unitree_gazebo
```

Launch Simulation:
```bash
roslaunch unitree_gazebo z1.launch
```

✔ If Gazebo opens and Z1 appears → ROS path is correct.

## 2. Configure Communication Mode (Important)

Edit file:
```
~/unitree_ws/src/unitree_ros/z1_controller/CMakeLists.txt
```

Choose ONE communication mode.

For Simulation (ROS):
```
set(COMMUNICATION ROS)
# set(COMMUNICATION UDP)
```

For Hardware / SDK Testing:
```
set(COMMUNICATION UDP)
# set(COMMUNICATION ROS)
```

❗ Only one must be active.

Rebuild workspace after changes:
```bash
cd ~/unitree_ws
catkin_make
```

### ③ Build z1_controller (Standalone SDK Test)
This is NOT ROS — this is SDK-level testing.

```bash
cd ~/unitree_ws/src/unitree_ros/z1_controller
mkdir -p build
cd build
cmake ..
make
```

Run:
```bash
./z1_ctrl
```

Keyboard mode:
```bash
./z1_ctrl k
```

Expected warning:
```
[WARNING] UDPPort::recv timeout
```

✔ Normal when no physical arm is connected.

### ④ Build and Test Z1 SDK
```bash
cd ~/unitree_ws/src/unitree_ros/z1_sdk
mkdir -p build
cd build
cmake ..
make
```

Run demo:
```bash
./highcmd_basic
```

Keyboard control (SDK):
- Press `2` → enter labeled state
- Press `0` → confirm
- Type `forward` → execute
- Press `~` → return home

Joint control mode activates automatically.

### ⑤ Environment Usage Rules (Non-Negotiable)

`.bashrc` should contain ONLY:
```bash
source /opt/ros/noetic/setup.bash
```

Activate Unitree workspace manually when needed:
```bash
source ~/unitree_ws/devel/setup.bash
```

Optional alias:
```bash
alias unitree='source ~/unitree_ws/devel/setup.bash'
```

🔬 Validation Checklist  
Run these after activation:
```bash
echo $ROS_DISTRO          # noetic
which roscore             # /opt/ros/noetic/bin/roscore
rospack find unitree_controller
```
