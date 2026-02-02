# Ansible Role: camera_ros

Builds and installs camera_ros with libcamera for Raspberry Pi cameras on ROS2.

This role builds the Raspberry Pi fork of libcamera (with imx500 support) and camera_ros together in a colcon workspace. This is necessary because Ubuntu 24.04 apt repositories don't include libcamera with full Raspberry Pi camera module support.

## Requirements

- ROS2 Jazzy already installed
- Raspberry Pi with camera module
- Ubuntu 24.04

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# ROS distribution
ROS_DISTRO: jazzy

# Workspace directory
camera_workspace_dir: "{{ ansible_env.HOME }}/camera_ws"

# Repository branches
libcamera_branch: jazzy
camera_ros_branch: jazzy

# Build configuration
build_type: release
enable_gstreamer: true
enable_pycamera: true

# Parallel build jobs (set to 1 for low-memory devices like Pi Zero)
build_jobs: auto
```

## Dependencies

This role requires ROS2 to be installed first (use `ansible-role-ros2`).

## Example Playbook

```yaml
- hosts: turtlebots
  roles:
    - ros2
    - camera_ros
```

## Testing

List available cameras:
```bash
ros2 run camera_ros camera_node --ros-args -p camera:=0
```

## License

MIT

## Author Information

Created for MXLab turtlebot deployment.
