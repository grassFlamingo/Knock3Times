# A Collection of Linux Bash commands

## SSH

SSH Tunnel

```bash
ssh -CfNg -L listen_port:Dest_host:Dest_port user@Tunnel_Host
ssh -CfNg -R listen_port:Dest_host:Dest_port user@Tunnel_Host
ssh -CfNg -D listen_port user@Tunnel_Host
```

Make a turnel proxy for WAN to access LAN

```bash
# devices in LAN
ssh -fgCNR wan_port:local_host:local_port user@wan_host

# device in WAN
ssh -p wan_port -CfNg -D listen_port user@lan_host
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

sleep until a specific time
```bash
sleep $((`date -d "09:34:00" +%s` - `date +%s`))s
```
### SSH and tar

You can tar a remote file to local machine.
```bash
ssh server "cat fullpath.tar.gz" | tar -xzvf -
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

or
```
let cnt=0;for i in *; do nn=`file -b --mime-type $i | awk -F/ '{print $2}'`; end=`printf "%06d.%s" $cnt $nn`; mv $i $end;let cnt=$cnt+1; done
```

## Debuger

```bash
gdb
ulimit -c unlimited
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

squeeze pdf (you need to install `ghostscript` first)

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```
where `-dPDFSETTINGS` could one of:
- /screen
- /ebook
- /prepress
- /default

extract images from pdf

```bash
pdfimages -all input.pdf output 
```

## VIM

When you run `vim -d file1, file2, file3 ...` you can use `:tabdo diffoff` to shutdown diff mode in that tab and then `dp` and `dg` will help.

## Weather

```
curl wttr.in
```


## journal 

watch journals
```bash
journalctl -f
```

## nvidia

Error: 
Failed to initialize NVML: Driver/library version mismatch

run
```
sudo modprobe -r nvidia-drm
```

if error, kill processes according to
```
sudo lsof /dev/nvidia*
```

then 
```bash
sudo rmmod nvidia_uvm
sudo rmmod nvidia_modest
sudo rmmod nvidia
sudo systemctl restart nvidia-presistences.service

# audo load
sudo nvidia-smi
```



