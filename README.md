# Project1 : SOHO Network 
![ef2195ab36f537f3fd8f992f1ab6aca2.png](/_resources/ef2195ab36f537f3fd8f992f1ab6aca2.png)

***XYZ*** company is a fast-growing company in Easter Australia with more than 2 milion customers globally.  The company deals with selling and buying of food items , which are basically operated from the headquarters. The company is intending to open a branch near the local village Bonalbo , Thus, the company is intending to open a branch near the ocal village Bonalbo, Thus , the company requires young IT graduates to design the network for the branch. The network is intended to operate seperately from HQ network . Being a small network, the company has the following requirements during implementation;
- One router and one switch to be used (All CISCO products)
- 3 departments (Admin/IT , Finance/HR and Customer Service/Reception)
- Each departement is required to be in different VLAN. 
- Each department is required to have a wireless network for users 
- Host devices in the network are required to obtain IPv4 address automatically.
- Devices in all the departments are required to communicate with each other. 

## Technologies Implemented :
1. Creating a simple Network using a Router and Access Layer Switch 
2. Connecting Networking devices with Correct cabling.
3. Creating VLANS and assigning ports VLAN numbers 
4. Subnetting and Ip addressing 
5. Configuring Inter-Vlan Routing (Router on a stick )
6. Configuring DHCP  Server (Router as the DHCP Server )
7. Configuring WLAN or Wireless network (Cisco Access Point)
8. Host Device Configuration 
9. Test and Verifying Network Communication 

## Final Result :
1. Packt tracer File for the final Project Result 
2. Full Documentation of The Process in Github


# 1. Creating a Simple Network 

We going to create a simple network using Router and Access Layer Switch 

## Basic Switch Configuration 

### Navigating User Levels 
```cisco 
enable
```
This will take you to the exec mode 

```cisco 
configure terminal 
```
This will take you to the configuration mode 
***Let's change the switch name*** 
```cisco 
hostname master 
```
***Enable the password*** 
```cisco
enable secret twargap3
```
***Enable the Line Console password*** 
```cisco
line console 0 
password <password>
login
```
Enable the Line VTY password 

```cisco 
line vty 0 15 
password <password>
login 
```
Exec timout 
```cisco
exec-timout 10
```
Logging Synchnrous
```cisco
line console 0
logging synchronous
```
Disabling ip domain 
```cisco
no ip domain-lookup
```

## Basic Router Configuration 
For configuring a router, the basic steps are similar to those for configuring a switch, but there are some differences in commands and configurations. Below is a basic outline for configuring a router:

### Navigating User Levels
```cisco
enable
```
This will take you to privileged exec mode.

```cisco
configure terminal
```
This will take you to global configuration mode.

### Changing the Router Name
```cisco
hostname router1
```
This command sets the hostname of the router to "router1". Replace "router1" with your desired hostname.

### Setting Enable Secret Password
```cisco
enable secret twargap3
```
This command sets the enable secret password to "twargap3". Replace "twargap3" with your desired enable secret password.

### Setting Console Line Password
```cisco
line console 0
password your_console_password
login
```
Replace "your_console_password" with your desired console line password.

### Setting VTY Line Password
```cisco
line vty 0 15
password your_vty_password
login
```
Replace "your_vty_password" with your desired VTY line password.

### Setting Executive Timeout
```cisco
exec-timeout 10
```
This command sets the executive timeout to 10 minutes.

### Synchronous Logging for Console Line
```cisco
line console 0
logging synchronous
```
This command enables synchronous logging for the console line.

### Disabling IP Domain Lookup
```cisco
no ip domain-lookup
```
This command disables DNS domain lookup.


# 2. Connecting Networking devices with Correct cabling.
![ead3336efc74ac72641af4bfab9c0e07.png](/_resources/ead3336efc74ac72641af4bfab9c0e07.png)
We used : he cable used to connect a switch to an end device like a computer is an "Ethernet cable."

# 3. Creating VLANS and assigning ports VLAN numbers 
### VLAN Configuration for Networking Project

#### Network Topology
- 3 departments:
  - IT Department
  - Finance / HR Department
  - Customer Services Department

#### VLANs
- VLAN 10: IT Department
- VLAN 20: Finance / HR Department
- VLAN 30: Customer Services Department

#### Subnetting:
- **VLAN 10**:
  - Network: 192.168.10.0
  - Range: 192.168.10.1 - 192.168.10.14
  - Gateway: 192.168.10.1
  - Broadcast: 192.168.10.15
  - Interfaces: f0 - f3

- **VLAN 20**:
  - Network: 192.168.20.0
  - Range: 192.168.20.1 - 192.168.20.14
  - Gateway: 192.168.20.1
  - Broadcast: 192.168.20.15
  - Interfaces: f4 - f6

- **VLAN 30**:
  - Network: 192.168.30.0
  - Range: 192.168.30.1 - 192.168.30.14
  - Gateway: 192.168.30.1
  - Broadcast: 192.168.30.15
  - Interfaces: f7 - f9

#### Configuration Steps:

1. **Assign VLANs to Switch Ports:**
```cisco
configure terminal
interface range f0-f3
switchport mode access
switchport access vlan 10
exit

interface range f4-f6
switchport mode access
switchport access vlan 20
exit

interface range f7-f9
switchport mode access
switchport access vlan 30
exit
```

# 5. Configuring Inter-Vlan Routing (Router on a stick )
```cisco 
interface f10.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.240
exit

interface f10.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.240
exit

interface f10.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.240
exit

```

# 6. Configuring DHCP  Server (Router as the DHCP Server )

## DHCP Configuration Tutorial:

### Step 1: Access Router Configuration

Access the configuration mode of your router. You're already in the router's CLI. Now, let's proceed with configuring DHCP.

### Step 2: Configure DHCP on the Router

1. **Enter DHCP Configuration Mode:**

   ```bash
   Router(config)# ip dhcp pool VLAN10
   Router(dhcp-config)# network 192.168.10.0 255.255.255.0
   Router(dhcp-config)# default-router 192.168.10.1
   Router(dhcp-config)# dns-server 8.8.8.8
   Router(dhcp-config)# exit
   ```

   This creates a DHCP pool for VLAN 10, specifies the network range, default gateway, and DNS server.

2. **Repeat for VLAN 20 and VLAN 30:**

   ```bash
   Router(config)# ip dhcp pool VLAN20
   Router(dhcp-config)# network 192.168.20.0 255.255.255.0
   Router(dhcp-config)# default-router 192.168.20.1
   Router(dhcp-config)# dns-server 8.8.8.8
   Router(dhcp-config)# exit

   Router(config)# ip dhcp pool VLAN30
   Router(dhcp-config)# network 192.168.30.0 255.255.255.0
   Router(dhcp-config)# default-router 192.168.30.1
   Router(dhcp-config)# dns-server 8.8.8.8
   Router(dhcp-config)# exit
   ```

   Repeat the process for VLAN 20 and VLAN 30, replacing the network addresses and default router addresses accordingly.

### Step 3: Verify DHCP Configuration

Use the commands you've provided to verify the DHCP configuration:

- `Router# show ip interface brief`: Verify that the interfaces have IP addresses assigned to them and that they are up and up.
- `Router# show ip dhcp pool`: Verify the DHCP pools and their configurations.
- `Router# show ip dhcp binding`: Check the DHCP bindings to see which devices have been assigned IP addresses.

### Step 4: Enable Router Interfaces

Ensure that the router interfaces are enabled:

```bash
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config-if)# exit
```

Enable any other interfaces that you want to use.

#### Step 5: Save Configuration

Don't forget to save your configuration changes:

```bash
Router# write memory
```

This command saves the configuration to the router's startup configuration, ensuring that your changes persist after a reboot.


# 7. Configuring WLAN or Wireless network (Cisco Access Point)
## IT department 
![fb5358b5a362a7b7eccb68abdf444bbf.png](/_resources/fb5358b5a362a7b7eccb68abdf444bbf.png)
## Finance department 
![fb537bc77329a69daeda1a75f3411c7b.png](/_resources/fb537bc77329a69daeda1a75f3411c7b.png)
## Customer Support department 
![3eb4d6e6018b337b06177b95bade4a6a.png](/_resources/3eb4d6e6018b337b06177b95bade4a6a.png)

