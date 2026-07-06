jsk_recognition
===============

jsk_recognition is a stack for the perception packages used in the JSK lab.

This branch (`ros2`) is the ROS 2 port. It currently provides the message
package that the rest of the JSK ROS 2 stack depends on.

## Packages

| Package | ROS 2 | Description |
|---|:---:|---|
| `jsk_recognition_msgs` | ✅ built | ROS 2 port of the messages / services / actions for jsk_pcl_ros and jsk_perception (76 msg, 24 srv, 2 action). Includes e.g. `BoundingBoxArray`, `PolygonArray`, `TorusArray`, `SegmentArray`, `HumanSkeletonArray`, `SimpleOccupancyGridArray`, `ClassificationResult`, `PeoplePoseArray`, which are used by `jsk_rviz_plugins`. |

The perception nodes/nodelets (`jsk_perception`, `jsk_pcl_ros`,
`jsk_pcl_ros_utils`, `resized_image_transport`, `jsk_recognition_utils`,
`checkerboard_detector`, `imagesift`) are **not ported in this branch**;
only the messages are provided so that dependent ROS 2 packages
(e.g. `jsk_visualization`) can build.

## Build

```bash
cd ~/ros2_ws
colcon build --packages-select jsk_recognition_msgs
source install/setup.bash
```

```bash
# list the generated interfaces
ros2 interface list | grep jsk_recognition_msgs
```

## Dependencies

`jsk_recognition_msgs` depends on `std_msgs`, `geometry_msgs`,
`sensor_msgs`, `pcl_msgs`, `builtin_interfaces`, `action_msgs` and
`jsk_footstep_msgs`.

## ROS 1 -> ROS 2 の主な変更点

- ビルドは `catkin` から `ament_cmake` + `rosidl`（`rosidl_interface_packages` グループ）に変更。
- ROS 1 の自動生成 README（`generate_readme.py`）・ReadTheDocs 連携・deb build status バッジは ROS 2 では使用しない（この README は手動管理）。
- 認識ノード群（jsk_perception / jsk_pcl_ros など）はこのブランチでは未移植で、メッセージのみを提供する。
