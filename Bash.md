# A Collection of Linux Bash commands

## Copy Directory Tree Only

```bash
find . -type d -exec mkdir -p /path/to/new/directory/{} \;
```

## Clean

```bash
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```

```bash
uname -a
dpkg --get-selections|grep linux
sudo apt-get remove linux-image-xxxxxxx-generic
```

## Files

```bash
df -h
du -sh *|sort -n
```

## Debuger

```bash
gdb
ultimate -c unlimited
gdb <program> <core dump file>
```

