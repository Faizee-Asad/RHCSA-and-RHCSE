# LAB 1 - Installation of RHEL8 & RHEL9

## Task: Install RHEL8

The below steps to install RHEL 9 can be used for both virtual and bare-metal deployment.

Step 1: Insert CD drive and Power "ON" the machine.
Note: If the machine is not boot from CD Drive then change the boot sequence form "BIOS".
Step 2: Choose the language then click on "Continue".
English - English (United States)
Step 3: To set the time and data, Click on "Time & Data".
Step 4: Select time format, then click on map to set the region and click on "Done"
Time/Date: Asia/Kolkata
Step 5: To define to packages to install in the system click on "Software selection".
Step 6: Click on "Server and GUI" and select all the packages then click on "Done".
Step 7: To define the installation disk and partitions for RHEL9, Click on "Installation Destination".
Step 8: Click the disk on which you want to install the OS, In "Storage Configration" select "Custom" to create partition on HHD, then click on "Done".
Step 9: To create partition, select partition scheme as "Standard Partition" and click on "+".
Step 10: Now you can see the "/" partition in SYSTEM. To create one more partition click on "+".
Step 11: Select mount point as "/boot" and define the capacity as "1gib then click on" Add mount point".
Step 12: Now you can see the "/boot" partitipn in SYSTEM.To create one more partiton click on "+".
Step 13: Select mount point as "/home" and define the capacity as "15gib then click on" Add mount point".
Step 14: Now you can see the "/home" partitipn in DATA.To create one more partiton click on "+".
Step 15: Select mount point as "swap" and define the capacity as "6gib then click on" Add mount point".
Step 16: Now you can see the "swap" partitipn in SYSTEM. We are done with all partitions, now click on "Done"
Step 17: Now you can see the summary of the partitions, click on "Accept Changes".
Step 18: To disable the kdump click on "KDUMP".
Step 19: Uncheck the "Enable kdump" then click on "Done".
Step 20: To manage the host name and the network configuration, Click on "Network & Host".
Step 21: By default the host name is "localhost.localdomain". Change the host name as "aserver".
Step 22: Click on "Begin installation".
Step 23: Now installation is began.To set the password click on "Root Password".
Step 24: Set your "Root Password" than click on "Done".
Step 25: To create a local user click on "User Creatation". Define Full Name and User name as "rst" and set the password as "Rst@123". Now click on Done.
Step 26: Once you installtion is complete it will provided you to reboot the system. Click on "Reboot".

## Task: Install RHEL9

# VMWare:

1. Firstly create a directory on base system (I have created: RHCSA-and-RHCSE)
2. Open Vmware.
3. Create new machine
4. Select Typical(recommended) -> Next
5. I will install later
6. Select Linux -> Red Hat Enterprise Linux 9
7. Name: RHEL9 Path: Browse Directory (RHCSA-and-RHCSE/Redhat-Linux)
8. HDD: 60GB, Single file.
9. Next
10.Finish

Edit virtual machine -> Adjust ram allocation (4GB Ram 4 Core) -> CD/DVD: Browse ISO File -> Close/Save -> Power on virtual machine.

(Press ctrl + g to capture mouse in VM | Press & release ctrl + alt to release mouse from VM | Press ctrl + alt + enter to do and exit full screen)

# Linux:

1. Install RHEL9
2. Press enter
3. Setup will start
4. Anaconda install will start
5. Language: Next
6. Package selection: Server with GUI, Tick all ADD-ONS
7. Time/Date: Asia/Kolkata
8. Installation Destination: Custom, Done, Type: Standard, Click On +, Mountpoint: (Note: 1gib = 1GB)

Hard Drive (60GB)
    |___ /boot (1GB)
    |___ /var (10GB)
    |___ / (40GB)
    |___ /home (4GB)
    |___ swap (4GB)

9. Hostname: server1
10. Root password: redhat
11: Local user: Name: abc, Password: redhat
12: Begin Install
13: Reboot



