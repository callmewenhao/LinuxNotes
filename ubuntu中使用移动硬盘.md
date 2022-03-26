## Ubuntu中使用移动硬盘

> Windows中使用U盘、移动硬盘非常方便，但在Linux中稍有不同！
>
> 将移动硬盘插入服务器后，需要在命令行中将其挂载到当前Linux系统，使用之后再解除挂载！
>
> 注意：在命令行中的挂载是临时的，reboot后会失效！

硬盘插入服务器中后，对应着/dev/中的一个文件，如：/dev/sdb1，要将其挂载到/mnt/usb/文件夹下，这样才能访问到其中的文件。

**查看当前磁盘挂载情况：`fdisk -l`**

```shell
 ubuntu@ubuntu~ sudo fdisk -l
[sudo] password for ubuntu:

Disk /dev/sda: 1.84 TiB, 2000398934016 bytes, 3907029168 sectors
Disk model: WDC WD20EZBX-00A
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes

# 这里的/dev/sdb就是我的移动硬盘
Disk /dev/sdb: 1.84 TiB, 2000365289472 bytes, 3906963456 sectors
Disk model: My Passport 2627
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 3F10D448-C88C-4851-B618-25AA0A44307C
```

**挂载：mount**

```shell
# 这样好像没问题，但要注意磁盘是否被分区！
sudo mount /dev/sdb1 /mnt/usb/

# 建议使用下面指定格式的命令，
mount -t ntfs-3g /dev/sdb1 /mnt/usb

# 挂载成功后，即可在/mnt/usb中查看硬盘的文件
ubuntu@ubuntu  ~  sudo mount /dev/sdb1 /mnt/usb/
ubuntu@ubuntu  ~  ls -l /mnt/usb
total 73925792
-rwxrwxrwx 2 root root 67181133536 3月   7 01:37  14_weathers_minimal_data.zip
-rwxrwxrwx 1 root root  3648738783 2月   6 22:23  CycleGAN.zip
-rwxrwxrwx 2 root root  4623578485 1月  26 20:04  PascalVOC.zip
-rwxrwxrwx 2 root root   246507478 3月  26 13:36  transfuser.zip
```

**如果出现如下错误：**

```shell
The disk contains an unclean file system (0, 0). 
The file system wasn't safely closed on Windows. 
Fixing......

# 使用修复命令：
sudo ntfsfix /dev/sdb1
```

**解除挂载**

```shell
sudo umount /mnt/usb
# 或者 sudo umount /dev/sdb1
```

