## Part 1
1) I am using an M1 Mac with macOS Big Sur. I will be be using the Ubuntu Operating System for this project.
2) I am using UTM for this guide on how to setup te Guest OS.
- Click on the "+" in the top left and click on "Start from Scratch"
- Name the virtual machine and contine to "System"
- In System verify the Architecture is "ARM64 (aarch64)" and the System is "QEMU 6.0 ARM Virtual Machine (alias of virt-6.0) (virt)"
Set the ammount of Memory also while in here. (I did 2 GB)
- Go to the "Drives" tab and click on "New Drive" with an interface of VirtIO and a size of your choice. Then click on "Create" (I did a drive of 20 GB and this is a fixed drive which means it will stay at 20 GB unless I change it later as I do not want it to take up more space on my PC without me knowing.)
- Click on "New Drive" again and check "Removable" and be sure the interface is USB. Then click "Create" and then "Save"
- Once you are back to the main screen, click on Browse under the "Interface: usb" and choose the ISO
- Start the VM and Install Ubuntu Desktop.
- Once this is done, you can shut down the VM and edit it. 
    - I went into Display settings and allowed "Full Graphics." This way I can use my full screen for the VM. There is no 3D Acceleration though.
    - If you want to allow any other drives that you plug into your PC like I did, go to the "Sharing" tab and make sure "USB 3.0 (XHCI) Support" is checked.
    - I also recommend enabling Clipboard Sharing. I use this as I copy things from my main OS to the VM and from my VM to my main OS.
    - If you want internet access and it is disabled by default go to the "Network" tab and check "Enabled" use the "virtio-net-pci" card for the default internet access.



## Part 2 - For part 2 I used a Windows Machine with VirtualBox
1) No, you can not access any of the files from the VM on the host machine. This is because the VM's are in their own containers. This means, that by defualt, it is not allowed for the host OS to get into the VM's files.
2) Disk Size: <br>
    Snapshot: 3.00 MB<br>
    Template: 3.37 GB<br>
What each one stores:<br>
    Snapshot: Stores the state of the VM included the disks, memory, and the settings. These capture the changes between each state (or between each snapshot) so it can be easily reverted back to the previous state without having to create a new VM.<br>
    Template: This is a copy of the entire VM, which includes the disks, devices, and the settings. This is used for VM cloning and can be givin to others so they have the same VM. This cannot be powered on and edited.
3) The network layout is NAT.
- it obtanied a private IP from my DHCP server and the VMM then mapped it to a TCP port on my machince
- This means that it is using my host machine's IP to access the external network/outside world
- This also means we can access the VM from the external network through port forwarding

## Part 3 - For part 3 I used a Windows Machine with VirtualBox
1) I am going to use a Bridged Network. To do this:
- Went to settings of VM and went to Network
- Adapter 2 > Enabled > Attacted To: Bridged Adapter > OK
- This will allow us to connect to the VM from other PCs (other as in within the local network and not on the VM)
- Then start the VM and go to the terminal and type "ip a"
- We can now see that it has its own IP address on the network (for me my home network)
- To verify this is working, we can install aoache2
- To install > use the command: sudo apt install apache2
- I went on a different device and typed in the ip of 192.168.1.117
- We get a page saying that "It works!"

## Bonus Info: Getting Bitlocker to Work in Ubuntu
1) Open a terminal
2) Install dislocker:<br>
sudo apt install dislocker
3) Make a directory for decrypting and mounting the drive<br>
sudo mkdir -p /media/bitlocker<br>
sudo mkdir -p /media/bitlockermount
4) Find your disk that you are decrypting and take note of the device<br>
sudo fdisk -l
5) Decrypt the drive where "partition" will be the device name and "password" is the password of the drive<br>
sudo dislocker "partition" -u"password" -- /media/bitlocker
6) Mount the drive so you can easily access it's files<br>
sudo mount -o loop /media/bitlocker/dislocker-file /media/bitlockermount
7) Now you should be able to access the encrypted drive like a normal external USB