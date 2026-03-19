# Wazuh_SocLab
This project demonstrates my Wazuh SIEM lab setup using an Ubuntu Server, a Windows 10 machine with Sysmon, and a Kali Linux VM to simulate attacks. It includes screenshots and analysis of how I detected and investigated suspicious activity.
## Attack Simulation

### Local Attack Simulation (Windows)

To simulate attacker behavior on a compromised system, I executed the following command on the Windows 10 endpoint:

net user attacker Password123 /add

### Purpose:
This simulates an attacker creating a new user account for persistence after gaining access to a system.

---

## Detection & Analysis

### Sysmon Detection (Process Creation)
- Process: net.exe → net1.exe
- Command:
  net user attacker Password123 /add

### Key Observations:
- The command execution was captured in Sysmon logs (Event ID 1)
- The parent process was identified as cmd.exe
- The activity was tied to user: DESKTOP-B0HARM5\natje

---

### Windows Security Logs
- Event ID 4738 → User account changed
- Event ID 4728 → User added to group

### Key Observations:
- New account created: attacker
- Action performed by: natje
- Security logs confirmed account modification

---

## MITRE ATT&CK Mapping

- T1087 → Account Discovery
- T1059.003 → Windows Command Shell
- T1098 → Account Manipulation

---

## Key Takeaway

This simulation demonstrates how attacker activity can be detected by correlating Sysmon process logs with Windows Security events. It shows how actions such as account creation can be traced from execution to system impact within a SIEM.
