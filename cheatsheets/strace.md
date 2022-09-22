# Strace
## Super funky command
```
strace -tt -f -ff -o /tmp/strace  -p "`pidof apache2`"
pids=""; for pid in $(pidof apache2); do pids="$pids -p $pid"; done; sudo strace -tt -f -ff -o /tmp/strace $pids
```

## Trace system calls involving process management
```
pids=""; for pid in $(pidof code); do pids="$pids -p $pid"; done; sudo strace -tt -f --trace=process $pids
```
