# LINUX_ROS2_SETUP_GUIDE.md

## 0) Preparation
Open a terminal and run:
```bash
sudo apt update
sudo apt install -y git curl wget build-essential software-properties-common gnupg lsb-release
```

---

## 1) Linux Terminal Basics
Work through these two resources from start to finish:  
1. **Ubuntu Command Line for Beginners:**  
   https://ubuntu.com/tutorials/command-line-for-beginners#1-overview  
2. **Quick Reference Sheet (Cheat Sheet):**  
   https://gist.github.com/bradtraversy/cc180de0edee05075a6139e42d5f28ce  

**Minimum goal:**  
Be comfortable using the following commands:  
`ls`, `cd`, `pwd`, `mkdir`, `rm -rf`, `cp`, `mv`, `cat`, `less`, `nano`/`vim`, `grep`, `find`, `top`/`htop`, `ps`, `kill`, `chmod`/`chown`, and `apt`.

---

## 2) Visual Studio Code (for easier development)
Official installation guide:  
https://code.visualstudio.com/docs/setup/linux  

➡️ Click the `.deb` link at the top of the page → download → double-click to install.

**Recommended VS Code extensions:**  
- C/C++  
- Python  
- ROS (ms-iot.vscode-ros)  
- CMake Tools  
- XML  
- Markdown All in One  
- GitHub Pull Requests

---

## 3) ROS 2 Jazzy Installation
Official documentation:  
https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html  

**Required beginner tutorial:**  
https://docs.ros.org/en/jazzy/Tutorials/Beginner-CLI-Tools/Configuring-ROS2-Environment.html  

Complete the **Beginner CLI Tools** section — the others are optional for now.

---

## 4) Gazebo Installation + ROS–Gazebo Bridge
Official installation guide:  
https://gazebosim.org/docs/latest/install_ubuntu/  

Install the integrated ROS–Gazebo bridge:
```bash
sudo apt update
sudo apt install -y ros-jazzy-ros-gz
```

**Recommended Gazebo tutorials:**
- Building worlds and robots: https://gazebosim.org/docs/latest/building_robot/  
- Moving a robot: https://gazebosim.org/docs/latest/moving_robot/

**Quick test:**
```bash
# Open a sample world (you can also use examples from the docs)
gz sim -v 4
# In the opened GUI, select a sample world to load
```

---

## 5) GitHub Desktop (optional GUI)
Download page:  
https://github.com/shiftkey/desktop/releases/  

From the **Assets** section, download:  
`GitHubDesktop-linux-amd64-3.4.9-linux1.deb` → double-click to install.

---
