```s
$ mount | grep ^tmpfs
tmpfs on /sys/fs/cgroup type tmpfs (rw,nosuid,nodev,noexec,relatime,mode=755)

$ free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi       748Mi        28Gi       0.0Ki       1.8Gi        30Gi
Swap:         8.0Gi          0B       8.0Gi
```

```s
sudo mount -t tmpfs tmpfs /mnt -osize=1G
mount | grep /mnt
```

```s
$ mount | grep /mnt
...
tmpfs on /mnt type tmpfs (rw,relatime,size=1048576k)
```

mount 後もファイルがないと shared は 0 のまま

```s
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi       754Mi        28Gi       0.0Ki       1.8Gi        30Gi
Swap:         8.0Gi          0B       8.0Gi
```

```s
$ sudo dd if=/dev/zero of=/mnt/testfile bs=100M count=2
2+0 records in
2+0 records out
209715200 bytes (210 MB, 200 MiB) copied, 0.0601126 s, 3.5 GB/s

$ free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi       775Mi        28Gi       200Mi       2.0Gi        29Gi
Swap:         8.0Gi          0B       8.0Gi
```

```s
$ sudo umount /mnt
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi       777Mi        28Gi       0.0Ki       1.8Gi        30Gi
Swap:         8.0Gi          0B       8.0Gi
```