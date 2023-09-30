# How to Permanently Mount External/Internal Drives in Linux

**Author:** David Boyd<br>
**Date:** 2023-09-29<br>
**Reference:** [EndavourOS][discovery]

## Introduction

This file lists only the instructions and commands to mount a drive. For the
full explanation of the commands, read the reference article taken from
[EndavourOS][discovery].

## Steps

### Step 1: Identify the drive and its device label

``` bash
lsblk
```

### Step 2: Make a new folder as the mount point for the new drive

``` bash
`sudo mkdir /mnt/<dir_name>`
```

### Step 3: Change ownership to self

``` bash
sudo chown -R $USER:$USER /mnt/<dir_name>
```

### Step 4: Change file mode permissions to self

``` bash
sudo chmod -R 744 /mnt/<dir_name>
```

### Step 5: Get drive's UUID

``` bash
sudo blkd /dev/<drive_and_partition_number> | cut -d'"' -f2 | xclip -sel clip
```

### Step 6: Note the drives filesystem (labeled in TYPE)

``` bash
sudo blkid /dev/<drive_and_partition_number>
```

### Step 7: Backup the fstab file

``` bash
sudo cp /etc/fstab /etc/fstab.bak
```

### Step 8: Add the new drive to the /etc/fstab file

Open the file:

``` bash
sudoedit /etc/fstab
```

Append the following record to the /etc/fstab file:

``` bash
# Secondary SSD
UUID=<paste_UUID> /mnt/<dir_name> <TYPE> defaults, noatime 02
```

## Step 9: Reload the fstab file

```bash
sudo systemctl daemon-reload
```

<!-- References -->

[discovery]: https://discovery.endeavouros.com/storage-and-partitions/how-to-permanently-mount-external-internal-drives-in-linux/2022/02/

