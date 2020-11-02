# hardware 

```
$ dmesg                          => Detected hardware and boot messages (dmesg many more options)
$ cat /proc/cpuinfo              => CPU model
$ cat /proc/meminfo              => Hardware memory
$ cat /proc/interrupts           => Lists the number of interrupts per CPU per I/O device
$ lshw                           => Displays information on hardware configuration of the system
$ lsblk                          => Displays block device related information in Linux (sudo yum install util-linux-ng)
$ free -m                        => Used and free memory (-m for MB) (free command in detail)
$ lspci -tv                      => Show PCI devices (very useful to find vendor ids)
$ lsusb -tv                      => Show USB devices (read more lsusb options)
$ lshal                          => Show a list of all devices with their properties 
$ dmidecode                      => Show hardware info from the BIOS (vendor details)
$ hdparm -i /dev/sda	          # Show info about disk sda 
$ hdparm -tT /dev/sda	         # Do a read speed test on disk sda
$ badblocks -s /dev/sda	         # Test for unreadable blocks on disk sda
$ lsblk -o NAME,FSTYPE,UUID,RO,RM,SIZE,STATE,OWNER,GROUP,MODE,TYPE,MOUNTPOINT,LABEL,MODEL # list all block devices like harddrives or usb drives
```
