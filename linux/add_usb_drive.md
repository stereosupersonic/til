# Add Usb drive

1. Plug it in

2. find out about the device and UUID

```
sudo lsblk -o NAME,FSTYPE,UUID,RO,RM,SIZE,STATE,OWNER,GROUP,MODE,TYPE,MOUNTPOINT,LABEL,MODEL 
```

3. Optional: format partition (ext4)

```
sudo mkfs.ext4 /dev/sdb1 # sdb1 is a example
```

4. mount device (e.g. /mnt/data)

```
sudo mkdir  /mnt/data

# add this line to /etc/fstab
# UUID="bb18a97e-cf26-491f-a4d7-695b1777bd64"	/mnt/data	ext4    defaults  0       1

```

5. mount
```
sudo mount -a 
```
