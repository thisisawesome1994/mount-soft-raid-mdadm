# mount-soft-raid-mdadm
Mount soft raid with mdadm on ubuntu 20.04

1. Install mdadm


```
apt install mdadm

```

2. Check available drives & partitions
```
lsblk
```

3. Create raid array

```
mdadm -Cv -l0 -c64 -n2 /dev/md0 /dev/sd{b,c}1
```

4. Check if raid is created
```
cat /proc/mdstat
```

5. Make filesystem
```
mkfs.ext4 /dev/md0
```

6. Make mount point & mount
```
mkdir /mnt/my_drive
mount /dev/md0 /mnt/my_drive
```

7. Edit /etc/fstab
```
/dev/md0        /mnt/my_drive        ext4    defaults        0 0
```

8. Optional: Add drives to existing Raid0

```
mdadm --grow /dev/md0 --level=0 --raid-devices=3 --add /dev/sda
```

