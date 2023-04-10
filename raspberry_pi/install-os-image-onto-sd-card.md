# Install an OS Image on an SD Card via CLI

> Author: David Boyd<br>
> Date: 2023-04-10<br>
> Ref: [raspberrypi.stackexchange]

## Steps

1. Download the image: [Raspberry PI OS List]
2. Extract the img file: `unxz name-of-os.img.xz`
3. (If mounted): Unmount drive if mounted: `umount /dev/name-of-device`
4. (If necessary): Format disk via: `fdisk /dev/name-of-device`
5. (If necessary): Change partition type to FAT32 via: `fdisk`
6. (If necessary): Create filesystem to MS DOS via: `mkfs.fat`
7. Copy the contents of the image file on the device: `sudo dd bs=1M
   if=name-of-os.img of=/dev/name-of-device`

[Raspberry PI OS List]: https://www.raspberrypi.com/software/operating-systems/
[raspberrypi.stackexchange]: https://raspberrypi.stackexchange.com/questions/931/how-do-i-install-an-os-image-onto-an-sd-card
