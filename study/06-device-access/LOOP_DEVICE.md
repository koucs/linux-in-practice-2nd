
```s
fallocate -l 1G loopdevice.img
sudo losetup -f loopdevice.img
losetup -l
```

```s
$ losetup -l
NAME       SIZELIMIT OFFSET AUTOCLEAR RO BACK-FILE                                                                                 DIO LOG-SEC
/dev/loop0         0      0         0  0 /home/d/linux-in-practice-2nd/study/06-device-access/loopdevice.img   0     512
```

```s
sudo mkfs.ext4 /dev/loop0

mkdir mnt
sudo mount /dev/loop0 mnt
mount

$ mount
...
/dev/loop0 on /home/dev/getting-started/linux-in-practice-2nd/study/06-device-access/mnt type ext4 (rw,relatime)
```

root user でやる

```s
echo "hello world" > mnt/testfile
ls mnt
cat mnt/testfile
unmount mnt
```

```s
# strings -t x /dev/loop0 
1091020 lost+found
1091034 testfile
80003fc OD;/
8081000 hello world
20009020 lost+found
20009034 testfile

# dd if=testfile-overwrite of=/dev/loop0 seek=$((0x8081000)) bs=1
16+0 records in
16+0 records out
16 bytes copied, 0.0389753 s, 0.4 kB/s

# strings -t x /dev/loop0 
1091020 lost+found
1091034 testfile
80003fc OD;/
8081000 HELLO WORLD NEW
20009020 lost+found
20009034 testfile
```

```s
# mount /dev/loop0 mnt
# ls
LOOP_DEVICE.md  loopdevice.img  mnt  testfile-overwrite
# cd mnt/
# ls
lost+found  testfile
# cat testfile 
HELLO WORLD 
```

大文字になった。 NEW が入っていないのはファイルサイズのせい？