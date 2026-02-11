## Minimal `.bashrc` Policy

For deterministic ROS behavior, `.bashrc` should contain only:

- System ROS sourcing
- Optional workspace activation alias

All legacy SDK paths and unused environment variables should be removed.

A minimal configuration:

```bash
source /opt/ros/noetic/setup.bash
alias unitree='source ~/unitree_ws/devel/setup.bash'
```

Workspaces must be activated explicitly using:

```
unitree
```
+
