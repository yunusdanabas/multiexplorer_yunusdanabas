# multiexplorer_yunusdanabas

ROS package for multi-robot frontier exploration with TurtleBot3. Simulation-only (Gazebo + RViz).

My first ROS project, developed after a 2-week boot camp and 2 weeks of focused work at TÜBİTAK BİLGEM. Demonstrates single-, double-, and triple-robot autonomous exploration, SLAM, and map merging.

## Overview

Each robot:

1. Builds a local map with `gmapping`
2. Finds frontiers (boundaries between known and unknown space)
3. Sends navigation goals via `explore_lite` and `move_base`
4. Contributes to a global merged map via `multirobot_map_merge`

| Component | Implementation |
|-----------|----------------|
| Exploration | `explore_lite` (frontier detection + goal selection) |
| Navigation | `move_base` with DWA local planner |
| SLAM | `gmapping` (per robot) |
| Map merging | `multirobot_map_merge` (fuses `/tb3_i/map` into `/tb3/map`) |

## Prerequisites

- Ubuntu 20.04 / 22.04, ROS Melodic / Noetic
- TurtleBot3 packages, `move_base`, `explore_lite`, `multirobot_map_merge`

## Installation

```bash
cd ~/catkin_ws/src
git clone https://github.com/yunusdanabas/multiexplorer_yunusdanabas.git
cd ~/catkin_ws
rosdep install --from-paths src --ignore-src -r -y
catkin_make
source devel/setup.bash
```

## Quick Start

```bash
roslaunch multiexplorer_yunusdanabas single_robot_exp.launch   # 1 robot
roslaunch multiexplorer_yunusdanabas double_robotexp.launch    # 2 robots
roslaunch multiexplorer_yunusdanabas multi_robotexp.launch     # 3 robots
```

Pass `gui:=false` for headless runs.

## Launch Files

| File | Purpose |
|------|---------|
| `single_robot_exp.launch` | SLAM + exploration + navigation |
| `double_robotexp.launch` | Two robots + map merge |
| `multi_robotexp.launch` | Three robots + map merge |
| `multi_map_merge.launch` | Map merge only |
| `fiducial_slam_turtlebot3.launch` | Experimental ArUco-based SLAM |

## Resources

- [GitHub](https://github.com/yunusdanabas/multiexplorer_yunusdanabas)
- [Canva Slides](https://www.canva.com/design/DAGe6rFLM7U/w38mwYjYpvIZk73nA4x4lg/view)

## Acknowledgements

Developed during internship at TÜBİTAK BİLGEM (Robotics). MIT License.
