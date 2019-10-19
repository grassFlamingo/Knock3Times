# A Collection of Linux Bash commands

## SSH

SSH Tunnel

```bash
ssh -CfNg -L listen_port:Dest_host:Dest_port user@Tunnel_Host
ssh -CfNg -R listen_port:Dest_host:Dest_port user@Tunnel_Host
ssh -CfNg -D listen_port user@Tunnel_Host
```

## Special Tricks

Manage your time

```bash
function alertDelay {
	sleep $1
	notify-send "Times Up"
	return 0
}
```
Then you can use it like:
```bash
alertDelay 20m
```

## squashfs

Squashfs is a hightly compressed read-only filesystem for Linux. It uses zlib compression to compress both files, inodes and directories. Inodes in the system are very small and all blocks are packed to minimize data overhead. Block sizes greather than 4K are supported up to a maximum of 64K.

Squashfs is intended for general read-only filesystem use, for archival use (i.e. in cases where a .tar.gz file may be used), and in constrained block device/memory systems (e.g. embedded systems) where low overhead is needed.

> Copied from `man mksquashfs`

If you are using Linux, you can mount a squashfs (from an ISO image or somewhere else) to your system. Change your root directory via `chroot`, and you will get a new system!!! YEAHHHHH..
Excepally when you want to use some Kali preinstall packages but you don't want to install them in your Linux or reboot to a live USB or whatever.

```bash
unsquashfs filesystem.squashfs
mv filesystem.squashfs /path/to/backup/

mksquashfs squashfs-root filesystem.squashfs -b 1024k -comp xz -Xbcj x86 -e boot
```

## Generate Random Passwords | Characters

```bash
tr -dc [:graph:] < /dev/urandom | head -c 40 | xargs -0 echo
```

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

rename all files

```bash
for i in ./*; do
        md5sum "$i" | awk -v FName="$i" '
            {cmd="mv " "\""FName"\"" " " $1 ".jpg"}
            {system(cmd)}
        '
done
```

## Debuger

```bash
gdb
ultimate -c unlimited
gdb <program> <core dump file>
```

## Adjustment

```bash
nice -n 

```

## PDF

This needs *poppler-utils*. You can install it through

```bash
sudo aptitude install poppler-utils
```
Avaliable tools are

- pdfdetach
- pdffonts
- pdfinfo
- pdftocairo
- pdftohtml
- pdftoppm
- pdftops
- pdftotext
- pdfseparate
- pdfsig
- pdfunite

Remove password in pdf file:

```bash
qpdf --password='mypassword' --decrypt password.pdf nopassword.pdf
```

