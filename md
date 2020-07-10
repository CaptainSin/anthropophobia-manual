Devuan
------

> Devuan GNU+Linux is a fork of Debian without systemd that allows users to reclaim control over their system by avoiding unnecessary entanglements and ensuring Init Freedom.

https://devuan.org/

Devuan is the distribution that I have been using recently for more hands-off machines.  It provides both stable upgrades and a means of downgrading (in case something does break).  I'm using it instead of Debian because System D is extremely complicated, unreliable, and poorly maintained.

An example of upgrading software.

    root@anthropophobia:~# apt-get update
    Get:1 http://deb.devuan.org/merged stable InRelease [25.6 kB]
    Get:2 http://deb.devuan.org/merged stable-security InRelease [25.6 kB]
    Fetched 51.2 kB in 4s (12.0 kB/s)
    Reading package lists... Done
    root@anthropophobia:~# apt-get upgrade
    Reading package lists... Done
    Building dependency tree
    Reading state information... Done
    Calculating upgrade... Done
    0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.


LVM2
----

> LVM2 refers to the userspace toolset that provide logical volume management facilities on linux.

http://www.sourceware.org/lvm2/

LVM2 is responsible for managing partitions and redundancy for both our storage array (the three hard drives loaded into the front of the server) and the operating system drives (the two solid state drives mounted internally at the bottom of the server).

Information about the two volume groups.

    root@anthropophobia:~# vgdisplay -s
      "anthropophobia" 893.12 GiB [64.00 GiB used / 829.12 GiB free]
      "storage" <5.46 TiB [384.01 GiB used / 5.08 TiB free]

A listing of current volumes.

    root@anthropophobia:~# lvs
      LV        VG             Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
      home      anthropophobia -wi-ao----  32.00g
      root      anthropophobia -wi-ao----  32.00g
      syncthing storage        rwi-aor--- 256.00g                                    100.00


Runit
-----

> runit - a UNIX init scheme with service supervision

http://smarden.org/runit/index.html

We're using Runit to manage services.  The "run scripts" are super short and take (relatively) very little effort to troubleshoot.

Listing process information for Syncthing.

    root@anthropophobia:~# sv status syncthing
    run: syncthing: (pid 13866) 3025s


Syncthing
---------

> Syncthing is a continuous file synchronization program.

https://syncthing.net/
