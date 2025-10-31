# 🐧 Ubuntu 24.04 Installation Guide (via VirtualBox)

This guide will help you **install Ubuntu 24.04** and set it up inside a **VirtualBox virtual machine**.  
Follow the steps carefully to get your system ready for development.

---

## Step 1. Download Ubuntu 24.04

1. Go to the official Ubuntu download page:  
   👉 https://ubuntu.com/download/server/arm
2. Click **“Download Ubuntu Desktop 24.04 LTS”**.
3. Save the `.iso` file to your computer — you’ll need it in the next step.

---

## Step 2. Install Ubuntu on VirtualBox

1. Open the VirtualBox setup tutorial:  
   👉 [https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)
2. Follow each section in the guide carefully:
   - **Step 1:** Overview  
   - **Step 2:** Install VirtualBox
   - Rest is not compitable with ARM so go to the next steps

# 🟣 Install Default GNOME Desktop on Ubuntu Server

This guide explains how to convert your **Ubuntu Server (ARM or x86)** into a full **Ubuntu Desktop (GNOME)** environment.  
It works for both VirtualBox and Parallels installations.

---

## 🧩 Step 1. Update and Upgrade Your System

Make sure all existing packages are current:

```bash
sudo apt update && sudo apt upgrade -y
sudo reboot
```

---

## 💻 Step 2. Install Ubuntu Desktop (GNOME)

Install the full Ubuntu Desktop environment:

```bash
sudo apt install ubuntu-desktop -y
```

> ⚠️ This may take a while — it downloads several GB of packages (the full GNOME environment and dependencies).

---

## 🔁 Step 3. Reboot After Installation

Once installation is complete, reboot your system:

```bash
sudo reboot
```

---

## 🖥️ Step 4. Boot into the Graphical Interface

After rebooting, you should see the **Ubuntu login screen** (GNOME Display Manager).  
Log in with your username and password to enter the graphical desktop.

If the system still boots into the command line, set the default target to graphical mode:

```bash
sudo systemctl set-default graphical.target
sudo reboot
```

---

## ⚙️ Step 5. (Optional) Install Parallels Tools

If you’re using **Parallels Desktop (ARM)**, install Parallels Tools to enable:
- Clipboard sharing (copy/paste between macOS and Ubuntu)  
- Drag & drop  
- Screen resizing  

### Option A — Menubar Installation

```
Menubar → Actions → Install Parallels Tools
```

### Option B — Terminal Installation

```bash
cd /media/USERNAME/Parallels\ Tools
sudo ./install
sudo reboot
```

---

## 🌐 Step 6. (Optional) Install Extra Utilities

Once inside the GNOME desktop, install common applications:

```bash
sudo apt install firefox gnome-terminal gedit nautilus -y
```

---

## ✅ Step 7. Finished!

You now have a fully functional **Ubuntu Desktop (GNOME)** running on your server installation — identical to Ubuntu 24.04 Desktop Edition.

---

*Author: Emre Can Eker*  
*Last updated: October 2025*
