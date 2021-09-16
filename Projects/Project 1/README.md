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

## Part 2
1) No, you can not access any of the files from the VM on the host machine. This is because the VM's are in their own containers. This means, that by defualt, it is not allowed for the host OS to get into the VM's files.
2) Disk Size:
    Snapshot: 3.00 MB
    Template: 3.37 GB
What each one stores:
    Snapshot: Stores the state of the VM included the disks, memory, and the settings. These capture the changes between each state (or between each snapshot) so it can be easily reverted back to the previous state without having to create a new VM.
    Template: This is a copy of the entire VM, which includes the disks, devices, and the settings. This is used for VM cloning and can be givin to others so they have the same VM. This cannot be powered on and edited.
3) 