# Robotics & Automation Projects

Three robotics and automation projects built during my **Robotics & Automation Internship at DecodeLabs** (Jun–Jul 2026): robot arm kinematics, autonomous navigation and vision-based quality inspection. Everything is written from scratch in Python, so the math is visible rather than hidden behind a framework.

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?logo=opencv&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C)

| # | Project | Problem | Core techniques |
|---|---|---|---|
| 1 | [6-DOF Robotic Arm Simulation](./6-DOF%20Robotic%20Arm%20Simulation) | Move an arm's end-effector from point A to point B without hitting an obstacle | DH forward kinematics, damped least squares IK, quintic trajectories, collision-aware waypoints |
| 2 | [Gear Inspection System](./Gear%20Inspection%20System) | Classify gears on a production line as PASS or FAIL | Thresholding, contours, convex hull defect analysis |
| 3 | [Autonomous Mobile Robot](./Autonomous%20Mobile%20Robot) | Navigate an unknown maze and recover when a new obstacle blocks the path | Simulated 360° LiDAR, occupancy grid mapping, A* planning, dynamic replanning |

---

## 1. 6-DOF Robotic Arm Simulation

<img src="./6-DOF%20Robotic%20Arm%20Simulation/arm_trajectory_result.png" width="600" alt="6-DOF arm trajectory">

- **Forward kinematics:** computes the end-effector pose from joint angles using Denavit-Hartenberg parameters.
- **Inverse kinematics:** a damped least squares numerical solver finds joint angles for a target while respecting joint limits.
- **Trajectory planning:** generates a smooth quintic trajectory. If the straight path intersects an obstacle, it routes through a safe waypoint instead.
- **Visualization:** a 3D Matplotlib animation of the arm's motion.

| File | Role |
|---|---|
| `forward_kinematics.py` | DH model and pose computation |
| `inverse_kinematics.py` | Damped least squares IK solver |
| `trajectory_planner.py` | Quintic trajectories and collision avoidance |
| `robotic_arm_sim.py` | Entry point and 3D simulation |

## 2. Gear Inspection System

<p>
<img src="./Gear%20Inspection%20System/part_02_OK.jpg" width="220" alt="Gear marked OK">
<img src="./Gear%20Inspection%20System/part_06_DEFECT.jpg" width="220" alt="Gear with defect">
</p>

1. **Preprocess:** grayscale, noise filtering and thresholding to separate the gear from the background.
2. **Detect:** contour and convex hull analysis measure structural irregularities such as broken teeth or cracks.
3. **Decide:** the defect measure is compared with a threshold. Parts under it PASS, the rest FAIL, and defects are highlighted on the image.

`generate_test_images.py` creates synthetic OK and DEFECT gear images, so the pipeline can be tested without a camera.

## 3. Autonomous Mobile Robot

<img src="./Autonomous%20Mobile%20Robot/navigation_result.png" width="600" alt="Robot navigation result">

- **Mapping:** a simulated 360° LiDAR scans the surroundings and updates a 2D occupancy grid as the robot moves.
- **Planning:** A* finds the shortest path to the goal on the current map.
- **Replanning:** when an unexpected obstacle appears, the robot rescans, updates the map and plans a new route.

| File | Role |
|---|---|
| `maze_environment.py` | Maze world and obstacles |
| `lidar_simulator.py` | 360° LiDAR ray casting |
| `astar_pathfinder.py` | A* search on the occupancy grid |
| `robot_navigation_sim.py` | Entry point: explore, plan, replan, plot |

---

## Getting started

```bash
git clone https://github.com/Hafsa-Anwar65/decodelabs-tasks.git
cd decodelabs-tasks
pip install numpy matplotlib opencv-python

# 1. Robotic arm
cd "6-DOF Robotic Arm Simulation" && python robotic_arm_sim.py && cd ..

# 2. Gear inspection
cd "Gear Inspection System" && python generate_test_images.py && python gear_inspection.py && cd ..

# 3. Mobile robot
cd "Autonomous Mobile Robot" && python robot_navigation_sim.py
```

## What's next

- Port the arm and mobile robot to **ROS 2**, with MoveIt for the arm and Nav2 + Gazebo for the mobile robot.
- Swap the gear inspection threshold for a small trained defect classifier and compare their accuracy.
- Move from position-only IK to full 6D pose control.

## Author

**Hafsa Anwar**, BS Robotics & Intelligence Systems, Bahria University Karachi
[Portfolio](https://hafsaanwar.dev) · [LinkedIn](https://www.linkedin.com/in/hafsa-anwar-53b251313/) · [GitHub](https://github.com/Hafsa-Anwar65)
