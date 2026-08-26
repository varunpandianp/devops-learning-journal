# 🧩 Fixing “No Internet / Network Unreachable” in CentOS Stream 10 (VirtualBox)

### 📌 Problem

After installing **CentOS Stream 10** on **Oracle VirtualBox**, the VM could not connect to the internet.

**Symptoms observed:**
- `ping 8.8.8.8` → `Network is unreachable`
- `curl` / `yum update` → `Could not resolve host: mirrors.centos.org`
- `ip a` showed only:
127.0.0.1 (loopback only)
enp0s3 UP but no inet address

yaml
Copy code

The network adapter existed but had **no IP address**, meaning it never received one from DHCP.

---

## 🧠 Root Cause

CentOS uses **NetworkManager** to manage all network interfaces.  
In this VM:
- The interface `enp0s3` (VirtualBox default network adapter) was detected,
- But it was not connected or managed by NetworkManager,
- Hence, no DHCP request was sent → no IP assigned → no route to the internet.

---

## ✅ Solution — Commands Used

Run the following three commands inside your CentOS VM terminal:

```bash
# 1️⃣ Restart NetworkManager service
sudo systemctl restart NetworkManager

# 2️⃣ Connect the Ethernet interface manually
sudo nmcli device connect enp0s3

# 3️⃣ Bring the connection profile up (activate it)
sudo nmcli connection up enp0s3
🧩 Command Explanations
1️⃣ sudo systemctl restart NetworkManager
Restarts the NetworkManager daemon (service).

NetworkManager manages all wired/wireless interfaces and DHCP.

Restarting it forces a re-detection of network hardware and reinitializes connections.

Why it helps:
After VM setup or changing VirtualBox network modes (NAT ↔ Bridged), NetworkManager might not automatically re-detect the adapter. Restarting it ensures the service is running and managing interfaces correctly.

2️⃣ sudo nmcli device connect enp0s3
Uses nmcli (NetworkManager Command Line Interface).

“Connect” tells NetworkManager to attach and manage the physical device (enp0s3).

If the device is disconnected, this command triggers it to request a DHCP lease.

Why it helps:
It activates the physical NIC and initiates a DHCP request to get an IP from VirtualBox’s virtual network.

3️⃣ sudo nmcli connection up enp0s3
Activates the logical connection profile for the device.

Applies configuration (IP, DNS, routes) managed by NetworkManager.

Requests a DHCP lease and configures DNS servers.

Why it helps:
This completes the setup and brings the interface online, assigning a valid IP address to the VM.

🧾 Verification Steps
After running the commands:

✅ Check IP Address
bash
Copy code
ip a
Expected output:

sql
Copy code
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> ...
    inet 192.168.1.3/24 brd 192.168.1.255 scope global dynamic enp0s3
✅ Test Network Connectivity
bash
Copy code
ping -c 3 8.8.8.8
Output:

python
Copy code
64 bytes from 8.8.8.8: icmp_seq=1 ttl=119 time=5.51 ms
✅ Test DNS Resolution
bash
Copy code
ping -c 3 google.com
If successful, both network and DNS are working.

⚙️ Optional — Enable Autoconnect on Boot
To make sure the network reconnects automatically when the VM starts:

bash
Copy code
sudo nmcli connection modify enp0s3 connection.autoconnect yes
🧠 What is NetworkManager and nmcli?
NetworkManager
A background service in Linux that handles:

Wired and wireless connections

DHCP leases

DNS management

Routing and IP assignment

It replaces the older network service used in CentOS 6/7.

nmcli
A command-line interface to manage NetworkManager.
You can use it to:

Bring connections up or down

Configure IP, DNS, routes

Check connection status

Manage devices interactively

Example:

bash
Copy code
nmcli device status
nmcli connection show
🧰 Troubleshooting Tips
Command	Purpose
ip a	Check if the interface has an IP
nmcli device status	Show device and connection status
sudo systemctl restart NetworkManager	Restart network management service
sudo nmcli device connect <interface>	Attach a device to NetworkManager
sudo nmcli connection up <connection>	Activate connection profile
cat /etc/resolv.conf	Verify DNS configuration

🔁 When to Use These Commands
Use this fix whenever:

The VM says “Network is unreachable”

ping 8.8.8.8 fails

The adapter (enp0s3) shows no inet address

You just switched VirtualBox network mode (NAT ↔ Bridged)

You cloned or imported a VM and lost connectivity

✅ Final Result
After running:

bash
Copy code
sudo systemctl restart NetworkManager
sudo nmcli device connect enp0s3
sudo nmcli connection up enp0s3
The VM:

Obtained a valid IP via DHCP (e.g. 192.168.1.3)

Could ping external IPs and domains

yum, dnf, and curl commands worked successfully

🎉 Network and Internet access fully restored

