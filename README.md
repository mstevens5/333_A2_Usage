# VM Usage Guide and Troubleshooting

# Table of Contents

1. [Linux Host](#linux-host)
2. [Windows Host](#windows-host)
3. [Other Linux 1 and 2](#other-linux-1-and-2)
3. [Troubleshooting](#troubleshooting)


# Linux Host

## Contents:
1. [Network Interfaces](#network-interfaces)
2. [Text Editor](#text-editor)
3. [Useful Tools](#useful-tools)
4. [Internet Access](#internet-access)
5. [Shutting Down Your VM](#shutting-down-your-vm)

### Network Interfaces

When you start up your Linux host, check to make sure your network interfaces are set up correclty. If they are not, you will not be able to do the assignment. **Keep in mind that the intefaces might not be set up correclty the first time you run your VM, just shut it down and try again. If you have any problems, let me know and I can give you an easy fix.** First run ifconfig and make sure your output matches the pictures below. I have outlined the three interfaces in color, where:
* Green: enp0s3 - IP address 10.229.1.1
* Red: enp0s8 - 10.229.100.1
* yellow: lo - 127.0.0.1

```sh
ifconfig
```

![](Images/IfConfig.PNG)

Next, run the following command and make sure you have 4 interfaces: lo, enp0s3, enp0s8, enp0s9.

```sh
ip link
```

![Ip Link](Images/IpLink.PNG)  

Lastly, lets make sure all routes are correctly in place. The order shouldnt matter much, just make sure you have all four routes:

```sh
route
```

![route output](Images/route.PNG)


### Text Editor

I have installed Neovim on the Linux Host machine. To run it, type:

```sh
nvim <filename>  # Where <filename> is the path of the file you want to create/edit
```

Neovim is a fork of Vim. 

### Useful Programs

* htop
* tmux
* hexdump

### Internet Access

I have created a very simple shell script that you can run to "turn on" and "turn off" the internet, so to speak. These are in your path so you can run them from anywhere.

```sh
internet_on.sh   # This will bring up your enp0s9 interface and run dhcpd for an IP address
internet_off.sh  # Release dchcp lease and grin the enp0s9 interface down
```

Note that after you run `internet_on.sh`, you should see an additional enp0s9 interface when running ipconfig. Also if you run the route command you will most likely see two new routes like so: 

![](Images/route_internet_on.PNG)  

---

# Windows Host



---

# Other Linux 1 and 2

---

# Troubleshooting

## Errors While Importing/Running VMs

### Mac - kernel driver not installed (rc=-1908)

1. If you get this error, go to your system settings and click on Security & Privacy.
2. Go to the general tab and click on the "Allow" button at the bottom next to "System software from developer "Oracle America, Inc" was blocked from loading"
3. You may need to click on the little lock in the bottom left before you can click the Allow button
4. You will have to restart your computer.

### SHA 256 Checksum errors:

This is a weird one. So far these are the two solutions that have worked:
1. Try to delete the VM and import it again. This may take a couple tries.
2. When importing, `dont` click on the "Import hard drives as VDI". Make sure it is unchecked. This will result in a .vmdk hard disk file instead of .vdi


