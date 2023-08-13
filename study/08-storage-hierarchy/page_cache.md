```s
$ dd if=/dev/zero of=testfile oflag=sync bs=1G count=1
1+0 records in
1+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.516902 s, 2.1 GB/s

$ dd if=/dev/zero of=testfile bs=1G count=1
1+0 records in
1+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.471232 s, 2.3 GB/s
```

```s
$ free -h 
              total        used        free      shared  buff/cache   available
Mem:           31Gi       806Mi        26Gi       0.0Ki       3.9Gi        30Gi
Swap:         8.0Gi          0B       8.0Gi
$ sudo su
# echo 3 > /proc/sys/vm/drop_caches 
# free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi       755Mi        30Gi       0.0Ki       119Mi        30Gi
Swap:         8.0Gi          0B       8.0Gi
```

```s
dd if=testfile of=/dev/null bs=1G count=1

$ dd if=testfile of=/dev/null bs=1G count=1
1+0 records in
1+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.354661 s, 3.0 GB/s

$ dd if=testfile of=/dev/null bs=1G count=1
1+0 records in
1+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.17141 s, 6.3 GB/s
```

```s
$ sysctl vm.dirty_writeback_centisecs
vm.dirty_writeback_centisecs = 500

$ sysctl vm.dirty_background_ratio
vm.dirty_background_ratio = 10

$ sysctl vm.dirty_ratio
vm.dirty_ratio = 20

$ sysctl vm.dirty_bytes
vm.dirty_bytes = 0

$ sysctl vm.dirty_background_bytes
vm.dirty_background_bytes = 0
```