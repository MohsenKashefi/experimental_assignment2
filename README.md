# experimenta_assignment2

# team members :

Mohammad Ali PourYaghoub shahkhali s6063201

Seyed Alireza mortaza s6136275

Reza Davoudi Beni s6115320

Pezhman Rezaei Salkhori s6133283

Mohsen Kashefi s5964796

## Description

This project integrates a ROSPlan-based planning system for a mobile robot equipped with a camera and laser scanner. Operating in a simulated Gazebo environment, the robot navigates predefined waypoints, detects ArUco markers, and moves to the waypoint containing the marker with the smallest ID

### Key Features

- **Waypoint Navigation**: The robot autonomously moves to predefined waypoints:
  - WP0: x = -7.0, y = 1.5
  - WP1: x = -3.0, y = -8.0
  - WP2: x = 6.0, y = 2.0
  - WP3: x = 7.0, y = -5.0
  - WP4 (initial position): x = 0, y = 2.75

- **Marker Detection**: Detects ArUco markers at waypoints and tracks the marker with the smallest ID.
- **ROSPlan Integration**: Uses PDDL-based planning for automated sequencing and execution of robot actions.

---
## Usage Instructions

1. Clone the repository into your ROS workspace:
   ```bash
   git clone https://github.com/MohsenKashefi/experimental_assignment2.git
   ```
2. Install necessary dependencies
  
3. Replace the `marker_publish.cpp` file in the `aruco_ros` package with the modified version provided in this repository.

4. install SLAM and ROSPlan
  
5. Follow the installation instructions for the ROSPlan dependencies as outlined in their repository.(also you can find in the aulaweb)

6. Launch the system:
   - Start the robot, Gazebo environment, SLAM, and MoveBase:
     ```bash
     roslaunch assignment2_exprob main.launch
     ```
   - Begin the planning process:
     ```bash
     roslaunch assignment2_exprob plan_sim.launch
     ```
   - Generate and dispatch the plan:
     ```bash
     rosservice call /rosplan_problem_interface/problem_generation_server

     rosservice call /rosplan_planner_interface/planning_server

     rosservice call /rosplan_parsing_interface/parse_plan

     rosservice call /rosplan_plan_dispatcher/dispatch_plan
     ```

7. To view the generated plan:
   ```bash
   rostopic echo /rosplan_planner_interface/planner_output -p
   ```

---

## Actions

The system defines three primary actions in the `Robot_Domain.pddl` file:

1. **move_to**: Moves the robot to a target waypoint using `MoveBase`.
2. **identify**: Rotates the robot at a waypoint to detect the ArUco marker. Updates the smallest ID and corresponding waypoint.
3. **verify_targets**: Ensures all markers are detected and navigates to the waypoint with the smallest marker ID.

---
## Package Details


### `my_rosplan_interface`
- **Action Dispatch**: Implements PDDL action dispatching via the `my_action` node:
  - **move_to**: Sends waypoint coordinates to MoveBase for navigation.
  - **identify**: Detects markers, updates the smallest ID, and aligns the marker in the image center.
  - **verify_targets**: Navigates to the waypoint with the smallest marker ID.

### `aruco_ros`
- Contains the modified `marker_publish.cpp` file for ArUco marker detection.
---

