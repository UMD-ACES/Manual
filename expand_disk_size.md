# Expand Disk Size

## Expanding the Disk Size on Cypherpath

1. On the SDI topology, click on your machine
2. Make sure it is powered down.
3. Click on "Edit Component"
4. Click on the "Drives" Tab
5. Click on the disk image that you would like to expand
6. Click on "New Master" and choose a name for your disk image.
7. Go to Storage->Disk Images
8. You should now see the disk image but the gear should be spinning to indicate that it is currently working on creating the disk image. When it is done, you should see a check mark.
9. Once it has been successfully created, click on the disk image and press on Edit under "Disk Image Actions"
10. In the "Disk Size (GB)" field, type in a number that you deem is sufficient. It is recommended to not put in a value over 50.
11. When you are done typing in the number, click on "Save". If a warning pops up, simply click on "Yes".
12. Now, go back to your SDI topology.
13. Repeat Steps 1-5.
14. Click on the dropdown next to "Image" and select your new master disk image.
15. Click on "Save"
16. Find your operating system below and follow its instructions

## Ubuntu Server 16.04 - Logical Volume Manager.

1. Login to the system via the VNC web viewer
2. Become root
3. Type in "cfdisk"
4. Using the arrow keys, scroll down to "Free Space"
5. Select "[New]" and press the "enter" key
6. Press the "enter" key again to create a partition size consisting of the entire "Free Space"
7. Using the arrow keys, select "[Write]"
8. A prompt will ask you if you are sure that you want to proceed, simply type in "yes"
9. Using the arrow keys, select "[Quit]"
10. Reboot the system and repeat steps 1 and 2
11. Run "fdisk -l /dev/sda" and locate your partition (you may use the size of the disk to identify it and the "Type" should simply be "Linux")
12. Run "pvcreate /dev/sdaX" where X is the device number that you identified in the previous step. Now the partition is being managed by the LVM.
13. Run "vgdisplay" and identify your volume group name. It is located next to "VG Name" (e.g. "ubuntu-vg")
14. Run "vgextend <VG Name> /dev/sdaX" where "VG Name" is replaced by the volume group name and "X" is replaced by the device number.
16. Run "lvextend -l+100%FREE /dev/<VG Name>/root" to extend the logical volume to include the new physical volume as well.
17. Run "resize2fs /dev/mapper/<VG Name>-root" to extend the filesystem. You may need two hyphens (--) between "ubuntu" and "vg"
18. Voila!
