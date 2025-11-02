# ASSIGNMENT_ARM3DOF_KEYPOINTS.md

**Title:** 3-DOF Robot Arm — Joint Position Control (no BLDC)  
**Scope:** Minimal arm model + position control to named poses in Gazebo Harmonic using ROS 2 Jazzy.  
**Style:** You figure out the details. Below are **key points** only.

---

## 1) Quick-Start: New ROS 2 Package Setup (CMake)

**Goal:** Create a fresh ROS 2 package using **ament_cmake** that holds your model, world, launch, and a Python control script.

### A) Create the package skeleton
```bash
# In your workspace
mkdir -p ~/arm_ws/src && cd ~/arm_ws/src
ros2 pkg create arm3dof --build-type ament_cmake --dependencies rclpy std_msgs
# Create folders you’ll need
cd arm3dof
mkdir -p models/arm3dof worlds launch src
```

### B) Minimal `CMakeLists.txt` (drop-in)
```cmake
cmake_minimum_required(VERSION 3.16)
project(arm3dof)

find_package(ament_cmake REQUIRED)
find_package(rclpy REQUIRED)
find_package(std_msgs REQUIRED)

# Install non-code assets (models/worlds/launch)
install(DIRECTORY
  models
  worlds
  launch
  DESTINATION share/${PROJECT_NAME}
)

# Install Python scripts as executables
install(PROGRAMS
  src/move_demo.py
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()
```

### C) Minimal `package.xml` (essentials)
```xml
<?xml version="1.0"?>
<package format="3">
  <name>arm3dof</name>
  <version>0.0.1</version>
  <description>3-DOF arm with joint position control in Gazebo.</description>
  <maintainer email="you@example.com">Your Name</maintainer>
  <license>MIT</license>

  <buildtool_depend>ament_cmake</buildtool_depend>
  <depend>rclpy</depend>
  <depend>std_msgs</depend>
  <!-- Needed at runtime to bridge ROS <-> Gazebo topics -->
  <exec_depend>ros_gz_bridge</exec_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```

### D) Make your Python script executable
```bash
chmod +x src/move_demo.py
```

### E) Build and source
```bash
cd ~/arm_ws
colcon build
source install/setup.bash
```

> **Tip:** Keep assets in-package (install via `share/${PROJECT_NAME}`) so fresh clones work without hard-coded paths.

---

## 2) Objectives (what you must achieve)
- Spawn a **3-DOF arm** (revolute joints: base yaw, shoulder, elbow) in Gazebo.
- Command **joint positions** from ROS 2 to move between at least **three named poses** (A→B→C).
- Keep motion stable (no oscillations, no joint explosions), with limits respected.

---

## 3) Modeling (SDF or URDF — your choice)
- **Links:** rectangular links with **sane inertias** (no zero/NaN; magnitudes consistent with mass/size).
- **Joints:**  
  - `j1_base_yaw`: axis **Z**  
  - `j2_shoulder`, `j3_elbow`: axis **Y** (planar elbow)  
  - **Limits:** reasonable ranges (e.g., ±π for yaw; about ±90° for shoulder/elbow).
- **Damping:** add small joint damping to avoid chatter.
- **Controller system:** attach a **Joint Position Controller** per joint (Harmonic).  
  - Expose **per-joint topics** for commands (clean namespace like `/arm/jX/cmd_pos`).  
  - Decide whether to use **velocity slewing** vs. PID (document your choice).

> **Deliverable:** `models/` (or `urdf/`) with your arm; short note explaining your axis/limit/inertia choices.

---

## 4) ROS ↔ Gazebo interfacing
- **Bridge the joint command topics:** ROS `std_msgs/Float64` ↔ Gazebo `gz.msgs.Double`.
- Keep topic names consistent; avoid hidden defaults.
- Show the **topic graph** you end up with (diagram or `rqt_graph` screenshot).

> **Deliverable:** brief config or command list + one diagram/screenshot.

---

## 5) Control node (you implement)
- Single ROS 2 node (Python or C++) that publishes **target angles** for all 3 joints.  
- **Poses:** define at least **A, B, C** (radians).  
- **Timing:** publish at fixed rate with brief holds; avoid instant discontinuities.
- Optional: tiny **ramp** to setpoints if you use strict position PID (reduces jerk).

> **Deliverable:** source file + minimal CLI (e.g., parameter `posture:=A`).

---

## 6) Runbook (you write it)
- From fresh clone to “arm is moving” in **clear, exact steps**.  
- Include **workspace layout**, build steps, and how you launch sim + bridge + control.

> **Deliverable:** `README.md` (short, exact, copy-paste-able).

---

## 7) Acceptance criteria (measured, not vibes)
- **Functionality:** A→B→C sequence completes without errors.
- **Stability:** each move settles in **≤ 1.0 s** with **≤ 5°** steady-state error per joint.
- **Safety:** joint limits never exceeded; no NaNs; clean shutdown (no spammy warnings).
- **Reproducibility:** your README steps work on a fresh machine.

---

## 8) Constraints (to ensure learning)
- **No BLDC plugin.** Use joint position control only.  
- Don’t paste ready-made models; **author the arm yourself** (credit any inspiration).  
- PID gains (if you use them) must be **justified** (1–2 sentences).

---

## 9) What to hand in
- Repo with: model, launch/world, control node, README.
- **One 15–30s GIF/video** showing A→B→C.
- **One diagram** of topics/pubs/subs.  
- **One paragraph**: design notes (axes, limits, controller choice, key tuning).

---

## 10) Hints (minimal)
- If it chatters: add damping, reduce P, or switch to velocity-slew mode.
- If commands don’t reach Gazebo: **type mismatch or wrong topic name** is the usual culprit.
- Start with small angles; scale up after stability is confirmed.

---

## 11) Stretch goals (optional, pick one)
- Add a simple **planar IK** for (x, y) to `j2/j3`; keep `j1` as yaw.
- Add a tiny GUI or RViz sliders to command joints.
- Log angles and compute **overshoot/settling** automatically.

---
