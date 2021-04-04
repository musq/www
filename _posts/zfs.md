✦ ❯ lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda       8:0    0   477G  0 disk
├─sda1    8:1    0   260M  0 part /boot/efi
├─sda2    8:2    0    16M  0 part
├─sda3    8:3    0   100G  0 part
├─sda4    8:4    0 100.1G  0 part
├─sda5    8:5    0   800M  0 part
├─sda6    8:6    0  23.9G  0 part /
├─sda7    8:7    0   102G  0 part /home
├─sda8    8:8    0    17G  0 part [SWAP]
├─sda9    8:9    0  29.3G  0 part
├─sda10   8:10   0    20G  0 part
├─sda11   8:11   0    20G  0 part
├─sda12   8:12   0    20G  0 part
├─sda13   8:13   0    20G  0 part
├─sda14   8:14   0     3G  0 part
├─sda15   8:15   0     3G  0 part
├─sda16 259:0    0     3G  0 part
└─sda17 259:1    0     3G  0 part

root in ~
✦ ❯ modinfo zfs | grep version
version:        0.7.5-1ubuntu16.10
srcversion:     67FB53EEE2E7A895E7E0074


✦ ❯ zpool create dpool mirror sda14 sda15

root in ~
✦ ❯ zpool status
  pool: dpool
 state: ONLINE
  scan: none requested
config:

        NAME        STATE     READ WRITE CKSUM
        dpool       ONLINE       0     0     0
          mirror-0  ONLINE       0     0     0
            sda14   ONLINE       0     0     0
            sda15   ONLINE       0     0     0

errors: No known data errors

root in ~
✦ ❯ zfs create dpool/data

root in ~
✦ ❯ zfs list -t all
NAME         USED  AVAIL  REFER  MOUNTPOINT
dpool        112K  2.86G    24K  /dpool
dpool/data    24K  2.86G    24K  /dpool/data

✦ ❯ zfs list -t all -o space
NAME        AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool       2.86G   114K        0B     24K             0B        90K
dpool/data  2.86G    24K        0B     24K             0B         0B

✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   126K  2.98G         -     0%     0%  1.00x  ONLINE  -

✦ ❯ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            7.8G     0  7.8G   0% /dev
tmpfs           1.6G   11M  1.6G   1% /run
/dev/sda6        24G   22G  848M  97% /
tmpfs           7.8G  172M  7.6G   3% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
/dev/sda7       101G   92G  3.3G  97% /home
/dev/sda1       256M   45M  212M  18% /boot/efi
tmpfs           1.6G   28K  1.6G   1% /run/user/126
tmpfs           1.6G   44K  1.6G   1% /run/user/1000
dpool           2.9G     0  2.9G   0% /dpool
dpool/data      2.9G     0  2.9G   0% /dpool/data

✦ ❯ ls -lh
total 572M
-rw-r--r-- 1 root root 571M Jan  5 13:24 latest-nixos-minimal-x86_64-linux.iso

root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/

root in ~/tools took 4s
✦ ❯ zfs list -t all -o space
NAME        AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool       2.30G   572M        0B     24K             0B       571M
dpool/data  2.30G   571M        0B    571M             0B         0B

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     4%    18%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            7.8G     0  7.8G   0% /dev
tmpfs           1.6G   11M  1.6G   1% /run
/dev/sda6        24G   22G  850M  97% /
tmpfs           7.8G  154M  7.7G   2% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
/dev/sda7       101G   92G  3.3G  97% /home
/dev/sda1       256M   45M  212M  18% /boot/efi
tmpfs           1.6G   32K  1.6G   1% /run/user/126
tmpfs           1.6G   48K  1.6G   1% /run/user/1000
dpool           2.4G  128K  2.4G   1% /dpool
dpool/data      2.9G  572M  2.4G  20% /dpool/data

Delete ISO
root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso

Show list immediately
root in ~/tools
✦ ❯ zfs list -t all -o space
NAME        AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool       2.30G   572M        0B     24K             0B       572M
dpool/data  2.30G   571M        0B    571M             0B         0B

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     2%    18%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            7.8G     0  7.8G   0% /dev
tmpfs           1.6G   11M  1.6G   1% /run
/dev/sda6        24G   22G  849M  97% /
tmpfs           7.8G  154M  7.7G   2% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
/dev/sda7       101G   92G  3.3G  97% /home
/dev/sda1       256M   45M  212M  18% /boot/efi
tmpfs           1.6G   32K  1.6G   1% /run/user/126
tmpfs           1.6G   48K  1.6G   1% /run/user/1000
dpool           2.9G     0  2.9G   0% /dpool
dpool/data      2.9G     0  2.9G   0% /dpool/data


Show list after a couple of seconds
root in ~/tools
✦ ❯ zfs list -t all -o space
NAME        AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool       2.86G   171K        0B     24K             0B       147K
dpool/data  2.86G    24K        0B     24K             0B         0B

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   340K  2.98G         -     2%     0%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            7.8G     0  7.8G   0% /dev
tmpfs           1.6G   11M  1.6G   1% /run
/dev/sda6        24G   22G  850M  97% /
tmpfs           7.8G  154M  7.7G   2% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
/dev/sda7       101G   92G  3.3G  97% /home
/dev/sda1       256M   45M  212M  18% /boot/efi
tmpfs           1.6G   32K  1.6G   1% /run/user/126
tmpfs           1.6G   48K  1.6G   1% /run/user/1000
dpool           2.9G     0  2.9G   0% /dpool
dpool/data      2.9G     0  2.9G   0% /dpool/data



root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/

root in ~/tools took 3s
✦ ❯ zfs snapshot dpool/data@snap1

root in ~/tools
✦ ❯ zfs snapshot dpool/data@snap2

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             2.30G   572M        0B     24K             0B       572M
dpool/data        2.30G   571M        0B    571M             0B         0B
dpool/data@snap1      -     0B         -       -              -          -
dpool/data@snap2      -     0B         -       -              -          -

✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     5%    18%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            7.8G     0  7.8G   0% /dev
tmpfs           1.6G   11M  1.6G   1% /run
/dev/sda6        24G   22G  849M  97% /
tmpfs           7.8G  154M  7.7G   2% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
/dev/sda7       101G   92G  3.3G  97% /home
/dev/sda1       256M   45M  212M  18% /boot/efi
tmpfs           1.6G   32K  1.6G   1% /run/user/126
tmpfs           1.6G   48K  1.6G   1% /run/user/1000
dpool           2.4G     0  2.4G   0% /dpool
dpool/data      2.9G  572M  2.4G  20% /dpool/data

root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             2.30G   572M        0B     24K             0B       572M
dpool/data        2.30G   571M      571M     24K             0B         0B
dpool/data@snap1      -     0B         -       -              -          -
dpool/data@snap2      -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     5%    18%  1.00x  ONLINE  -

✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           2.4G     0  2.4G   0% /dpool
dpool/data      2.4G     0  2.4G   0% /dpool/data

root in ~/tools
✦ ❯ zfs snapshot dpool/data@snap3

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             2.30G   572M        0B     24K             0B       572M
dpool/data        2.30G   571M      571M     24K             0B         0B
dpool/data@snap1      -     0B         -       -              -          -
dpool/data@snap2      -     0B         -       -              -          -
dpool/data@snap3      -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     5%    18%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           2.4G     0  2.4G   0% /dpool
dpool/data      2.4G     0  2.4G   0% /dpool/data


root in ~/tools
✦ ❯ zfs destroy dpool/data@snap1

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             2.30G   572M        0B     24K             0B       572M
dpool/data        2.30G   571M      571M     24K             0B         0B
dpool/data@snap2      -   571M         -       -              -          -
dpool/data@snap3      -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     5%    18%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           2.4G     0  2.4G   0% /dpool
dpool/data      2.4G     0  2.4G   0% /dpool/data


root in ~/tools
✦ ❯ zfs destroy dpool/data@snap3

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             2.30G   572M        0B     24K             0B       572M
dpool/data        2.30G   571M      571M     24K             0B         0B
dpool/data@snap2      -   571M         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   572M  2.43G         -     5%    18%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           2.4G     0  2.4G   0% /dpool
dpool/data      2.4G     0  2.4G   0% /dpool/data


✦ ❯ zfs destroy dpool/data@snap2

After a couple of seconds
root in ~/tools
✦ ❯ zfs list -t all -o space
NAME        AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool       2.86G   765K        0B     24K             0B       741K
dpool/data  2.86G    24K        0B     24K             0B         0B

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G   890K  2.98G         -     3%     0%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           2.9G     0  2.9G   0% /dpool
dpool/data      2.9G     0  2.9G   0% /dpool/data










root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.1

root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.2

root in ~/tools took 5s
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.3

root in ~/tools
✦ ❯ ls -lh /dpool/data/
total 1.2G
-rw-r--r-- 1 root root 571M Jan  7 16:20 latest-nixos-minimal-x86_64-linux.iso.1
-rw-r--r-- 1 root root 571M Jan  7 16:21 latest-nixos-minimal-x86_64-linux.iso.2
-rw-r--r-- 1 root root 571M Jan  7 16:21 latest-nixos-minimal-x86_64-linux.iso.3


root in ~/tools
✦ ❯ zfs list -t all -o space
NAME        AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool       1.19G  1.67G        0B     24K             0B      1.67G
dpool/data  1.19G  1.67G        0B   1.67G             0B         0B

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  1.67G  1.31G         -    12%    56%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           1.2G     0  1.2G   0% /dpool
dpool/data      2.9G  1.7G  1.2G  59% /dpool/data


root in ~/tools
✦ ❯ zfs snapshot dpool/data@snap4

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             1.18G  1.67G        0B     24K             0B      1.67G
dpool/data        1.18G  1.67G        0B   1.67G             0B         0B
dpool/data@snap4      -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  1.68G  1.31G         -    12%    56%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           1.2G  128K  1.2G   1% /dpool
dpool/data      2.9G  1.7G  1.2G  59% /dpool/data


root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso.3

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             1.18G  1.67G        0B     24K             0B      1.67G
dpool/data        1.18G  1.67G      571M   1.12G             0B         0B
dpool/data@snap4      -   571M         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  1.67G  1.31G         -    12%    56%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           1.2G  128K  1.2G   1% /dpool
dpool/data      2.4G  1.2G  1.2G  49% /dpool/data


root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso.2

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             1.18G  1.67G        0B     24K             0B      1.67G
dpool/data        1.18G  1.67G     1.12G    571M             0B         0B
dpool/data@snap4      -  1.12G         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  1.67G  1.31G         -    12%    56%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           1.2G     0  1.2G   0% /dpool
dpool/data      1.8G  572M  1.2G  33% /dpool/data


root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso.1

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             1.18G  1.67G        0B     24K             0B      1.67G
dpool/data        1.18G  1.67G     1.67G     24K             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  1.67G  1.31G         -    12%    56%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           1.2G     0  1.2G   0% /dpool
dpool/data      1.2G     0  1.2G   0% /dpool/data


root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.4

root in ~/tools took 5s
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool              641M  2.23G        0B     24K             0B      2.23G
dpool/data         641M  2.23G     1.67G    571M             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.23G   769M         -    19%    74%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           642M     0  642M   0% /dpool
dpool/data      1.2G  572M  642M  48% /dpool/data


root in ~/tools
✦ ❯ zfs snapshot dpool/data@snap5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool              641M  2.23G        0B     24K             0B      2.23G
dpool/data         641M  2.23G     1.67G    571M             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.23G   768M         -    19%    74%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           642M     0  642M   0% /dpool
dpool/data      1.2G  572M  642M  48% /dpool/data

t in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso
/dpool/data/latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools took 7s
✦ ❯ ls -lh /dpool/data/
total 1.2G
-rw-r--r-- 1 root root 571M Jan  7 17:10 latest-nixos-minimal-x86_64-linux.iso.4
-rw-r--r-- 1 root root 571M Jan  7 17:19 latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             69.7M  2.79G        0B     24K             0B      2.79G
dpool/data        69.7M  2.79G     1.67G   1.12G             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -    14K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.79G   197M         -    39%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      1.2G  1.2G   70M  95% /dpool/data

t in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso
/dpool/data/latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools took 7s
✦ ❯ ls -lh /dpool/data/
total 1.2G
-rw-r--r-- 1 root root 571M Jan  7 17:10 latest-nixos-minimal-x86_64-linux.iso.4
-rw-r--r-- 1 root root 571M Jan  7 17:19 latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             69.7M  2.79G        0B     24K             0B      2.79G
dpool/data        69.7M  2.79G     1.67G   1.12G             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -    14K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.79G   197M         -    39%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      1.2G  1.2G   70M  95% /dpool/data

root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools took 7s
✦ ❯ ls -lh /dpool/data/
total 1.2G
-rw-r--r-- 1 root root 571M Jan  7 17:10 latest-nixos-minimal-x86_64-linux.iso.4
-rw-r--r-- 1 root root 571M Jan  7 17:19 latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             69.7M  2.79G        0B     24K             0B      2.79G
dpool/data        69.7M  2.79G     1.67G   1.12G             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -    14K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.79G   197M         -    39%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      1.2G  1.2G   70M  95% /dpool/data


root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools took 7s
✦ ❯ ls -lh /dpool/data/
total 1.2G
-rw-r--r-- 1 root root 571M Jan  7 17:10 latest-nixos-minimal-x86_64-linux.iso.4
-rw-r--r-- 1 root root 571M Jan  7 17:19 latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             69.7M  2.79G        0B     24K             0B      2.79G
dpool/data        69.7M  2.79G     1.67G   1.12G             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -    14K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.79G   197M         -    39%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      1.2G  1.2G   70M  95% /dpool/data


root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso.5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool              642M  2.23G        0B     24K             0B      2.23G
dpool/data         642M  2.23G     1.67G    571M             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -    14K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.23G   769M         -    24%    74%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool           642M     0  642M   0% /dpool
dpool/data      1.2G  572M  642M  48% /dpool/data


root in ~/tools
✦ ❯ cp latest-nixos-minimal-x86_64-linux.iso /dpool/data/latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ ls -lh /dpool/data/
total 1.2G
-rw-r--r-- 1 root root 571M Jan  7 17:10 latest-nixos-minimal-x86_64-linux.iso.4
-rw-r--r-- 1 root root 571M Jan  7 17:26 latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools took 7s
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             69.5M  2.79G        0B     24K             0B      2.79G
dpool/data        69.5M  2.79G     1.67G   1.12G             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -    14K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.79G   197M         -    43%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M  128K   70M   1% /dpool
dpool/data      1.2G  1.2G   70M  95% /dpool/data


root in ~/tools
✦ ❯ rm /dpool/data/latest-nixos-minimal-x86_64-linux.iso.4

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dpool             69.4M  2.79G        0B     24K             0B      2.79G
dpool/data        69.4M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -   571M         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME    SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dpool  2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      641M  572M   70M  90% /dpool/data

root in ~/tools
✦ ❯ zpool status
  pool: dpool
 state: ONLINE
  scan: none requested
config:

        NAME        STATE     READ WRITE CKSUM
        dpool       ONLINE       0     0     0
          mirror-0  ONLINE       0     0     0
            sda14   ONLINE       0     0     0
            sda15   ONLINE       0     0     0

errors: No known data errors


root in ~/tools
✦ ❯ zpool create dbackup mirror sda16 sda17

root in ~/tools
✦ ❯ zpool status
  pool: dbackup
 state: ONLINE
  scan: none requested
config:

        NAME        STATE     READ WRITE CKSUM
        dbackup     ONLINE       0     0     0
          mirror-0  ONLINE       0     0     0
            sda16   ONLINE       0     0     0
            sda17   ONLINE       0     0     0

errors: No known data errors

  pool: dpool
 state: ONLINE
  scan: none requested
config:

        NAME        STATE     READ WRITE CKSUM
        dpool       ONLINE       0     0     0
          mirror-0  ONLINE       0     0     0
            sda14   ONLINE       0     0     0
            sda15   ONLINE       0     0     0

errors: No known data errors

root in ~/tools
✦ ❯ zfs create dbackup/data

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME              AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup           2.86G   112K        0B     24K             0B      88.5K
dbackup/data      2.86G    24K        0B     24K             0B         0B
dpool             69.4M  2.79G        0B     24K             0B      2.79G
dpool/data        69.4M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4      -  1.67G         -       -              -          -
dpool/data@snap5      -   571M         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G   192K  2.98G         -     0%     0%  1.00x  ONLINE  -
dpool    2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      641M  572M   70M  90% /dpool/data
dbackup         2.9G     0  2.9G   0% /dbackup
dbackup/data    2.9G     0  2.9G   0% /dbackup/data

root in ~/tools
✦ ❯ zfs send dpool/data@snap4 | zfs recv dbackup/data
cannot receive new filesystem stream: destination 'dbackup/data' exists
must specify -F to overwrite it

root in ~/tools
✦ ❯ zfs destroy dbackup/data


root in ~/tools
✦ ❯ zfs send dpool/data@snap4 | zfs recv dbackup/data

root in ~/tools took 15s
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup             1.18G  1.67G        0B     25K             0B      1.67G
dbackup/data        1.18G  1.67G        0B   1.67G             0B         0B
dbackup/data@snap4      -     0B         -       -              -          -
dpool               69.4M  2.79G        0B     24K             0B      2.79G
dpool/data          69.4M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -

root in ~/tools
✦ ❯ zfs send -i dpool/data@snap4 dpool/data@snap5 | zfs recv dbackup/data

root in ~/tools took 6s
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup              641M  2.23G        0B     25K             0B      2.23G
dbackup/data         641M  2.23G     1.67G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -     0B         -       -              -          -
dpool               69.4M  2.79G        0B     24K             0B      2.79G
dpool/data          69.4M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.23G   770M         -    19%    74%  1.00x  ONLINE  -
dpool    2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      641M  572M   70M  90% /dpool/data
dbackup         642M     0  642M   0% /dbackup
dbackup/data    1.2G  572M  642M  48% /dbackup/data


root in ~/tools
✦ ❯ ll /dpool/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ ll /dbackup/data/
.rw-r--r-- 598M root root  7 Jan 17:10 latest-nixos-minimal-x86_64-linux.iso.4

root in ~/tools
✦ ❯ zfs snapshot dpool/data@snap6

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup              642M  2.23G        0B     25K             0B      2.23G
dbackup/data         642M  2.23G     1.67G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -    13K         -       -              -          -
dpool               69.4M  2.79G        0B     24K             0B      2.79G
dpool/data          69.4M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.23G   770M         -    19%    74%  1.00x  ONLINE  -
dpool    2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      641M  572M   70M  90% /dpool/data
dbackup         642M     0  642M   0% /dbackup
dbackup/data    1.2G  572M  642M  48% /dbackup/data


root in ~/tools
✦ ❯ zfs send -i dpool/data@snap4 dpool/data@snap6 | zfs recv dbackup/data
cannot receive incremental stream: destination dbackup/data has been modified
since most recent snapshot


root in ~/tools
✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv dbackup/data
cannot receive incremental stream: destination dbackup/data has been modified
since most recent snapshot

root in ~/tools
✦ ❯ zfs rollback dbackup/data@snap5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup              642M  2.23G        0B     25K             0B      2.23G
dbackup/data         642M  2.23G     1.67G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -     0B         -       -              -          -
dpool               69.4M  2.79G        0B     24K             0B      2.79G
dpool/data          69.4M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.23G   770M         -    19%    74%  1.00x  ONLINE  -
dpool    2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      641M  572M   70M  90% /dpool/data
dbackup         642M     0  642M   0% /dbackup
dbackup/data    1.2G  572M  642M  48% /dbackup/data


root in ~/tools
✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv dbackup/data

root in ~/tools took 9s
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup             69.7M  2.79G        0B     25K             0B      2.79G
dbackup/data        69.7M  2.79G     2.23G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -   571M         -       -              -          -
dbackup/data@snap6      -     0B         -       -              -          -
dpool               70.0M  2.79G        0B     24K             0B      2.79G
dpool/data          70.0M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.79G   197M         -    40%    93%  1.00x  ONLINE  -
dpool    2.98G  2.79G   198M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M  128K   70M   1% /dpool
dpool/data      642M  572M   70M  90% /dpool/data
dbackup          70M  128K   70M   1% /dbackup
dbackup/data    641M  572M   70M  90% /dbackup/data


root in ~/tools
✦ ❯ ll /dbackup/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ ll /dpool/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6



root in ~/tools
✦ ❯ zfs destroy dbackup/data@snap5

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup              641M  2.23G        0B     25K             0B      2.23G
dbackup/data         641M  2.23G     1.67G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap6      -     0B         -       -              -          -
dpool               70.0M  2.79G        0B     24K             0B      2.79G
dpool/data          70.0M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -     0B         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.23G   769M         -    23%    74%  1.00x  ONLINE  -
dpool    2.98G  2.79G   196M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            69M  128K   69M   1% /dpool
dpool/data      640M  572M   69M  90% /dpool/data
dbackup         642M     0  642M   0% /dbackup
dbackup/data    1.2G  572M  642M  48% /dbackup/data


✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv dbackup/data
cannot receive incremental stream: destination dbackup/data has been modified
since most recent snapshot

root in ~/tools
✦ ❯ zfs destroy dbackup/data@snap6

root in ~/tools
✦ ❯ ll /dpool/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ ll /dbackup/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup              642M  2.23G        0B     25K             0B      2.23G
dbackup/data         642M  2.23G     1.67G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dpool               70.0M  2.79G        0B     24K             0B      2.79G
dpool/data          70.0M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -    13K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.23G   770M         -    23%    74%  1.00x  ONLINE  -
dpool    2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      642M  572M   70M  90% /dpool/data
dbackup         642M     0  642M   0% /dbackup
dbackup/data    1.2G  572M  642M  48% /dbackup/data

root in ~/tools
✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv dbackup/data
cannot receive incremental stream: destination dbackup/data has been modified
since most recent snapshot

root in ~/tools
✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv -F dbackup/data

root in ~/tools took 15s
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup             69.4M  2.79G        0B     25K             0B      2.79G
dbackup/data        69.4M  2.79G     2.23G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -   571M         -       -              -          -
dbackup/data@snap6      -     0B         -       -              -          -
dpool               70.0M  2.79G        0B     24K             0B      2.79G
dpool/data          70.0M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -    13K         -       -              -          -

root in ~/tools
✦ ❯ zpool list
NAME      SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
dbackup  2.98G  2.79G   197M         -    44%    93%  1.00x  ONLINE  -
dpool    2.98G  2.79G   198M         -    44%    93%  1.00x  ONLINE  -

root in ~/tools
✦ ❯ df -h /dpool /dpool/data /dbackup /dbackup/data
Filesystem      Size  Used Avail Use% Mounted on
dpool            70M     0   70M   0% /dpool
dpool/data      642M  572M   70M  90% /dpool/data
dbackup          70M     0   70M   0% /dbackup
dbackup/data    641M  572M   70M  90% /dbackup/data

root in ~/tools
✦ ❯ ll /dbackup/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ ll /dpool/data/
.rw-r--r-- 598M root root  7 Jan 17:26 latest-nixos-minimal-x86_64-linux.iso.6


Send and Receive are atomic operations. If send/recv is interrupted in the middle, we'll
either have the intermediary snapshots or not. The filesystem won't be in an
inconsistent state.

root in ~/tools
✦ ❯ zfs destroy dbackup/data@snap5

root in ~/tools
✦ ❯ zfs destroy dbackup/data@snap6

root in ~/tools
✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv -F dbackup/data
^C (Interrupt at 10 seconds into the operation)

root in ~/tools took 11s
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup              640M  2.23G        0B     25K             0B      2.23G
dbackup/data         640M  2.23G     1.67G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -     0B         -       -              -          -
dpool               69.9M  2.79G        0B     24K             0B      2.79G
dpool/data          69.9M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -    13K         -       -              -          -

We notice that we have received snap5, but snap6 hasn't yet been received. So we rerun
the send/recv commands to resume our operation. It takes the time proportional to the
snap6-snap5

root in ~/tools
✦ ❯ zfs send -I dpool/data@snap4 dpool/data@snap6 | zfs recv -F dbackup/data

root in ~/tools took 8s
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup             68.7M  2.79G        0B     25K             0B      2.79G
dbackup/data        68.7M  2.79G     2.23G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -   571M         -       -              -          -
dbackup/data@snap6      -     0B         -       -              -          -
dpool               69.9M  2.79G        0B     24K             0B      2.79G
dpool/data          69.9M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -    13K         -       -              -          -



root in ~/tools
✦ ❯ zfs diff dpool/data@snap4 dpool/data@snap6
M       /dpool/data/
-       /dpool/data/latest-nixos-minimal-x86_64-linux.iso.3
-       /dpool/data/latest-nixos-minimal-x86_64-linux.iso.1
-       /dpool/data/latest-nixos-minimal-x86_64-linux.iso.2
+       /dpool/data/latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ zfs diff dpool/data@snap5 dpool/data@snap6
M       /dpool/data/
-       /dpool/data/latest-nixos-minimal-x86_64-linux.iso.4
+       /dpool/data/latest-nixos-minimal-x86_64-linux.iso.6

root in ~/tools
✦ ❯ zfs diff dpool/data@snap6 dpool/data@snap5
Unable to obtain diffs:
   Not an earlier snapshot from the same fs



Rollback

✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup             67.3M  2.79G        0B     25K             0B      2.79G
dbackup/data        67.3M  2.79G     2.23G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -   571M         -       -              -          -
dbackup/data@snap6      -     0B         -       -              -          -
dpool               69.9M  2.79G        0B     24K             0B      2.79G
dpool/data          69.9M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -    13K         -       -              -          -

root in ~/tools
✦ ❯ zfs rollback dbackup/data@snap4
cannot rollback to 'dbackup/data@snap4': more recent snapshots or bookmarks exist
use '-r' to force deletion of the following snapshots and bookmarks:
dbackup/data@snap6
dbackup/data@snap5

root in ~/tools
✦ ❯ zfs rollback dbackup/data@snap6

root in ~/tools
✦ ❯ zfs rollback dbackup/data@snap5
cannot rollback to 'dbackup/data@snap5': more recent snapshots or bookmarks exist
use '-r' to force deletion of the following snapshots and bookmarks:
dbackup/data@snap6

root in ~/tools
✦ ❯ zfs list -t all -o space
NAME                AVAIL   USED  USEDSNAP  USEDDS  USEDREFRESERV  USEDCHILD
dbackup             67.4M  2.79G        0B     25K             0B      2.79G
dbackup/data        67.4M  2.79G     2.23G    571M             0B         0B
dbackup/data@snap4      -  1.67G         -       -              -          -
dbackup/data@snap5      -   571M         -       -              -          -
dbackup/data@snap6      -     0B         -       -              -          -
dpool               69.9M  2.79G        0B     24K             0B      2.79G
dpool/data          69.9M  2.79G     2.23G    571M             0B         0B
dpool/data@snap4        -  1.67G         -       -              -          -
dpool/data@snap5        -   571M         -       -              -          -
dpool/data@snap6        -    13K         -       -              -          -

