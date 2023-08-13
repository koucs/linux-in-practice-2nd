inf-loop.py 実行中

```s
$ top -b -n 1 | head
top - 16:45:06 up  1:24,  0 users,  load average: 0.15, 0.04, 0.01
Tasks:  23 total,   2 running,  21 sleeping,   0 stopped,   0 zombie
%Cpu(s):  4.1 us,  0.0 sy,  0.0 ni, 95.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  32068.0 total,  30782.8 free,    648.4 used,    636.8 buff/cache
MiB Swap:   8192.0 total,   8192.0 free,      0.0 used.  31039.3 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
12147 cou       20   0   15828   9040   5760 R 100.0   0.0   0:02.60 inf-loop.py
    1 root      20   0    1816   1180   1108 S   0.0   0.0   0:00.01 init
  577 root      20   0    1812     88      0 S   0.0   0.0   0:00.00 init

```

```s
# mkdir /sys/fs/cgroup/cpu/test
# ls /sys/fs/cgroup/cpu/test
cgroup.clone_children  cpu.cfs_period_us  cpu.rt_period_us   cpu.shares  notify_on_release
cgroup.procs           cpu.cfs_quota_us   cpu.rt_runtime_us  cpu.stat    tasks

# cat /sys/fs/cgroup/cpu/test/cpu.cfs_period_us
100000
# cat /sys/fs/cgroup/cpu/test/cpu.cfs_quota_us 
-1
```

```s
echo 12882 > /sys/fs/cgroup/cpu/test/tasks
cat /sys/fs/cgroup/cpu/test/tasks
```

```s
$ top -b -n 1 | head
top - 16:50:30 up  1:30,  0 users,  load average: 0.63, 0.19, 0.06
Tasks:  27 total,   2 running,  25 sleeping,   0 stopped,   0 zombie
%Cpu(s):  4.1 us,  0.0 sy,  0.0 ni, 95.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  32068.0 total,  30743.8 free,    684.0 used,    640.2 buff/cache
MiB Swap:   8192.0 total,   8192.0 free,      0.0 used.  31003.6 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
12882 root      20   0   15828   9040   5760 R 100.0   0.0   0:54.15 inf-loop.py
    1 root      20   0    1816   1180   1108 S   0.0   0.0   0:00.01 init
  577 root      20   0    1812     88      0 S   0.0   0.0   0:00.00 init
```

```s
echo 50000 > /sys/fs/cgroup/cpu/test/cpu.cfs_quota_us 

$ top -b -n 1 | head
top - 16:53:07 up  1:32,  0 users,  load average: 0.62, 0.43, 0.18
Tasks:  27 total,   2 running,  25 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.5 us,  0.0 sy,  0.0 ni, 97.5 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  32068.0 total,  30746.5 free,    681.2 used,    640.4 buff/cache
MiB Swap:   8192.0 total,   8192.0 free,      0.0 used.  31006.3 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
12882 root      20   0   15828   9040   5760 R  50.0   0.0   2:58.99 inf-loop.py
    1 root      20   0    1816   1180   1108 S   0.0   0.0   0:00.01 init
  577 root      20   0    1812     88      0 S   0.0   0.0   0:00.00 init
```