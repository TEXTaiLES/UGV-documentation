# UR5e Hardware Interfacing via RTDE: Setup Guide

<p style="text-align: justify;">
This guide outlines the initial configuration required to establish a high-frequency control loop between a workstation and a physical <b>UR5e robotic arm</b> using the <b>Real-Time Data Exchange (RTDE)</b> protocol. This setup is optimized for low-latency communication, essential for real-time control and data acquisition.
</p>

---

## 1. Robot Configuration (PolyScope)

To ensure a stable connection, the robot must have a dedicated static identity on the network.

1. **Navigate to:** `Settings` > `System` > `Network`
2. **IP Address:** `192.168.20.35`
3. **Subnet Mask:** `255.255.255.0`
4. **Remote Control:** Ensure that **Remote Control** is set to **Enabled** in the PolyScope settings to allow external commands.

---

## 2. Workstation Configuration (Laptop)

The host computer must reside on the same logical network to communicate with the robot.

* **Access Network Settings:** Navigate to `Wired Settings` > `IPv4`
* **Method:** `Manual`
* **Address:** `192.168.20.36`
* **Netmask:** `255.255.255.0`

## Connectivity Verification
Verify the physical layer connection and port accessibility via the terminal:

```
# Check physical connectivity
ping 192.168.20.35
```
```
# Scan specialized UR ports: 29999 (Dashboard) and 30004 (RTDE)
nmap -Pn -p 29999,30004 192.168.20.35
```
##  Testing and Control Scripts

Once the network configuration is complete, we can proceed to execute the following scripts to verify communication and control the arm.

### Script 1: Real-Time Data Acquisition (RTDE Receive)
This script uses the ur_rtde library to retrieve joint positions in real time. It is the ideal tool to confirm that we are receiving correct data from the controller.

```
python3 first_test.py
```

### Script 2: Precision Step Control (GUI via Tkinter)

The second script implements a graphical user interface (GUI) for incremental control of the UR5e. It uses direct TCP/IP sockets on port 30003 to send move commands.

```
python3 move.py
```
<p align="center">
  <img src="../../assets/6.gif" alt="Robot3" width="700"/>
</p>