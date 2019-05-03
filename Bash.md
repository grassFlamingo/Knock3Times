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


