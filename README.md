# Overview - Linux VM

Here I have collected a few miscellaneous topics that may be useful/interesting. The topics include:
1. ### **Changing screen resolution**
2. ### **Changing font size**
3. ### **Enabling shared folder between host and guest OS**
4. ### **ZSH shell**


## 1. Change screen resolution

#### ******* `Note`: Do this at your own risk. It worked for me, but I cannot guarantee the same for you *******

### First, we enter Grub prompt to determine supported screen resolutions:

1. Turn on VM and hold shift. 
2. When the Grub menu pops up, press c. This will bring you to the Grub prompt.  
3. On the prompt type:
```sh
videoinfo 
```
4. Observe the output to determine possible screen resolutions supported.  
5. Then reboot via:
```sh
reboot
```
6. Log in to Linux normally
```sh
# Edit or add the following line (assuming you want a 1400 X 1050 X 32 resolution)
# GRUB_GFXMODE=1400x1050x32
nvim /etc/default/grub

# Modify this line:
# if [ "x${GRUB_GFXMODE}" = "x" ] ; then GRUB_GFXMODE=auto ; fi
# so that it looks like this one:
# if [ "x${GRUB_GFXMODE}" = "x" ] ; then GRUB_GFXMODE=1400x1050x32 ; fi
nvim /etc/grub.d/00_header

# Next, update Grub
grub-mkconfig -o /boot/grub/grub.cfg
```


## 2. Change font size

```sh
pacman -S terminus-font  # Get terminus font
setfont ter-132n         # Change font to larger terminus font
setfont                  # Restore default font
```


## 3. Adding a shared folder

1. First, log on to your VM and create a directory that you want to use as your mount point for sharing with your host OS. (You can use the /home/shared/ directory if you wish. I created this folder for this exact purpose when I made the VMs.
2. Make sure the vboxservice is running:
```sh
systemctl status vboxservice 
# If it says enabled, you are good to go. Otherwise you must enable it with the following command:
systemctl enable vboxservice
```
3. Second, shutdown your VM, open VirtualBox and open the settings for your VM.
4. Go to the Shared Folders tab
5. Click on the green plus sign (on the right)
```
Folder Path: the path to a directory on your host OS where you want to share files.
Folder Name: on your host OS
Mount Point: the directory on your guest OS (/home/shared/ for example)
I usually click "Auto-mount" but it is up to you. 
``` 

```
#### Open VM settings and create a shared folder 

Use the mount point we just creaetd: /home/shared

#### Start VM - Test shared folder

Log in as root  
Note: The persmissions for /home/shared should be changed to group vboxsf.  

## 4. ZSH
```sh
cd /usr/share/oh-my-zsh
```


## 5. Useful commands

```sh
nvim
hexdump
hexdump -C # Show ascii next to the hex output
```


# Windows

## Shared Folder
* Shutdown VM
* In VirtualBox, click on settings and then Shared folders
* Add a Machine Folder
* Folder Path: Your host OS
* Folder Name: Your host OS
* I usually click Auto-mount and Make Permanent (You can research these yourself)
* Mount point: This would be the path on your guest OS where you want the shared folder mounted. It seems like you can ignore this for the most part on Windows.
* Start your VM and open File Explorer. You should see a new drive under "This PC" or "Network".
