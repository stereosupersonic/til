# System infos Raspberry Pi

## vcgencmd 

temperature of the SoC (system on a chip) as measured by the on-board temperature sensor.

```
sudo vcgencmd measure_temp # =>  temp=66.0'C
```

Displays the current voltages used by the specific block.
```
sudo vcgencmd measure_volts
```

memory split between the CPU (arm) and GPU.
```
sudo vcgencmd get_mem arm && sudo vcgencmd get_mem gpu
```

list all commands
```
sudo vcgencmd commands
```

## hardware

hardware infos 
```
sudo apt-get install lshw
sudo lshw | less
```

cpu
```
lscpu
```

frequency of the core
```
vcgencmd measure_clock arm
```

more frequence info
```
sudo apt-get install cpufrequtils
cpufreq-info
```

## os 

info
```
hostnamectl
```

realeas info
```
cat /etc/os-release
```

kernel
```
uname -a
```

## hd 

```
df -h -t ext4 -t vfat
```
