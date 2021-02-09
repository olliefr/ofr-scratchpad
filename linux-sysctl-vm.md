# Linux kernel VM settings

Some settings of _Virtual Memory_ kernel subsystem which I find to be of interest. 

The default values can be changed in a number of ways:

* directly via the pseudofilesystem directory `/proc/sys/vm`;
* at boot time via `/etc/sysctl.conf`, or the drop-ins directory `/etc/sysctl.d/`;
* using the `sysctl` utility.

## vm.oom_kill_allocating_task

I change the default value via creating `/etc/sysctl.d/20-vm-oom-kill-allocating-task.conf` with the following content:

```
# Kills the task that triggered the out of memory situation,
# rather than trying to select the "best" one. Default is 0.

vm.oom_kill_allocating_task = 1
```

## vm.oom_dump_tasks

If enabled, dump information produced when `oom-killer` cuts in. Enabled by default: `vm.oom_dump_tasks = 1`

## vm.panic_on_oom

Enable system to crash on an out of memory situation. Disabled by default: `vm.panic_on_oom = 0`

## vm.overcommit_memory

* If 0, kernel estimates how much free memory is left when allocations are made. 
* If 1, permits all allocations until memory actually does run out. 
* If 2, prevents any overcommission. 

Default is `vm.overcommit_memory = 0`
