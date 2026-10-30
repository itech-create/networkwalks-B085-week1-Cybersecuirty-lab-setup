<div align="center">

# 🛡️ Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
 <img src="https://img.shields.io/badge/Ogunleye%20Oluwasemilore-C00000?style=flat-square" />
</p>

---

## 🛡️ Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration testing laboratory** using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

---

## 🛡️ Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration testing laboratory** using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

---

⚠️ **Disclaimer:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## 🛡️ Lab Architecture

<img width="1109" height="494" alt="Screenshot 2026-08-10 234811" src="https://github.com/user-attachments/assets/8ce0edd8-f3e6-4e20-9e2e-83567f1a8c08" />



Additional target machines can be added to the same virtual network in future projects.

## 🛡️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------  |
| 🖥️ Host OS         | Windows 10         |
| 🧠 Host RAM        | 8 GB               |
| ⚡ Processor       | Intel Core i5      |
| 🧰 Hypervisor      | VirtualBox 7.2  |
| 🐉 Security OS     | Kali Linux 2026.2  |
| 🧠 Kali RAM        | 4096 MB            |
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | 10.0.0.0/24        |
| 🐧 Kali IP Address | 10.0.0.2/24        |
| 🚪 Default Gateway | 10.0.0.1           |
| 🌍 DNS Server      | 8.8.8.8            |
| 🔮 Future VM Range | 10.0.0.3–10.0.0.99 |

---

# 🛡️ Lab Setup Procedure

## Step 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

**Tool:** 7-Zip

---

## Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

---

## Step 3. Create the NAT Network
A dedicated NAT Network was created in VirtualBox.

Configuration:

Network Name: NatNetwork

IPv4 Prefix: 10.0.0.0/24

DHCP: Enabled

IPv6: Disabled

<img width="1366" height="768" alt="Screenshot (48)" src="create customNAT.PNG" />

![](2-screenshot-network-settings-1.png)

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.

---


## Step 4. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

```text
Adapter 1
Attached to: NAT Network
Network:     CustomNAT
Adapter Type: Intel PRO/1000 MT Desktop
```

The VM was allocated:

```text
RAM: 4096 MB
```
<img width="1366" height="691" alt="VirtualBox_kali-linux-2026 1-virtualbox-amd64_11_08_2026_00_06_50" src="configure VM to use NAT adapter.PNG" />

A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

<img width="1366" height="691" alt="VirtualBox_kali-linux-2026 1-virtualbox-amd64_11_08_2026_00_06_50" src="enable both features.PNG" />

---

## Step 5. Configure the Kali Linux Network

You also have the option to create and start the network with **VBoxManage**.

Open terminal on Linux/macOS.

**1. Create the network:**

```text
VBoxManage natnetwork add \
  --netname CustomNAT \
  --network "10.0.0.0/24" \
  --enable \
  --dhcp on
```

**2. Start the NAT Network service:**

```text
VBoxManage natnetwork start --netname CustomNAT
```

**3. Check the configuration:**

```text
VBoxManage list natnetworks
```

**4. Verify the network inside your VM**

Start the VM and check its assigned IP address.

For Linux:

```text
ip addr
ip route
```

For Windows:

```text
ipconfig
```

With DHCP enabled, your VM should receive an address in the **10.0.0.x** subnet, along with a gateway and DNS configuration. The exact gateway and DHCP range depend on the VirtualBox configuration.

Test internet connectivity:

```text
ping 8.8.8.8
```

Then test DNS resolution:

```text
ping google.com
```

If the first test works but the second fails, check the VM's DNS configuration.

**5. Configure the static IP in Kali:**

The following method uses NetworkManager, which is common on Kali Linux.

First, list your network connections:

```text
nmcli connection show
```

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

<img width="1366" height="691" alt="VirtualBox_kali-linux-2026 1-virtualbox-amd64_11_08_2026_00_42_50" src="https://github.com/user-attachments/assets/045ee1aa-9c4f-49f5-890b-f259752d235c" />

