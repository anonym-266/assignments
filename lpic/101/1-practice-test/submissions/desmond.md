# LPIC-101 Practice Test

### Section 1: System Architecture
1. B: `lscpu`
2.
* In terms of boot process:
  1. The BIOS
     The POST, during which the firmware checks that the basic components required for booting are oparational(e.g. RAM, hard disk, processor)
     BIOS firmware activates basic components required to boot the system.
     The firmware passes control to the bootloader
     The bootloader loads and passes control to the kernel
     The kernel initializes the variouse scripts and services required by the system
     
  1. The boot process with the UEFI firmware interface is similar  to that with the BIOS with the only difference that the EFI compatible programs are stored in
     seperate partitions

* In terms of functionality:
  The UEFI firmware interface provides additional features which are not provided by BIOS. Some of which are:
  * secure boot
  * EFI compatible softwares stored in different partitions
3. The command `lsmod` can be used to determine which kernel modules are loaded in the current system
     *  To load the new module(asuming it's device is connected to a usd port):
        Type `lsusb` to get the list of u
         ```bash
         modprobe dummy
         ```
4. The /proc and /sys directories are two important directories in the FSH that have important and distinct functions
     1. *The /proc*
          It is a  virtual filesystem that stores information about devices and asssociated currently running processes
     1. *The /sys*
          It stores information about all devices available to the system
***

### Section 2: Linux Installation and Package Management
5. C. apt install package
6. Both apt and  dpkg are package managers for debian based disros, but here are some ponts in which they differ:
   | apt | dpkg |
   |------|------|
   | apt is a high level package manager | dpkg is a low level package manager |
   | apt is more provides switches with a more user friendly format eg `apt install` | dpkg provides switches with a less user friendly format e.g. `dpkg -i`|
   | apt manages dependences | dpkg does not manage dependencies |
7. `sudo apt auto remove`

   ***

   ### Section 3: GNU and Unix Commands

9. A. head
10.  ```bash
      grep error /var/log/syslog | wc -l
       grep -c error /var/log/syslog
     ```
11.
    | hard links | soft link |
    |-------------|-----------|
    | They point to the inode of a file | They point to a path to a file |
    | Can't span accross different filesystems | Can span accross different filesystems |
    | created with `ln <target-file> <hard-link-name>` |   created with `ln -s <target-file> <soft-link-name>` |

12. ```bash
    find /etc -type f -name "*.conf" -mtime 7
    ```

13. Cron is a deamon that is responsible for executing scheduled tasks(scripts or simple commands found in files called `crontabs`)
    There are of two types: `user crontabs`(can be created and managed by the all users and found in `/var/spool/cron`) and `system crons`(can be created and managed by the root and found in `/etc/crontab`)
    By default, the cron daemond runs the scipt in the home directory of the user who created it unless the variable `HOME` points to another path in the crontab.
    If the output of the cron isn't redirected to a file, it is mailed to the user who created it unless the varable `MAILTO` points to an empty string in the crontab 
    > Example
    
      0 0 * * * ./backup.sh

***

### Section 4: Devices, Filesystems, and FHS

14. B. Disk usage in human-readable format
15. fdisk -x
16. | etx3 | etx4 |
17. Creating a new partition in etx4 filesystem
    - `Step 1`: identify the correct device to be handled. This can be done with:
    ```bash
    sudo fdisk -l
    ```
    The peripheral device may be listed as `/dev/sdX` where X can be any letter(e.g. /dev/sdb)
    
    - `step 2`: select the device
    ```bash
    sudo fdisk <device-name>
    ```
    - Enter p to print the partition table
    - Enter d as many times as there are partitions to delete existing partitions
    - Enter n for a new partition
    - Enter p for primary partition
    - Press on `Enter` to select the default first sector or enter a custum one
    - Press on `Enter` to create a partition on all the unallocated space or enter a custum space (e.g. 4G for 4 gigabytes)
    - Enter w to write the changes into the disk

      
18. The /etc/fstab is a configuration directory used to store configutions for all currently mounted filesystems
    example of an entry is
    `LABEL=cloudimg-rootfs	/	 ext4	discard,errors=remount-ro	0 1`
    
    ***

 ### Bonus Question

> **The boot process**

    When the computer is powered on, the following activities take place:
    
      - The firmware carries out the POST(Power On Self Test), and checks if the basic components required to boot the system are operational
      
      - The firmware loads the first sequence of the bootloader called the `bootstrap program`
      
      - the first sequence of the bootloader loads the second sequence of the bootloader
      
      - the second sequence of the bootloader loads the kernel
      
      - the kernel loads the initramfs and executes the scripts associated with the different services
