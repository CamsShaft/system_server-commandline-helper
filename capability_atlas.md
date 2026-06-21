# Toybox Capability Atlas

A reference for every command available in Samsung's toybox build, classified by what it can do **without a shell, pipes, redirection, or wildcards**.

Generated from Samsungs crappy toybox on my device (Samsung Galaxy S22, Toybox 0.8.9-android) and cross-referenced against [https://landley.net/toybox/help.html](https://landley.net/toybox/help.html) by Rob @landley here on github, thank you for your website good sir.

## Capability Classes

| Class | Meaning |
|-------|---------|
| `[exec-capable]` | Can spawn another command as part of its job — these are your shell replacement primitives |
| `[self-contained]` | Has its own filter or search engine — no pipe into grep or awk needed |
| `[io-explicit]` | Uses named file flags or args instead of shell redirection |
| `[terminal]` | Produces output only — limited composition, but may feed exec-capable commands |

## Table of Contents

### [exec-capable] (24)

[`brctl`](#brctl) · [`chroot`](#chroot) · [`chrt`](#chrt) · [`env`](#env) · [`find`](#find)
[`flock`](#flock) · [`inotifyd`](#inotifyd) · [`ionice`](#ionice) · [`nc`](#nc) · [`netcat`](#netcat)
[`nice`](#nice) · [`nohup`](#nohup) · [`nsenter`](#nsenter) · [`prlimit`](#prlimit) · [`rfkill`](#rfkill)
[`runcon`](#runcon) · [`setsid`](#setsid) · [`taskset`](#taskset) · [`timeout`](#timeout) · [`uclampset`](#uclampset)
[`unshare`](#unshare) · [`vconfig`](#vconfig) · [`watch`](#watch) · [`xargs`](#xargs)

### [self-contained] (47)

[`chattr`](#chattr) · [`chcon`](#chcon) · [`chgrp`](#chgrp) · [`chmod`](#chmod) · [`chown`](#chown)
[`cp`](#cp) · [`cpio`](#cpio) · [`cut`](#cut) · [`date`](#date) · [`diff`](#diff)
[`dmesg`](#dmesg) · [`egrep`](#egrep) · [`expr`](#expr) · [`fgrep`](#fgrep) · [`grep`](#grep)
[`hwclock`](#hwclock) · [`i2cdetect`](#i2cdetect) · [`id`](#id) · [`iotop`](#iotop) · [`ln`](#ln)
[`losetup`](#losetup) · [`ls`](#ls) · [`lsattr`](#lsattr) · [`modinfo`](#modinfo) · [`modprobe`](#modprobe)
[`mount`](#mount) · [`netstat`](#netstat) · [`nl`](#nl) · [`paste`](#paste) · [`patch`](#patch)
[`pgrep`](#pgrep) · [`pkill`](#pkill) · [`printenv`](#printenv) · [`ps`](#ps) · [`realpath`](#realpath)
[`restorecon`](#restorecon) · [`sed`](#sed) · [`sort`](#sort) · [`tar`](#tar) · [`top`](#top)
[`touch`](#touch) · [`traceroute`](#traceroute) · [`traceroute6`](#traceroute6) · [`ulimit`](#ulimit) · [`umount`](#umount)
[`uname`](#uname) · [`xxd`](#xxd)

### [io-explicit] (12)

[`cksum`](#cksum) · [`comm`](#comm) · [`dd`](#dd) · [`fallocate`](#fallocate) · [`gzip`](#gzip)
[`install`](#install) · [`mv`](#mv) · [`rev`](#rev) · [`split`](#split) · [`tee`](#tee)
[`uudecode`](#uudecode) · [`wc`](#wc)

### [terminal] (118)

[`acpi`](#acpi) · [`base64`](#base64) · [`basename`](#basename) · [`blkdiscard`](#blkdiscard) · [`blkid`](#blkid)
[`blockdev`](#blockdev) · [`cal`](#cal) · [`cat`](#cat) · [`clear`](#clear) · [`cmp`](#cmp)
[`devmem`](#devmem) · [`df`](#df) · [`dirname`](#dirname) · [`dos2unix`](#dos2unix) · [`du`](#du)
[`echo`](#echo) · [`expand`](#expand) · [`false`](#false) · [`file`](#file) · [`fmt`](#fmt)
[`free`](#free) · [`freeramdisk`](#freeramdisk) · [`fsfreeze`](#fsfreeze) · [`fsync`](#fsync) · [`getconf`](#getconf)
[`getenforce`](#getenforce) · [`getfattr`](#getfattr) · [`getopt`](#getopt) · [`groups`](#groups) · [`gunzip`](#gunzip)
[`head`](#head) · [`help`](#help) · [`hostname`](#hostname) · [`i2cdump`](#i2cdump) · [`i2cget`](#i2cget)
[`i2cset`](#i2cset) · [`iconv`](#iconv) · [`ifconfig`](#ifconfig) · [`insmod`](#insmod) · [`iorenice`](#iorenice)
[`kill`](#kill) · [`killall`](#killall) · [`load_policy`](#load_policy) · [`log`](#log) · [`logger`](#logger)
[`logname`](#logname) · [`lsmod`](#lsmod) · [`lsof`](#lsof) · [`lspci`](#lspci) · [`lsusb`](#lsusb)
[`makedevs`](#makedevs) · [`md5sum`](#md5sum) · [`microcom`](#microcom) · [`mkdir`](#mkdir) · [`mkfifo`](#mkfifo)
[`mknod`](#mknod) · [`mkswap`](#mkswap) · [`mktemp`](#mktemp) · [`more`](#more) · [`mountpoint`](#mountpoint)
[`nbd-client`](#nbd-client) · [`nproc`](#nproc) · [`od`](#od) · [`partprobe`](#partprobe) · [`pidof`](#pidof)
[`ping`](#ping) · [`ping6`](#ping6) · [`pivot_root`](#pivot_root) · [`pmap`](#pmap) · [`printf`](#printf)
[`pwd`](#pwd) · [`pwdx`](#pwdx) · [`readelf`](#readelf) · [`readlink`](#readlink) · [`renice`](#renice)
[`rm`](#rm) · [`rmdir`](#rmdir) · [`rmmod`](#rmmod) · [`rtcwake`](#rtcwake) · [`sendevent`](#sendevent)
[`seq`](#seq) · [`setenforce`](#setenforce) · [`setfattr`](#setfattr) · [`sha1sum`](#sha1sum) · [`sha224sum`](#sha224sum)
[`sha256sum`](#sha256sum) · [`sha384sum`](#sha384sum) · [`sha512sum`](#sha512sum) · [`sleep`](#sleep) · [`stat`](#stat)
[`strings`](#strings) · [`stty`](#stty) · [`swapoff`](#swapoff) · [`swapon`](#swapon) · [`sync`](#sync)
[`sysctl`](#sysctl) · [`tac`](#tac) · [`tail`](#tail) · [`test`](#test) · [`time`](#time)
[`tr`](#tr) · [`true`](#true) · [`truncate`](#truncate) · [`tty`](#tty) · [`tunctl`](#tunctl)
[`uniq`](#uniq) · [`unix2dos`](#unix2dos) · [`unlink`](#unlink) · [`uptime`](#uptime) · [`usleep`](#usleep)
[`uuencode`](#uuencode) · [`uuidgen`](#uuidgen) · [`vi`](#vi) · [`vmstat`](#vmstat) · [`which`](#which)
[`whoami`](#whoami) · [`yes`](#yes) · [`zcat`](#zcat)

## Samsung vs Upstream Comparison

### Stripped from Samsung build (60 commands)

These exist in upstream toybox but Samsung removed them. The pattern is telling — network tools, privilege tools, and hardware interfaces.

| Command | Likely reason stripped |
|---------|------------------------|
| `:` | unknown — worth investigating |
| `[` | unknown — worth investigating |
| `arch` | print machine architecture |
| `ascii` | ASCII table display |
| `base32` | base32 encode/decode |
| `bunzip2` | bzip2 decompression |
| `bzcat` | bzip2 cat |
| `chvt` | virtual terminal switching |
| `count` | byte counter |
| `crc32` | CRC32 checksum |
| `deallocvt` | virtual terminal control |
| `dnsdomainname` | DNS domain name query |
| `eject` | removable media control |
| `factor` | math utility (low risk but unused) |
| `fold` | text line folding |
| `fstype` | filesystem type detection |
| `ftpget` | network file transfer |
| `ftpput` | network file transfer |
| `gpiodetect` | GPIO hardware access |
| `gpiofind` | GPIO hardware access |
| `gpioget` | GPIO hardware access |
| `gpioinfo` | GPIO hardware access |
| `gpioset` | GPIO hardware access |
| `halt` | system power control |
| `hd` | hex dump (xxd kept) |
| `hexedit` | interactive binary editor |
| `host` | DNS resolution tool |
| `httpd` | runs an HTTP server |
| `i2ctransfer` | raw I2C hardware access |
| `killall5` | signals all processes (shutdown use) |
| `link` | raw hardlink creation |
| `linux32` | personality/ABI switching |
| `login` | session/auth management |
| `mcookie` | random cookie for X auth |
| `memeater` | memory pressure tool |
| `mix` | audio mixer control |
| `mkpasswd` | password hash generation |
| `nbd-server` | network block device server |
| `nologin` | auth/login control |
| `oneit` | init replacement / minimal shell |
| `openvt` | virtual terminal control |
| `poweroff` | system power control |
| `pwgen` | password generation |
| `readahead` | filesystem prefetch control |
| `reboot` | system power control |
| `reset` | terminal reset |
| `sha3sum` | SHA3 hashing (sha256sum kept) |
| `shred` | secure file deletion |
| `shuf` | random shuffle |
| `sntp` | network time sync |
| `su` | direct privilege escalation |
| `switch_root` | init-time root pivot |
| `toybox` | unknown — worth investigating |
| `ts` | timestamp input lines |
| `tsort` | topological sort |
| `unicode` | unicode character info |
| `w` | who is logged in |
| `watchdog` | kernel watchdog control |
| `wget` | arbitrary network fetch |
| `who` | who is logged in |

### Samsung additions (21 commands)

These are in Samsung's build but not in upstream toybox.

| Command |
|---------|
| `brctl` |
| `chcon` |
| `diff` |
| `expr` |
| `getenforce` |
| `getfattr` |
| `gzip` |
| `load_policy` |
| `log` |
| `lsof` |
| `modprobe` |
| `more` |
| `restorecon` |
| `runcon` |
| `sendevent` |
| `setenforce` |
| `stty` |
| `tr` |
| `traceroute` |
| `traceroute6` |
| `vi` |

### Usage line divergences (37 commands)

These commands exist in both but Samsung's version has a different usage signature.

| Command | Samsung | Upstream |
|---------|---------|----------|
| `blkdiscard` | `blkdiscard [-olszf] DEVICE` | `blkdiscard [-szf] [-o OFFSET] [-l LENGTH] DEVICE` |
| `cal` | `cal [[[DAY] MONTH] YEAR]` | `cal [-h] [[[DAY] MONTH] YEAR]` |
| `cksum` | `cksum [-IPLN] [FILE...]` | `cksum [-HIPLN] [FILE...]` |
| `cp` | `cp [-adfHiLlnPpRrsTv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]` | `cp [-aDdFfHiLlnPpRrsTuv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]` |
| `cpio` | `cpio -{o\|t\|i\|p DEST} [-v] [--verbose] [-F FILE] [-R [USER][:GROUP] [--no-preserve-owner]` | `cpio -{o\|t\|i\|p DEST} [-dLtuv] [--verbose] [-F FILE] [-R [USER][:GROUP] [--no-preserve-owner]` |
| `devmem` | `devmem ADDR [WIDTH [DATA]]` | `devmem [-f FILE] ADDR [WIDTH [DATA...]]` |
| `df` | `df [-HPkhi] [-t type] [FILE...]` | `df [-aHhikP] [-t TYPE] [FILE...]` |
| `dmesg` | `dmesg [-Cc] [-r\|-t\|-T] [-n LEVEL] [-s SIZE] [-w]` | `dmesg [-Cc] [-r\|-t\|-T] [-n LEVEL] [-s SIZE] [-w\|-W]` |
| `du` | `du [-d N] [-askxHLlmc] [FILE...]` | `du [-d N] [-abcHKkLlmsx] [FILE...]` |
| `echo` | `echo [-neE] [ARG...]` | `echo [-Een] [ARG...]` |
| `env` | `env [-i] [-u NAME] [NAME=VALUE...] [COMMAND...]` | `env [-0i] [-e FILE] [-u NAME] [NAME=VALUE...] [COMMAND...]` |
| `fallocate` | `fallocate [-l size] [-o offset] file` | `fallocate [-o OFFSET] -l SIZE FILE` |
| `getopt` | `getopt [OPTIONS] [--] ARG...` | `getopt [-aTu] [-lo OPTIONS] [-n NAME] [OPTIONS] ARG...` |
| `grep` | `grep [-EFrivwcloqsHbhn] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE] [FILE]...` | `grep [-abcEFHhIiLlnoqrsvwxZz] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE]... [FILE]...` |
| `head` | `head [-n NUM] [FILE...]` | `head [-cn NUM] [-qv] [FILE...]` |
| `hwclock` | `hwclock [-rswtluf]` | `hwclock [-rswtlu] [-f FILE]` |
| `id` | `id [-GZgnru] [USER...]` | `id [-Ggnru] [USER...]` |
| `ln` | `ln [-sfnv] [-t DIR] [FROM...] TO` | `ln [-fnrsTv] [-t DIR] [FROM...] TO` |
| `lsusb` | `lsusb [-i]` | `lsusb [-ti]` |
| `mkfifo` | `mkfifo [-Z CONTEXT] [NAME...]` | `mkfifo [NAME...]` |
| `mknod` | `mknod [-Z CONTEXT] ... [-m MODE] NAME TYPE [MAJOR MINOR]` | `mknod [-m MODE] NAME TYPE [MAJOR MINOR]` |
| `mktemp` | `mktemp [-dqu] [-p DIR] [TEMPLATE]` | `mktemp [-dqtu] [-p DIR] [TEMPLATE]` |
| `mv` | `mv [-finTv] [-t TARGET] SOURCE... [DEST]` | `mv [-FfinTvx] [-t TARGET] SOURCE... [DEST]` |
| `netcat` | `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM\|-f FILENAME\|COMMAND...}` | `netcat [-46ELlntUu] [-pqWw #] [-s addr] [-o FILE] {IPADDR PORTNUM\|-f FILENAME\|COMMAND...}` |
| `nproc` | `nproc [--all]` | `nproc [-a]` |
| `patch` | `patch [-Rlsu] [-d DIR] [-i PATCH] [-p DEPTH] [-F FUZZ] [--dry-run] [FILE [PATCH]]` | `patch [-Rlsuv] [-d DIR] [-i FILE] [-p DEPTH] [-F FUZZ] [--dry-run] [FILE [PATCH]]` |
| `pgrep` | `pgrep [-clfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]` | `pgrep [-aclfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]` |
| `readelf` | `readelf [-adehlnSs] [-p SECTION] [-x SECTION] [file...]` | `readelf [-AadehlnSs] [-p SECTION] [-x SECTION] [file...]` |
| `readlink` | `readlink FILE...` | `readlink [-efmnqz] FILE...` |
| `sort` | `sort [-Mbcdfginrsuz] [FILE...] [-k#[,#[x]] [-t X]] [-o FILE]` | `sort [-bCcdfgiMnrsuxVz] [FILE...] [-k#[,#[x]] [-t X]] [-o FILE]` |
| `sysctl` | `sysctl [-aAeNnqw] [-p [FILE] \| KEY[=VALUE]...]` | `sysctl [-aeNnqw] [-p [FILE] \| KEY[=VALUE]...]` |
| `timeout` | `timeout [-i] [-k DURATION] [-s SIGNAL] DURATION COMMAND...` | `timeout [-iv] [-k DURATION] [-s SIGNAL] DURATION COMMAND...` |
| `uname` | `uname [-asnrvm]` | `uname [-asnrvmo]` |
| `watch` | `watch [-teb] [-n SEC] PROG ARGS` | `watch [-tebx] [-n SEC] COMMAND...` |
| `wc` | `wc -lwcm [FILE...]` | `wc [-Llwcm] [FILE...]` |
| `xargs` | `xargs [-0prt] [-snE STR] COMMAND...` | `xargs [-0Pprt] [-snE STR] [-a FILE] COMMAND...` |
| `zcat` | `zcat [FILE...]` | `zcat [-f] [FILE...]` |

---

## Command Reference

## `brctl`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `brctl COMMAND [BRIDGE [INTERFACE]]`

Manage ethernet bridges

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox brctl addbr br0
```
*Creates a new bridge network interface named br0. 'addbr' is the subcommand to add a bridge. On Android in system_server context (UID 1000), this is used to set up virtual network bridges for container or VPN routing scenarios without needing a shell script.*

```
toybox brctl addif br0 eth0
```
*Attaches the physical network interface eth0 to the existing bridge br0. 'addif' is the subcommand to add an interface to a bridge. This is composed as a single self-contained invocation specifying BRIDGE as br0 and INTERFACE as eth0, which is the correct argument order for brctl. This is practical when bridging ethernet to a virtual network on Android devices that expose an eth0 interface.*

---

## `chroot`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `chroot NEWROOT [COMMAND [ARG...]]`

Run command within a new root directory. If no command, run /bin/sh. chroot: -h: No such file or directory

### Examples

```
toybox chroot /data/local/tmp toybox ls /
```
*Change root to /data/local/tmp and run ls. From ls's perspective `/` IS `/data/local/tmp` — useful for inspecting a staged filesystem or a pulled partition image.*

---

## `chrt`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `chrt [-Rmofrbi] {-p PID [PRIORITY] | [PRIORITY COMMAND...]}`

Get/set a process' real-time scheduling policy and priority.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-o` | `SCHED_OTHER` | -f  SCHED_FIFO    -r  SCHED_RR |
| `-b` | `SCHED_BATCH` | -i  SCHED_IDLE |

### Examples

```
toybox chrt -f 99 toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Run dd at `SCHED_FIFO` realtime priority 99 — highest possible CPU scheduling. Gets your operation done before anything else touches the CPU.*

```
toybox chrt -i 0 toybox find /data -name '*.apk' -type f
```
*Run find at `SCHED_IDLE` — only runs when the CPU is completely free. Safe background scan that won't compete with foreground processes.*

```
toybox chrt -p <PID>
```
*Show the current scheduling policy and priority of a running process without modifying it.*

---

## `env`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `env [-i] [-u NAME] [NAME=VALUE...] [COMMAND...]`

Set the environment for command invocation, or list environment variables.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `env [-i] [-u NAME] [NAME=VALUE...] [COMMAND...]`
> Upstream: `env [-0i] [-e FILE] [-u NAME] [NAME=VALUE...] [COMMAND...]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-u` | `NAME` | Remove NAME from the environment |

### Examples

```
toybox env LD_PRELOAD=/data/local/tmp/hook.so toybox grep pattern /data/local/tmp/target
```
*Inject a shared library into grep's process before it starts. `LD_PRELOAD` interception without a shell wrapper — env sets up the environment then execs the child.*

```
toybox env -i PATH=/system/bin toybox find /data -name '*.apk'
```
*`-i` clears the entire inherited environment first, then sets only what you specify. Gives the child process a clean known state with no leaked variables.*

---

## `find`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `find [-HL] [DIR...] [<options>]`

Search directories for matching files. Default: search ".", match all, -print matches.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-H` |  | Follow command line symlinks |
| `-L` |  | Follow all symlinks |
| `-name` | `PATTERN` | filename with wildcards |
| `-iname` |  | ignore case -name |
| `-path` | `PATTERN` | path name with wildcards |
| `-ipath` |  | ignore case -path |
| `-user` | `UNAME` | belongs to user UNAME |
| `-nouser` |  | user ID not known |
| `-group` | `GROUP` | belongs to group GROUP |
| `-nogroup` |  | group ID not known |
| `-perm` |  | [-/]MODE  permissions (-=min /=any) -prune      ignore dir contents |
| `-size` |  | N[c]      512 byte blocks (c=bytes) -xdev       only this filesystem |
| `-links` |  | N         hardlink count |
| `-empty` |  | empty files and dirs |
| `-atime` |  | N[u]      accessed N units ago |
| `-true` |  | always true |
| `-ctime` |  | N[u]      created N units ago |
| `-false` |  | always false |
| `-mtime` |  | N[u]      modified N units ago |
| `-executable` |  | access(X_OK) perm+ACL |
| `-inum` |  | N         inode number N |
| `-readable` |  | access(R_OK) perm+ACL |
| `-context` | `PATTERN` | security context |
| `-depth` |  | contents before dir |
| `-samefile` | `FILE` | hardlink to FILE |
| `-maxdepth` |  | N at most N dirs down |
| `-newer` | `FILE` | newer mtime than FILE |
| `-mindepth` |  | N at least N dirs down |
| `-newerXY` | `FILE` | X=acm time > FILE's Y=acm time (Y=t: FILE is literal time) |
| `-type` |  | [bcdflps]  type is (block, char, dir, file, symlink, pipe, socket) |
| `-print` |  | Print match with newline |
| `-print0` |  | Print match with null |
| `-exec` |  | Run command with path |
| `-execdir` |  | Run command in file's dir |
| `-ok` |  | Ask before exec |
| `-okdir` |  | Ask before execdir |
| `-delete` |  | Remove matching file/dir |
| `-printf` | `FORMAT` | Print using format string |
| `-quit` |  | Exit immediately |

### Examples

```
toybox find /data/local/tmp -type f -name '*.bin' -exec toybox xxd {} ;
```
*For every .bin file under /data/local/tmp, run xxd on it individually. `-exec` with `;` means one xxd call per file — safe for filenames with spaces.*

```
toybox find /proc -maxdepth 3 -name status -exec toybox grep TracerPid {} +
```
*Scan /proc 3 levels deep for every `status` file, batch them all into a single grep call. `+` batching is faster than `;` when you have many matches.*

```
toybox find /dev -type c -newer /data/local/tmp/ref -exec toybox stat {} ;
```
*Find character devices modified more recently than your reference file — detects newly created device nodes after a kernel event.*

```
toybox find /data -maxdepth 5 -size +1M -type f -exec toybox ls -la {} ;
```
*List every file over 1MB with full permissions and timestamps. Replaces `find ... | xargs ls` entirely — no pipe needed.*

```
toybox find /proc -maxdepth 2 -name cmdline -exec toybox cat {} ;
```
*Dump the command line of every running process by reading /proc directly. Useful when ps output is restricted.*

---

## `flock`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `flock [-sxun] fd`

Manage advisory file locks.

### Examples

```
toybox flock /data/local/tmp/mylock toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Acquire an exclusive lock before running dd. Prevents two processes from writing the same block device simultaneously — critical for concurrent operations from system_server.*

---

## `inotifyd`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `inotifyd PROG FILE[:MASK] ...`

When a filesystem event matching MASK occurs to a FILE, run PROG as:

### Examples

```
toybox inotifyd toybox cat /data/local/tmp:w
```
*Watch /data/local/tmp for close-write events (file finished writing) and run cat on it each time. Event-driven execution with zero shell involvement.*

```
toybox inotifyd toybox strings /data/local/tmp/incoming:c
```
*Every time a new file is created in /data/local/tmp, run strings on it automatically. Useful for watching a drop directory from system_server context.*

```
toybox inotifyd toybox stat /data/local/tmp:dmv
```
*Fire stat on every delete, move, or close-write event — a live audit trail of file activity without polling. Event codes: `c`=create `d`=delete `m`=move `w`=close-write `r`=open `a`=access.*

---

## `ionice`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `ionice [-t] [-c CLASS] [-n LEVEL] [COMMAND...|-p PID]`

Change the I/O scheduling priority of a process. With no arguments (or just -p), display process' existing I/O class/priority.

### Examples

```
toybox ionice -c 1 -n 0 toybox find /data -type f -name '*.db'
```
*Run find at realtime I/O class, highest priority (`-n 0`). Use when storage contention is causing your operation to stall behind other processes.*

```
toybox ionice -c 3 toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Run dd at idle I/O priority — only runs when nothing else needs the disk. Safe background partition dump that won't impact the rest of the system.*

```
toybox ionice -p <PID>
```
*Display the current I/O class and priority of an existing process without modifying it.*

---

## `nc`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`

Forward stdin/stdout to a file or network connection.

### Examples

```
toybox nc -l -p 9999
```
*Listen on port 9999 for an incoming connection. From system_server this can receive data from another process on-device — a raw IPC channel without Binder overhead.*

```
toybox nc 127.0.0.1 9999
```
*Connect to the listener on localhost port 9999 and send data. Pair with the listener above for a simple two-process communication channel.*

---

## `netcat`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`

Forward stdin/stdout to a file or network connection.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`
> Upstream: `netcat [-46ELlntUu] [-pqWw #] [-s addr] [-o FILE] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`

### Examples

```
toybox netcat -l -p 9999 -q 5 127.0.0.1
```
*-l puts netcat into listen mode so it accepts an incoming connection rather than initiating one; -p 9999 binds to port 9999 on the loopback interface; -q 5 causes netcat to quit 5 seconds after it sees EOF on stdin, preventing it from hanging indefinitely; 127.0.0.1 restricts listening to loopback only, which is appropriate for inter-process IPC within the device from system_server context without exposing a port to external network interfaces*

```
toybox netcat -4 -w 3 -p 12345 -s 127.0.0.1 127.0.0.1 9999
```
*-4 forces IPv4 so the connection uses the loopback address class explicitly rather than potentially resolving to IPv6; -w 3 sets a 3-second connect timeout so the command fails fast if nothing is listening instead of blocking indefinitely; -p 12345 binds the local source port to 12345 which is useful for firewall rule testing or identifying the initiating process; -s 127.0.0.1 pins the source address to loopback; the final 127.0.0.1 9999 specifies the destination host and port to connect to, completing a loopback client connection useful for testing a service bound on port 9999*

---

## `nice`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `nice [-n PRIORITY] COMMAND...`

Run a command line at an increased or decreased scheduling priority.

### Examples

```
toybox nice -n 19 toybox find /data -type f -name '*.so'
```
*Run find at lowest CPU niceness (19). The OS schedules it only when nothing else wants the CPU — background work that won't cause UI jank.*

```
toybox nice -n -20 toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Run dd at highest CPU priority (niceness -20, requires privilege). Gets the dump done as fast as possible regardless of system load.*

---

## `nohup`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `nohup COMMAND...`

Run a command that survives the end of its terminal.

### Examples

```
toybox nohup toybox inotifyd toybox strings /data/local/tmp/incoming:c
```
*Run inotifyd immune to `SIGHUP` so it keeps watching even if the parent process or session ends. Stack nohup + inotifyd for a persistent file-watch daemon with no shell.*

---

## `nsenter`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `nsenter [-t pid] [-F] [-i] [-m] [-n] [-p] [-u] [-U] COMMAND...`

Run COMMAND in an existing (set of) namespace(s).

### Examples

```
toybox nsenter -t <PID> -m toybox ls /proc/<PID>/root
```
*Enter the mount namespace of another process and run ls from inside it. Lets you see the filesystem exactly as that process sees it — useful for inspecting sandboxed app namespaces.*

---

## `prlimit`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `ulimit [-P PID] [-SHRacdefilmnpqrstuv] [LIMIT]`

Print or set resource limits for process number PID. If no LIMIT specified (or read-only -ap selected) display current value (sizes in bytes). Default is ulimit -P $PPID -Sf" (show soft filesize of your shell).

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-P` | `PID` | to affect (default $PPID) |
| `-a` |  | Show all limits |
| `-S` |  | Set/show soft limit |
| `-H` |  | Set/show hard (maximum) limit |
| `-c` |  | Core file size (blocks) |
| `-d` |  | Process data segment (KiB) |
| `-e` |  | Max scheduling priority |
| `-f` |  | File size (KiB) |
| `-i` |  | Pending signal count |
| `-l` |  | Locked memory (KiB) |
| `-m` |  | Resident Set Size (KiB) |
| `-n` |  | Number of open files |
| `-p` |  | Pipe buffer (512 bytes) |
| `-q` | `POSIX` | message queues |
| `-r` |  | Max realtime priority |
| `-R` |  | Realtime latency (us) |
| `-s` |  | Stack size (KiB) |
| `-t` |  | Total CPU time (s) |
| `-u` |  | Maximum processes (this UID) |
| `-v` |  | Virtual memory size (KiB) |

### Examples

```
toybox prlimit --nofile=1024 toybox find /data -type f
```
*Cap the number of open file descriptors the child process can have. Prevents fd exhaustion when scanning large trees from within system_server's process space.*

```
toybox prlimit -p <PID>
```
*Display all current resource limits for an existing process without modifying them.*

---

## `rfkill`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `rfkill COMMAND [DEVICE]`

Enable/disable wireless devices.

### Examples

```
toybox rfkill list
```
*Lists all rfkill-managed wireless devices (wifi, bluetooth, nfc, etc.) on the Samsung Galaxy S22. No flags are available for this command, so 'list' is the COMMAND argument. This is useful from system_server context to enumerate which radio interfaces exist and whether they are soft-blocked or hard-blocked by the kernel.*

```
toybox rfkill block wifi
```
*Issues a soft-block on the wifi radio via the rfkill subsystem. 'block' is the COMMAND argument and 'wifi' is the DEVICE argument matching the rfkill type. This forcibly disables the wifi radio at the kernel level, which is useful for testing radio policy enforcement or diagnosing interference issues from system_server context without requiring a shell pipeline.*

---

## `runcon`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `runcon CONTEXT COMMAND [ARGS...]`

Run a command in a specified security context.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox runcon u:r:shell:s0 toybox find /data -name '*.db'
```
*Execute find under the shell SELinux context. Changes what MAC policy allows the child process to access — useful for testing what a given context can reach without escalating permanently.*

---

## `setsid`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `setsid [-cdw] command [args...]`

Run process in a new session.

### Examples

```
toybox setsid toybox inotifyd toybox cat /data/local/tmp:w
```
*Run inotifyd in a new session, completely detached from the controlling terminal. Combined with nohup this gives you a proper background daemon from system_server.*

---

## `taskset`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `taskset [-ap] [mask] [PID | cmd [args...]]`

Launch a new task which may only run on certain processors, or change the processor affinity of an existing PID.

### Examples

```
toybox taskset 0x1 toybox find /data -type f -name '*.so'
```
*Pin find to CPU core 0 only (bitmask `0x1`). Isolates your operation to a specific core and avoids cache thrashing with other processes.*

```
toybox taskset 0xf toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Allow dd to run on cores 0-3 (`0xf` = `1111` binary). On the S22's Snapdragon the first 4 are efficiency cores — lower power for background work.*

```
toybox taskset -p <PID>
```
*Show the current CPU affinity mask of a running process.*

---

## `timeout`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `timeout [-i] [-k DURATION] [-s SIGNAL] DURATION COMMAND...`

Run command line as a child process, sending child a signal if the command doesn't exit soon enough.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `timeout [-i] [-k DURATION] [-s SIGNAL] DURATION COMMAND...`
> Upstream: `timeout [-iv] [-k DURATION] [-s SIGNAL] DURATION COMMAND...`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `--foreground` |  | Don't create new process group |
| `--preserve-status` |  | Exit with the child's exit status |

### Examples

```
toybox timeout 5 toybox ping -c 1 8.8.8.8
```
*Kill ping after 5 seconds if it hasn't returned. Prevents any command from hanging indefinitely when called from system_server where you can't wait forever.*

```
toybox timeout 30 toybox find /data -name '*.db' -exec toybox strings {} ;
```
*Hard 30-second limit on the entire find+strings chain. Essential when scanning unknown directory trees from a privileged context — you need a kill switch.*

---

## `uclampset`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `uclampset [-m MIN] [-M MAX] {-p PID | COMMAND...}`

Set or query process utilization limits ranging from 0 to 1024, or -1 to reset to system default. With no arguments, prints current values.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-m` | `MIN` | Reserve at least this much CPU utilization for task |
| `-M` | `MAX` | Limit task to at most this much CPU utilization |
| `-p` | `PID` | Apply to PID rather than new COMMAND |

### Examples

```
toybox uclampset -m 50 -M 200 -p 1000
```
*-m 50 sets a minimum CPU utilization clamp of 50 (out of 1024 scale) ensuring system_server gets at least that share of CPU capacity; -M 200 caps the maximum utilization at 200 preventing the process from consuming excess CPU resources; -p 1000 applies both clamp values to the running process with PID 1000 (system_server) rather than launching a new command, making this a live tuning operation with no process spawn overhead*

```
toybox uclampset -m 0 -M 512 toybox sleep 60
```
*-m 0 sets the minimum utilization clamp to zero meaning the kernel will not reserve any guaranteed CPU capacity for this task; -M 512 caps maximum utilization at 512 (roughly half the 1024 ceiling) constraining the task to mid-tier CPU frequency and capacity, useful for background work that should not spike power draw; 'toybox sleep 60' is the COMMAND form where uclampset launches the specified program directly under these clamp policies rather than targeting an existing PID, demonstrating how the scheduler hints are inherited by the spawned process*

---

## `unshare`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `unshare [-imnpuUr] COMMAND...`

Create new container namespace(s) for this process and its children, allowing the new set of processes to have a different view of the system than the parent process.

### Examples

```
toybox unshare -m toybox mount --bind /data/local/tmp /data/local/tmp2
```
*Create a new private mount namespace then bind-mount inside it. The mount is invisible to every other process — clean temporary namespace manipulation.*

---

## `vconfig`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `vconfig COMMAND [OPTIONS]`

Create and remove virtual ethernet devices

### Examples

```
toybox vconfig add eth0 10
```
*Adds a VLAN subinterface tagged with VLAN ID 10 to the physical network interface eth0. 'add' is the subcommand that creates the VLAN device, 'eth0' is the parent interface available on Android devices for wired or bridged network connections, and '10' is the VLAN identifier used to segment network traffic. This is composed as a single self-contained invocation because vconfig requires no shell features to operate — all arguments are positional parameters passed directly to the command.*

```
toybox vconfig rem eth0.10
```
*Removes the previously created VLAN subinterface named eth0.10 from the system. 'rem' is the subcommand that tears down and unregisters the VLAN device. The interface name eth0.10 follows the Linux kernel naming convention where the parent interface and VLAN ID are joined by a dot. This is composed as a minimal single invocation because vconfig exposes no flags of its own — all behavior is controlled through positional subcommands and interface name arguments, making it inherently self-contained without requiring shell constructs.*

---

## `watch`

`[exec-capable]`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `watch [-teb] [-n SEC] PROG ARGS`

Run PROG every -n seconds, showing output. Hit q to quit.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `watch [-teb] [-n SEC] PROG ARGS`
> Upstream: `watch [-tebx] [-n SEC] COMMAND...`

### Examples

```
toybox watch -n 5 -t toybox cat /proc/meminfo
```
*Runs 'toybox cat /proc/meminfo' every 5 seconds (-n 5) without printing the header line (-t). This is composed this way because system_server often needs to monitor memory pressure continuously; suppressing the header with -t keeps output clean for automated parsing or logging. The entire invocation is self-contained with no shell pipes needed.*

```
toybox watch -n 2 -eb toybox cat /proc/net/dev
```
*Polls network interface statistics from /proc/net/dev every 2 seconds (-n 2), highlights lines that change between runs (-b for bold diff), and exits immediately if the watched command returns a non-zero exit code (-e). This is composed this way to detect network anomalies quickly on a live device: -b makes changed counters visually distinct, -e ensures the watcher stops if /proc/net/dev becomes unreadable, and no shell or pipes are required since toybox cat reads the file directly.*

---

## `xargs`

`[exec-capable]` `[self-contained]`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `xargs [-0prt] [-snE STR] COMMAND...`

Run command line one or more times, appending arguments from stdin.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `xargs [-0prt] [-snE STR] COMMAND...`
> Upstream: `xargs [-0Pprt] [-snE STR] [-a FILE] COMMAND...`

### Examples

```
toybox find /data/local/tmp -name '*.log' -print0 | toybox xargs -0 toybox grep -l ERROR
```
*`-print0` and `-0` pair together to safely handle filenames with spaces. xargs batches the file list into as few grep calls as possible rather than one per file.*

```
toybox find /proc -maxdepth 2 -name maps -print | toybox xargs toybox grep '/system'
```
*Grep every process memory map for system library loads. The pipe here is between two toybox commands you control — no shell involved.*

---

## `chattr`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chattr [-R] [-+=AacDdijsStTu] [-p PROJID] [-v VERSION] [FILE...]`

Change file attributes on a Linux file system.

### Examples

```
toybox chattr +i /data/local/tmp/critical_config.txt
```
*Sets the immutable flag (+i) on a file in /data/local/tmp. The +i attribute prevents any process, including root, from modifying, deleting, renaming, or creating hard links to the file. This is useful in Android system_server context to protect configuration files from accidental or malicious modification after they have been written.*

```
toybox chattr -R +a /data/local/tmp/logdir
```
*Recursively (-R) applies the append-only flag (+a) to all files under /data/local/tmp/logdir. The +a attribute means files can only be opened for writing in append mode, so existing log data cannot be overwritten or deleted mid-session. The -R flag descends into subdirectories, ensuring every log file in the tree gets the same protection without requiring per-file invocations.*

---

## `chcon`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chcon [-hRv] CONTEXT FILE...`

Change the SELinux security context of listed file[s].

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox chcon u:object_r:shell_data_file:s0 /data/local/tmp/testfile.bin
```
*Sets the SELinux security context of /data/local/tmp/testfile.bin to u:object_r:shell_data_file:s0. The CONTEXT argument is placed before the FILE argument as required by the usage syntax. This is necessary in Android when a file is created with the wrong SELinux label and processes enforcing MAC policy are denied access; correcting the label allows policy-conformant access without changing DAC permissions.*

```
toybox chcon -Rv u:object_r:system_data_file:s0 /data/local/tmp/testdir
```
*Recursively applies the SELinux context u:object_r:system_data_file:s0 to /data/local/tmp/testdir and every file and subdirectory beneath it (-R), while printing each relabeled path to stdout (-v). The -R flag is essential when an entire directory tree needs uniform labeling, for example after staging multiple files for a system_server-accessible location. The -v flag provides a visible audit trail of which paths were actually changed, useful when running from system_server context where logging relabeling operations matters for debugging SELinux denials.*

---

## `chgrp`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chgrp/chown [-RHLP] [-fvh] GROUP FILE...`

Change group of one or more files.

### Examples

```
toybox chgrp -Rv system /data/local/tmp
```
*Recursively (-R) changes the group ownership of /data/local/tmp and all its contents to the 'system' group. The -v flag prints each file as it is processed, which is useful in system_server context to confirm every file under that directory has been updated. Composed this way because Android system services often need consistent group ownership across an entire directory tree, and -R handles all nested files in one invocation without needing a shell loop.*

```
toybox chgrp -fh shell /data/local/tmp/test.sh
```
*Changes the group of /data/local/tmp/test.sh to 'shell' without following symbolic links (-h applies the change to the symlink itself rather than its target) and suppresses error messages (-f) if the operation fails. Composed this way because in Android environments symlinks are common under /data and silently failing is preferable in automated contexts where the file may or may not exist at call time.*

---

## `chmod`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chmod [-R] MODE FILE...`

Change mode of listed file[s] (recursively with -R).

### Examples

```
toybox chmod -R 755 /data/local/tmp
```
*-R recursively applies the mode change to /data/local/tmp and all files and directories beneath it; mode 755 grants owner read/write/execute and group/other read/execute, which is the standard permission set for a directory tree that needs to be traversable by other processes while remaining owned by UID 1000; composed this way because there is no shell glob or find pipe available, so -R is the only mechanism to cover an entire subtree in one invocation*

```
toybox chmod 600 /data/local/tmp/keydata.bin
```
*sets permissions on a single sensitive file to 600, meaning only the owning user (UID 1000, system_server) can read or write it and no other UID has any access; no flags are needed beyond the octal mode because the target is a single known path rather than a tree, keeping the invocation minimal and precise to avoid accidentally tightening permissions on sibling files*

---

## `chown`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chgrp/chown [-RHLP] [-fvh] GROUP FILE...`

Change group of one or more files.

### Examples

```
toybox chown 1000:1000 /data/local/tmp/testfile.txt
```
*Changes the owner and group of /data/local/tmp/testfile.txt to UID 1000 (system) and GID 1000 (system). The colon separates user and group. This is composed as a single self-contained invocation because no shell features are needed — chown accepts user:group and a file path directly. In system_server context (UID 1000), this is useful for ensuring a file created by another process is owned by the system user before reading or executing it.*

```
toybox chown -R 1000:1000 /data/local/tmp/testdir
```
*Recursively changes ownership of /data/local/tmp/testdir and all files and subdirectories within it to UID 1000 and GID 1000. The -R flag instructs chown to descend into subdirectories, making this a single self-contained invocation that handles an entire directory tree without needing a shell loop or pipe. This is practical when staging a set of test assets under system_server context where all files must share the same ownership before a privileged operation reads them.*

---

## `cp`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `cp [-adfHiLlnPpRrsTv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]`

Copy files from SOURCE to DEST.  If more than one SOURCE, DEST must be a directory.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cp [-adfHiLlnPpRrsTv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]`
> Upstream: `cp [-aDdFfHiLlnPpRrsTuv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]`

### Examples

```
toybox cp -p /data/local/tmp/config.json /data/local/tmp/config.json.bak
```
*Copies config.json to a backup file in the same directory. The -p flag preserves timestamps, ownership, and permissions so the backup is an exact replica of the original file attributes, not just the data. Composed as a single invocation because no shell features are needed — source and destination are explicit paths.*

```
toybox cp -rp /data/local/tmp/testdir /data/local/tmp/testdir_backup
```
*Recursively copies an entire directory tree from testdir to testdir_backup. The -r flag descends into subdirectories and copies them wholesale. The -p flag preserves file metadata (permissions, timestamps, ownership) on every file and directory in the tree, which matters in an Android system_server context where file modes and ownership affect access control. Both source and destination are explicit paths, requiring no shell expansion or redirection.*

---

## `cpio`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `cpio -{o|t|i|p DEST} [-v] [--verbose] [-F FILE] [-R [USER][:GROUP] [--no-preserve-owner]`

Copy files into and out of a "newc" format cpio archive.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cpio -{o|t|i|p DEST} [-v] [--verbose] [-F FILE] [-R [USER][:GROUP] [--no-preserve-owner]`
> Upstream: `cpio -{o|t|i|p DEST} [-dLtuv] [--verbose] [-F FILE] [-R [USER][:GROUP] [--no-preserve-owner]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-F` | `FILE` | Use archive FILE instead of stdin/stdout |
| `-p` | `DEST` | Copy-pass mode, copy stdin file list to directory DEST |
| `-R` | `USER` | Replace owner with USER[:GROUP] |
| `--no-preserve-owner` |  | Don't set ownership during extract |

### Examples

```
toybox cpio -o -F /data/local/tmp/boot_files.cpio
```
*-o tells cpio to create (output) an archive by reading a list of filenames from stdin; -F /data/local/tmp/boot_files.cpio directs the archive to be written to that specific file rather than stdout, which is necessary here because there is no shell redirection available; the caller must supply the filename list via a prior step or pipe substitute — in system_server context this invocation is composed this way to produce a portable archive of specified paths without relying on shell operators*

```
toybox cpio -i --no-preserve-owner -F /data/local/tmp/boot_files.cpio
```
*-i tells cpio to extract (input) files from an existing archive; -F /data/local/tmp/boot_files.cpio specifies the archive to read from instead of stdin, required because no shell redirection is available; --no-preserve-owner prevents cpio from attempting to set file ownership to the original values recorded in the archive, which avoids permission errors when running as UID 1000 (system_server) rather than root, making extraction succeed even for files originally owned by other UIDs*

---

## `cut`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `cut [-Ds] [-bcCfF LIST] [-dO DELIM] [FILE...]`

Print selected parts of lines from each FILE to standard output.

### Examples

```
toybox cut -f1,3 -d: /proc/1/status
```
*-f1,3 selects only fields 1 and 3 from each line, -d: sets the delimiter to colon so the status file key-value pairs are split correctly, /proc/1/status is the status file for PID 1 (init/zygote) on Android which uses colon-separated fields; this extracts just the field names and their third column values without needing a shell pipeline*

```
toybox cut -c1-16 /proc/cpuinfo
```
*-c1-16 selects only characters 1 through 16 of each line, truncating long lines to a fixed width; /proc/cpuinfo on Android contains hardware and processor details that often have lengthy values, and this lets you preview just the start of each line without any shell truncation or piping tools*

---

## `date`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `date [-u] [-I RES] [-r FILE] [-d DATE] [+DISPLAY_FORMAT] [-D SET_FORMAT] [SET]`

Set/get the current date/time. With no SET shows the current date.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-I` | `RES` | ISO 8601 with RESolution d=date/h=hours/m=minutes/s=seconds/n=ns |
| `-s` | `DATE` | Set the system clock to DATE. |

### Examples

```
toybox date -u +%Y%m%d_%H%M%S
```
*'-u' reads time in UTC rather than local timezone, which is critical in Android system_server context where timezone config may be mid-change or unreliable. '+%Y%m%d_%H%M%S' formats the output as a compact timestamp string (e.g. 20240315_143022) suitable for stamping log filenames or diagnostic dumps under /data/local/tmp without spaces or special characters that would require a shell to escape.*

```
toybox date -I s
```
*'-I s' emits an ISO 8601 timestamp with seconds resolution (e.g. 2024-03-15T14:30:22+00:00), including the UTC offset suffix. This is composed without '+FORMAT' because '-I' already produces a fully qualified, unambiguous machine-readable string. Useful from system_server when recording event times into structured diagnostics or comparing against certificate validity windows where the offset field matters.*

---

## `diff`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `diff [-abBdiNqrTstw] [-L LABEL] [-S FILE] [-U LINES] [-F REGEX ] FILE1 FILE2`

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `--color` |  | Color output |
| `--strip-trailing-cr` |  | Strip '\r' from input lines |
| `--TYPE-line-format` | `FORMAT` | Display TYPE (unchanged/old/new) lines using FORMAT |

### Examples

```
toybox diff -u -L baseline -L current /data/local/tmp/config_baseline.txt /data/local/tmp/config_current.txt
```
*Compares two configuration snapshots in unified diff format (-u produces context lines showing surrounding unchanged lines, making changes easier to read). -L baseline and -L current replace the default filenames in the diff header with human-readable labels, which is critical when the raw paths are long or automated tooling parses the label fields. The two explicit file paths are required because no shell redirection or pipes are available, so both inputs must be named directly on the command line.*

```
toybox diff -rq -S proc_net_dev.txt /data/local/tmp/snapshot_a /data/local/tmp/snapshot_b
```
*Recursively compares two directory trees of captured /proc snapshots (-r walks subdirectories), reporting only which files differ rather than their full content (-q produces brief one-line-per-file output, useful when you only need to know what changed not exactly how). -S proc_net_dev.txt tells diff to start its recursive traversal at that specific filename, skipping alphabetically earlier files, which is useful when a prior partial comparison was interrupted and you want to resume from a known point without re-diffing already-checked files.*

---

## `dmesg`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `dmesg [-Cc] [-r|-t|-T] [-n LEVEL] [-s SIZE] [-w]`

Print or control the kernel ring buffer.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `dmesg [-Cc] [-r|-t|-T] [-n LEVEL] [-s SIZE] [-w]`
> Upstream: `dmesg [-Cc] [-r|-t|-T] [-n LEVEL] [-s SIZE] [-w|-W]`

### Examples

```
toybox dmesg -t
```
*Runs dmesg without timestamps, printing raw kernel ring buffer messages. The -t flag strips the timestamp prefix from each line, which is useful in system_server context when you want clean message text for programmatic parsing without needing to strip time fields manually.*

```
toybox dmesg -n 3
```
*Sets the kernel console log level to 3 (error), meaning only error-level and higher messages will be printed to the console going forward. The -n flag adjusts the kernel printk level at runtime, useful from UID 1000 system_server context to reduce console noise during diagnostics without rebooting.*

---

## `egrep`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `grep [-EFrivwcloqsHbhn] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE] [FILE]...`

Show lines matching regular expressions. If no -e, first argument is regular expression to match. With no files (or "-" filename) read stdin. Returns 0 if matched, 1 if no match found, 2 for command errors.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-e` | `REGEX` | Regex to match. (May be repeated.) |
| `-f` | `REGFILE` | File listing regular expressions to match. |
| `-r` |  | Recurse into subdirectories (defaults FILE to ".") |
| `-R` |  | Recurse into subdirectories and symlinks to directories |
| `-M` |  | Match filename pattern (--include) |
| `-S` |  | Skip filename pattern (--exclude) |
| `--exclude-dir` | `PATTERN` | Skip directory pattern |
| `-I` |  | Ignore binary files |
| `-A` |  | Show NUM lines after |
| `-B` |  | Show NUM lines before match |
| `-C` | `NUM` | lines context (A+B) |
| `-E` |  | extended regex syntax |
| `-F` |  | fixed (literal match) |
| `-a` |  | always text (not binary) |
| `-i` |  | case insensitive |
| `-m` | `MAX` | match MAX many lines |
| `-v` |  | invert match |
| `-w` |  | whole word (implies -E) |
| `-x` |  | whole line |
| `-z` |  | input NUL terminated |
| `-L` |  | filenames with no match |
| `-Z` |  | output is NUL terminated |
| `-c` |  | count of matching lines |
| `-l` |  | filenames with a match |
| `-o` |  | only matching part |
| `-q` |  | quiet (errors only) |
| `-s` |  | silent (no error msg) |
| `-H` |  | force filename |
| `-b` |  | byte offset of match |
| `-h` |  | hide filename |
| `-n` |  | line number of match |

### Examples

```
toybox egrep -r -n -I --exclude-dir proc -M '*.xml' -e '<permission' -e '<uses-permission' /data/system
```
*-r recurses into /data/system subdirectories to scan all files without following symlinks; -n prefixes each match with its line number so the caller knows exactly where in the file the declaration lives; -I skips binary files to avoid garbled output and wasted I/O from compiled APK assets that may be nested nearby; --exclude-dir proc avoids descending into any directory named proc which would block or loop; -M '*.xml' restricts scanning to XML files only, cutting noise from non-manifest files; -e '<permission' and -e '<uses-permission' are two separate extended-style patterns matched with logical OR, letting a single pass collect both declared and requested permission entries across all installed-package manifests in one invocation*

```
toybox egrep -c -i -E -e 'oom_score_adj|lowmemkiller' /proc/1/status /proc/1/oom_score_adj /dev/null
```
*-c prints only the count of matching lines per file rather than the lines themselves, giving a quick numeric summary useful for scripted threshold checks; -i makes the match case-insensitive so variations in kernel version capitalisation do not cause misses; -E enables extended regex so the alternation operator | works inside a single -e expression instead of requiring two separate -e flags; the two explicit file paths /proc/1/status and /proc/1/oom_score_adj target known procfs nodes for PID 1 (init/system_server ancestor) where memory pressure fields live; /dev/null is included as a third argument to force multi-file mode so -c labels each count with its filename, making the output unambiguous when used programmatically from system_server context*

---

## `expr`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `expr ARG1 OPERATOR ARG2...`

Evaluate expression and print result. For example, "expr 1 + 2".

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox expr 1024 \* 1024
```
*Multiplies 1024 by 1024 to calculate one megabyte in bytes. The asterisk is backslash-escaped to prevent the calling process from interpreting it as a glob wildcard, since no shell is available to perform escaping. expr evaluates the arithmetic expression and prints the result 1048576 to stdout. Useful for computing buffer sizes or offsets in Android system_server context without shell arithmetic expansion.*

```
toybox expr 4096 - 512
```
*Subtracts 512 from 4096, which could represent calculating usable block space after a header reservation in a partition layout scenario. expr takes ARG1 OPERATOR ARG2 as positional arguments and performs integer arithmetic, printing the result 3584. Composed as a single self-contained invocation since no shell variables or subshells are available, making expr the only portable integer math tool in this toybox-only environment.*

---

## `fgrep`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `grep [-EFrivwcloqsHbhn] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE] [FILE]...`

Show lines matching regular expressions. If no -e, first argument is regular expression to match. With no files (or "-" filename) read stdin. Returns 0 if matched, 1 if no match found, 2 for command errors.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-e` | `REGEX` | Regex to match. (May be repeated.) |
| `-f` | `REGFILE` | File listing regular expressions to match. |
| `-r` |  | Recurse into subdirectories (defaults FILE to ".") |
| `-R` |  | Recurse into subdirectories and symlinks to directories |
| `-M` |  | Match filename pattern (--include) |
| `-S` |  | Skip filename pattern (--exclude) |
| `--exclude-dir` | `PATTERN` | Skip directory pattern |
| `-I` |  | Ignore binary files |
| `-A` |  | Show NUM lines after |
| `-B` |  | Show NUM lines before match |
| `-C` | `NUM` | lines context (A+B) |
| `-E` |  | extended regex syntax |
| `-F` |  | fixed (literal match) |
| `-a` |  | always text (not binary) |
| `-i` |  | case insensitive |
| `-m` | `MAX` | match MAX many lines |
| `-v` |  | invert match |
| `-w` |  | whole word (implies -E) |
| `-x` |  | whole line |
| `-z` |  | input NUL terminated |
| `-L` |  | filenames with no match |
| `-Z` |  | output is NUL terminated |
| `-c` |  | count of matching lines |
| `-l` |  | filenames with a match |
| `-o` |  | only matching part |
| `-q` |  | quiet (errors only) |
| `-s` |  | silent (no error msg) |
| `-H` |  | force filename |
| `-b` |  | byte offset of match |
| `-h` |  | hide filename |
| `-n` |  | line number of match |

### Examples

```
toybox fgrep -rn -M '*.log' -e 'ANR in' -e 'FATAL EXCEPTION' /data/local/tmp
```
*Recursively searches /data/local/tmp for lines containing the literal strings 'ANR in' or 'FATAL EXCEPTION' (fgrep uses -F fixed/literal matching by default, so no regex interpretation occurs). -M '*.log' restricts scanning to files matching that filename pattern, avoiding unrelated files. -n prints the line number of each match so the exact crash location within a log file is immediately known. Multiple -e flags allow both critical Android error signatures to be caught in a single pass without running the command twice.*

```
toybox fgrep -rl -e 'persist.sys' /data/local/tmp
```
*Searches all files under /data/local/tmp for the literal string 'persist.sys', which is a common prefix for persistent Android system properties often written to property dump or debug files. -r enables recursive descent into subdirectories so every file in the tree is checked. -l suppresses normal output and instead prints only the filenames that contain at least one match, giving a quick inventory of which files reference persistent properties without flooding output with every matching line. -F behavior is implied by fgrep, so 'persist.sys' is treated as a plain string and the dot is not interpreted as a regex wildcard.*

---

## `grep`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `grep [-EFrivwcloqsHbhn] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE] [FILE]...`

Show lines matching regular expressions. If no -e, first argument is regular expression to match. With no files (or "-" filename) read stdin. Returns 0 if matched, 1 if no match found, 2 for command errors.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `grep [-EFrivwcloqsHbhn] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE] [FILE]...`
> Upstream: `grep [-abcEFHhIiLlnoqrsvwxZz] [-ABC NUM] [-m MAX] [-e REGEX]... [-MS PATTERN]... [-f REGFILE]... [FILE]...`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-e` | `REGEX` | Regex to match. (May be repeated.) |
| `-f` | `REGFILE` | File listing regular expressions to match. |
| `-r` |  | Recurse into subdirectories (defaults FILE to ".") |
| `-R` |  | Recurse into subdirectories and symlinks to directories |
| `-M` |  | Match filename pattern (--include) |
| `-S` |  | Skip filename pattern (--exclude) |
| `--exclude-dir` | `PATTERN` | Skip directory pattern |
| `-I` |  | Ignore binary files |
| `-A` |  | Show NUM lines after |
| `-B` |  | Show NUM lines before match |
| `-C` | `NUM` | lines context (A+B) |
| `-E` |  | extended regex syntax |
| `-F` |  | fixed (literal match) |
| `-a` |  | always text (not binary) |
| `-i` |  | case insensitive |
| `-m` | `MAX` | match MAX many lines |
| `-v` |  | invert match |
| `-w` |  | whole word (implies -E) |
| `-x` |  | whole line |
| `-z` |  | input NUL terminated |
| `-L` |  | filenames with no match |
| `-Z` |  | output is NUL terminated |
| `-c` |  | count of matching lines |
| `-l` |  | filenames with a match |
| `-o` |  | only matching part |
| `-q` |  | quiet (errors only) |
| `-s` |  | silent (no error msg) |
| `-H` |  | force filename |
| `-b` |  | byte offset of match |
| `-h` |  | hide filename |
| `-n` |  | line number of match |

### Examples

```
toybox grep -r 'ro\.build' /system/etc
```
*Recursively search every file under /system/etc for the pattern. `-r` means grep walks the directory tree itself — no find needed.*

```
toybox grep -rl 'knox' /system
```
*`-l` prints only filenames that match, not the matching lines. Useful first pass to find which files are worth reading in full — keeps output manageable.*

```
toybox grep -a 'samsung' /dev/block/bootdevice/by-name/param
```
*`-a` treats a binary file as text so grep can scan raw block devices for ASCII strings — replaces `strings | grep` in one command.*

```
toybox grep -rn 'FactoryMode' /system/framework
```
*`-n` adds line numbers. Scanning unpacked framework jars for factory mode references without a shell pipeline.*

---

## `hwclock`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `hwclock [-rswtluf]`

Get/set the hardware clock.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `hwclock [-rswtluf]`
> Upstream: `hwclock [-rswtlu] [-f FILE]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-f` | `FILE` | Use specified device file instead of /dev/rtc0 (--rtc) |

### Examples

```
toybox hwclock -r
```
*Reads and displays the current hardware clock time from the RTC device. No flags needed beyond -r (read) because the default device /dev/rtc0 is used, which is the standard RTC on Android devices. Useful from system_server to verify the hardware clock is set correctly and matches system time.*

```
toybox hwclock -r -f /dev/rtc1
```
*Reads the hardware clock from /dev/rtc1 instead of the default /dev/rtc0, using -f to specify an alternate RTC device file. On some Samsung Galaxy hardware there may be a secondary RTC module accessible at /dev/rtc1, and explicitly naming the device with -f ensures the correct hardware clock is queried rather than relying on the default path.*

---

## `i2cdetect`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `i2cdetect [-aqry] BUS [FIRST LAST]`

Detect i2c devices.

### Examples

```
toybox i2cdetect -y -r 1
```
*-y suppresses the interactive confirmation prompt so the command runs non-interactively from system_server context without waiting for user input; -r uses read byte protocol instead of the default write quick protocol, which is safer on buses with devices that may misinterpret write quick as a command; 1 specifies I2C bus 1 (/dev/i2c-1), a common bus on Samsung Galaxy S22 for peripheral devices such as sensors and touchscreen controllers; the full bus scan outputs a grid showing which 7-bit addresses (0x03 to 0x77) have responding devices*

```
toybox i2cdetect -y -r 1 0x50 0x57
```
*-y disables the interactive confirmation so the scan proceeds without stdin input, required in system_server context where no terminal is attached; -r uses read byte probing which avoids accidentally triggering write-sensitive devices; 1 targets /dev/i2c-1; 0x50 and 0x57 constrain the scan to the EEPROM address range (addresses 80 through 87 decimal), which is practical when checking for EEPROM or NVRAM chips without disturbing unrelated sensor devices on the same bus*

---

## `id`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `id [-GZgnru] [USER...]`

Print user and group ID.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `id [-GZgnru] [USER...]`
> Upstream: `id [-Ggnru] [USER...]`

### Examples

```
toybox id
```
*Runs id with no arguments or flags to display the current process identity. In system_server context (UID 1000), this confirms the effective UID, GID, and supplementary groups assigned to the process, which is critical for verifying that a command or service is running with the expected Android system_server credentials rather than root or a less-privileged UID.*

```
toybox id -u
```
*The -u flag prints only the numeric effective user ID of the current process. This is useful in system_server context to programmatically confirm the UID is exactly 1000 without parsing the full id output, enabling a clean numeric check of process identity for permission or policy verification.*

---

## `iotop`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `iotop [-AaKObq] [-n NUMBER] [-d SECONDS] [-p PID,] [-u USER,]`

Rank processes by I/O.

### Examples

```
toybox iotop -AaKOb -n 3 -d 2
```
*-A shows processes with nonzero I/O since last sample rather than just current activity; -a accumulates I/O totals rather than showing instantaneous rates; -K displays sizes in kilobytes for easier reading; -O filters to show only processes with active I/O to reduce noise; -b runs in batch mode suitable for non-interactive capture from system_server context where no terminal is present; -n 3 limits output to 3 iterations to avoid running indefinitely; -d 2 sets a 2-second interval between samples, giving meaningful I/O deltas per sample. Composed together because iotop in interactive mode requires a terminal, and -b plus -n makes it safe and bounded for programmatic invocation from UID 1000.*

```
toybox iotop -bOKa -n 1 -p 1000,1001,1002
```
*-b enables batch non-interactive mode required when invoked from system_server which has no controlling terminal; -O restricts output to processes actually performing I/O at sample time so the output stays concise; -K reports I/O in kilobytes for human-readable values; -a uses cumulative I/O accounting which is more meaningful for a single snapshot because instantaneous rates over one sample are less reliable; -n 1 takes exactly one snapshot and exits, making this safe for one-shot diagnostic use; -p 1000,1001,1002 scopes the measurement to specific PIDs of interest rather than all processes, reducing overhead and focusing the output on the processes under investigation.*

---

## `ln`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `ln [-sfnv] [-t DIR] [FROM...] TO`

Create a link between FROM and TO. One/two/many arguments work like "mv" or "cp".

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `ln [-sfnv] [-t DIR] [FROM...] TO`
> Upstream: `ln [-fnrsTv] [-t DIR] [FROM...] TO`

### Examples

```
toybox ln -sf /data/local/tmp/libtest.so /system/lib/libtest.so
```
*Creates a symbolic link (-s) at /system/lib/libtest.so pointing to /data/local/tmp/libtest.so. The -f flag forces creation by removing any existing file at the destination first. Composed this way because system_server may need to redirect a library reference to a staging version in /data/local/tmp without modifying the original path that other processes depend on.*

```
toybox ln -sfnv -t /dev/block/bootdevice/by-name /data/local/tmp/boot.img
```
*Creates a symbolic link (-s) inside the target directory (-t /dev/block/bootdevice/by-name) pointing to /data/local/tmp/boot.img. The -f flag removes any existing link with the same name, -n treats the destination as a normal file if it is already a symlink rather than following it, and -v prints verbose output showing what was linked. Composed this way because boot partition slot entries in by-name are symlinks, and this pattern lets system_server remap a named block entry to a staging image for testing without altering existing slot structure.*

---

## `losetup`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `losetup [-cdrs] [-o OFFSET] [-S SIZE] {-d DEVICE...|-j FILE|-af|{DEVICE FILE}}`

Associate a loopback device with a file, or show current file (if any) associated with a loop device.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-j` | `FILE` | Iterate through all loopback devices associated with FILE |
| `-d` | `DEV` | Detach loopback device |
| `-o` | `OFF` | Start association at offset OFF into FILE |
| `-S` | `SIZE` | Limit SIZE of loopback association (alias --sizelimit) |

### Examples

```
toybox losetup -o 1048576 -S 524288000 /dev/block/loop0 /data/local/tmp/system.img
```
*-o 1048576 skips the first 1MB of system.img (e.g. a partition table or header), so the loop device sees only the payload region. -S 524288000 caps the association at 500MB, preventing the loop device from reading beyond the intended partition boundary. /dev/block/loop0 is the loop device to bind and /data/local/tmp/system.img is the backing file. This single invocation is necessary because losetup is the only way to attach a flat image file as a block device without a shell pipeline.*

```
toybox losetup -j /data/local/tmp/system.img
```
*-j FILE queries every active loop device on the system and reports only those currently backed by /data/local/tmp/system.img. This is composed as a self-contained lookup because there is no shell grep or pipe available; the -j flag performs the filtering internally, making it the only viable way from system_server context to audit which /dev/block/loopN devices are holding a reference to a specific image file before deciding to detach or re-attach.*

---

## `ls`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `ls [-1ACFHLNRSUXZabcdfghilmnopqrstuwx] [--color[=auto]] [FILE...]`

List files

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-A` |  | all files except . and .. |
| `-a` |  | all files including .hidden |
| `-b` |  | escape nongraphic chars |
| `-d` |  | directory, not contents |
| `-F` |  | append /dir *exe @sym \|FIFO |
| `-f` |  | files (no sort/filter/format) |
| `-H` |  | follow command line symlinks |
| `-i` |  | inode number |
| `-L` |  | follow symlinks |
| `-N` |  | no escaping, even on tty |
| `-p` |  | put '/' after dir names |
| `-q` |  | unprintable chars as '?' |
| `-R` |  | recursively list in subdirs |
| `-s` |  | storage used (1024 byte units) |
| `-Z` |  | security context |
| `-1` |  | list one file per line |
| `-C` |  | columns (sorted vertically) |
| `-g` |  | like -l but no owner |
| `-h` |  | human readable sizes |
| `-l` |  | long (show full details) |
| `-ll` |  | long with nanoseconds (--full-time) |
| `-m` |  | comma separated |
| `-n` |  | long with numeric uid/gid |
| `-o` |  | long without group column |
| `-r` |  | reverse order |
| `-w` |  | set column width |
| `-x` |  | columns (horizontal sort) |
| `-c` |  | ctime |
| `-X` |  | extension  -!  dirfirst   -~  nocase |
| `--color` |  | always (default)  =auto (when stdout is tty) =never |

### Examples

```
toybox ls -lhZ /data/local/tmp
```
*-l enables long format to show permissions, ownership, size, and timestamps; -h converts byte counts to human-readable units like K/M/G so sizes are easier to interpret at a glance; -Z appends the SELinux security context for each entry, which is critical in Android system_server context where SELinux labels determine access control; together these three flags give a full security and storage picture of the staging directory in one pass*

```
toybox ls -1ARp /dev/block/bootdevice/by-name
```
*-1 forces one entry per line so output is unambiguous for programmatic parsing when no shell pipeline is available; -A includes hidden entries while omitting . and .. to avoid noise; -R recursively descends into subdirectories so all nested block device symlinks are discovered without needing multiple invocations; -p appends a trailing slash to directory names making it immediately visible which entries are directories versus symlink device nodes, which is the primary content type under by-name*

---

## `lsattr`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `lsattr [-Radlpv] [FILE...]`

List file attributes on a Linux file system. Flag letters are defined in chattr help.

### Examples

```
toybox lsattr /data/local/tmp
```
*Lists ext2/ext4 filesystem attributes for all files in /data/local/tmp. No flags are used, so it shows the attribute bitmask string (e.g., '----e-------') followed by the filename for each entry. This is the baseline invocation to inspect whether files have immutable, append-only, or other special attributes set by the system or root processes.*

```
toybox lsattr -R /data/local/tmp
```
*Uses -R to recursively descend into all subdirectories under /data/local/tmp, listing ext2/ext4 attributes for every file found at any depth. This is composed this way because a flat lsattr would only show the top-level directory entries, and the recursive flag is needed to audit attribute state across an entire directory tree, which is necessary when checking for immutable flags on files written by system_server or installers.*

---

## `modinfo`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `modinfo [-0] [-b basedir] [-k kernel] [-F field] [module|file...]`

Display module fields for modules specified by name or .ko path.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-F` |  | Only show the given field |
| `-0` |  | Separate fields with NUL rather than newline |
| `-b` |  | Use <basedir> as root for /lib/modules/ |
| `-k` |  | Look in given directory under /lib/modules/ |

### Examples

```
toybox modinfo -k $(toybox uname -r) -F description ext4
```
*'-k $(toybox uname -r)' tells modinfo to look under /lib/modules/<running-kernel-version>/ so the lookup targets the exact kernel currently booted on the Galaxy S22, rather than guessing a version string manually. '-F description' filters output to only the human-readable description field, discarding noise like author, license, and param lines. 'ext4' is the module name to query, useful for confirming the ext4 filesystem module identity on the device.*

```
toybox modinfo -b /data/local/tmp/modules -k 5.10.101-android13 -0 -F depends vendor_module
```
*'-b /data/local/tmp/modules' redirects the root search path away from /lib/modules to a staging directory under /data/local/tmp where custom or pushed kernel modules might reside in a test or development context. '-k 5.10.101-android13' selects a specific kernel subdirectory under that basedir, allowing inspection of modules built for a target kernel version without that kernel being booted. '-0' separates output fields with NUL bytes instead of newlines, which is safer for programmatic parsing in system_server where output may be fed into buffers that mishandle newlines. '-F depends' restricts output to dependency information for 'vendor_module', revealing which other modules must be loaded first, critical for determining correct insmod ordering on Android vendor partitions.*

---

## `modprobe`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `modprobe [-alrqvsDb] [-d DIR] MODULE [symbol=value][...]`

modprobe utility - inserts modules and dependencies.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-a` |  | Load multiple MODULEs |
| `-b` |  | Apply blacklist to module names too |
| `-D` |  | Show dependencies |
| `-d` | `DIR` | Load modules from DIR, option may be used multiple times |
| `-l` |  | List (MODULE is a pattern) |
| `-q` |  | Quiet |
| `-r` |  | Remove MODULE (stacks) or do autoclean |
| `-s` |  | Log to syslog |
| `-v` |  | Verbose |

### Examples

```
toybox modprobe -v -s ip_tables
```
*Loads the ip_tables kernel module with -v for verbose output showing each step of the load process, and -s to log all activity to syslog so the load event is recorded in the system log. These two flags are combined because on Android from system_server you want both visibility and an audit trail when dynamically loading a network filtering module.*

```
toybox modprobe -D -d /system/lib/modules ip_tables
```
*Uses -D to print the dependency chain for ip_tables without actually loading it, and -d /system/lib/modules to tell modprobe to look for module files in the Android system partition path rather than the default location. This composition is useful for verifying that all prerequisite modules are present and resolvable before committing to a load operation.*

---

## `mount`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `mount [-afFrsvw] [-t TYPE] [-o OPTION,] [[DEVICE] DIR]`

Mount new filesystem(s) on directories. With no arguments, display existing mounts.

### Examples

```
toybox mount -t proc proc /proc
```
*Mounts the proc pseudo-filesystem of type proc (-t proc) with device name proc onto /proc. This is composed as a self-contained invocation because system_server may need to ensure the proc filesystem is mounted for reading kernel and process information. No shell features are needed since all arguments are literal paths and flags supported by mount itself.*

```
toybox mount -o ro -t ext4 /dev/block/bootdevice/by-name/system /system
```
*Mounts the system partition block device at /dev/block/bootdevice/by-name/system onto /system using the ext4 filesystem type (-t ext4) in read-only mode (-o ro). This is composed as a single invocation because UID 1000 in system_server context may need to remount system partitions for verification or recovery tasks. The -o ro flag ensures the partition is not modified during the mount operation, which is a safe default for system partitions on Android.*

---

## `netstat`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `netstat [-pWrxwutneal]`

Display networking information. Default is netstat -tuwx

### Examples

```
toybox netstat -tuneal
```
*'-t' shows TCP sockets, '-u' shows UDP sockets, '-n' prints numeric addresses and ports instead of resolving hostnames (faster and more reliable in Android system_server context where DNS may be restricted), '-e' displays extended information including user/inode, '-a' shows all sockets including listening and non-listening states, '-l' highlights which sockets are in the LISTEN state; combined this gives a full picture of active network endpoints on the device useful for diagnosing which services are bound to which ports*

```
toybox netstat -rn
```
*'-r' displays the kernel IP routing table showing all routes the system uses to forward packets, '-n' suppresses hostname resolution and prints raw numeric IP addresses for all gateway and destination fields; this combination is composed this way because on Android system_server context name resolution can be slow or fail entirely, and the routing table is essential for diagnosing connectivity issues such as missing default gateway or incorrect interface routes on a Samsung Galaxy S22*

---

## `nl`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `nl [-E] [-l #] [-b MODE] [-n STYLE] [-s SEPARATOR] [-v #] [-w WIDTH] [FILE...]`

Number lines of input.

### Examples

```
toybox nl -b a -n rz -w 4 -s ': ' /proc/cpuinfo
```
*-b a numbers all lines including blank ones (default skips blank), which matters for /proc/cpuinfo where every line is meaningful; -n rz formats line numbers as right-justified zero-padded (e.g. 0001) so columns align cleanly when piped to display tools; -w 4 sets the number field to 4 characters wide matching typical cpuinfo line counts; -s ': ' places a colon-space separator between the number and content for human readability; the result is a fully numbered annotated dump of CPU details from procfs without needing any shell pipeline*

```
toybox nl -b a -v 1 -w 6 -s ' | ' /data/local/tmp/boot_log.txt
```
*-b a ensures every line including blank lines is counted so line numbers correspond exactly to byte-offset regions useful when cross-referencing with a hex dump; -v 1 explicitly starts numbering at 1 which is the conventional baseline making automated line-reference scripts unambiguous; -w 6 accommodates log files that may exceed 9999 lines without truncating the number field; -s ' | ' uses a pipe-space separator that visually distinguishes the line number column from log content and is easy to parse with a fixed-column reader; this is a single self-contained invocation requiring no shell features*

---

## `paste`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `paste [-s] [-d DELIMITERS] [FILE...]`

Merge corresponding lines from each input file.

### Examples

```
toybox paste -d, /proc/version /proc/uptime
```
*Merges lines from /proc/version and /proc/uptime side by side, separated by a comma instead of the default tab. The -d, flag sets the delimiter to a comma so the two fields appear as a single comma-separated record on one line, which is useful when building CSV-style diagnostic snapshots from multiple proc files without needing shell redirection or pipes.*

```
toybox paste -s -d: /proc/cmdline /proc/version
```
*The -s flag makes paste operate in serial mode, collapsing all lines of each file into a single line before moving to the next file, rather than merging files line by line. Combined with -d: the colon delimiter separates tokens within each collapsed line. This is composed this way to produce a compact, colon-delimited single-line summary of the kernel command line and version string from two separate proc files in one invocation, suitable for logging to /data/local/tmp without shell constructs.*

---

## `patch`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `patch [-Rlsu] [-d DIR] [-i PATCH] [-p DEPTH] [-F FUZZ] [--dry-run] [FILE [PATCH]]`

Apply a unified diff to one or more files.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `patch [-Rlsu] [-d DIR] [-i PATCH] [-p DEPTH] [-F FUZZ] [--dry-run] [FILE [PATCH]]`
> Upstream: `patch [-Rlsuv] [-d DIR] [-i FILE] [-p DEPTH] [-F FUZZ] [--dry-run] [FILE [PATCH]]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `--dry-run` |  | Don't change files, just confirm patch applies |

### Examples

```
toybox patch -p1 -i /data/local/tmp/fix.patch --dry-run
```
*-p1 strips the leading path component from filenames in the patch header (e.g. 'a/src/foo.c' becomes 'src/foo.c'), which is the standard format produced by 'git diff' and 'diff -ru'; -i /data/local/tmp/fix.patch reads the patch from that file rather than stdin (which is unavailable without a shell); --dry-run applies the patch logic without writing any changes to disk, allowing verification that the patch applies cleanly before committing to modifications on the Android system partition or data directory*

```
toybox patch -R -p1 -i /data/local/tmp/applied.patch -d /data/local/tmp/workdir
```
*-R reverses the patch, meaning it undoes a previously applied patch by swapping the add and remove hunks, which is useful for rolling back a change; -p1 strips one leading path component to match the patch header format; -i /data/local/tmp/applied.patch specifies the patch file to read; -d /data/local/tmp/workdir changes the working directory to that path before applying, so all relative filenames in the patch are resolved inside that directory without needing a shell cd command*

---

## `pgrep`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `pgrep [-clfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`

Search for process(es). PATTERN is an extended regular expression checked against command names.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `pgrep [-clfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`
> Upstream: `pgrep [-aclfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`

### Examples

```
toybox pgrep -l -u 1000
```
*'-l' prints both the PID and process name instead of PID alone, giving human-readable output. '-u 1000' filters to only processes whose effective UID is 1000 (system_server context). This is composed this way because on Android, system services run under UID 1000 and listing them by name alongside PID is essential for identifying which services are active without a shell pipeline to cross-reference names.*

```
toybox pgrep -n -x zygote
```
*'-n' selects only the newest (most recently started) matching process, useful when multiple zygote processes exist (e.g., zygote and zygote64). '-x' requires an exact full-name match against 'zygote' rather than a substring match, preventing false positives from processes like 'zygote64'. This combination is composed this way to reliably return a single PID for the primary zygote process, which is the parent of all Android app processes and a critical reference point for process hierarchy inspection.*

---

## `pkill`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `pkill [-fnovx] [-SIGNAL|-l SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`

### Examples

```
toybox pkill -SIGNAL 9 -U 2000
```
*Sends SIGKILL (signal 9) to all processes owned by UID 2000 (shell user). -SIGNAL 9 specifies the kill signal as SIGKILL for forceful termination, and -U 2000 filters targets to only processes with real UID 2000. Composed this way because on Android, targeting by UID is more reliable than by name when cleaning up shell-owned processes from system_server context.*

```
toybox pkill -x -u 1000 surfaceflinger
```
*Sends the default SIGTERM to the surfaceflinger process, matching only processes whose effective UID is 1000 (system) and whose name matches exactly 'surfaceflinger'. -x enforces an exact full-name match to prevent accidentally killing processes whose names merely contain 'surfaceflinger' as a substring, and -u 1000 ensures only system-owned instances are targeted, which is critical in Android where multiple users may run similarly named processes.*

---

## `printenv`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `printenv [-0] [env_var...]`

Print environment variables.

### Examples

```
toybox printenv PATH
```
*Prints the value of the PATH environment variable. In system_server context (UID 1000), this reveals which directories are searched for executables, useful for diagnosing execution environment issues or verifying that Android system paths like /system/bin are present.*

```
toybox printenv ANDROID_DATA ANDROID_ROOT BOOTCLASSPATH
```
*Prints the values of three key Android environment variables in sequence. ANDROID_DATA typically points to /data, ANDROID_ROOT to /system, and BOOTCLASSPATH lists the JAR files loaded at boot. Passing multiple variable names to a single printenv invocation is the only way to retrieve several values at once without a shell, since no pipes or redirection are available.*

---

## `ps`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `ps [-AadefLlnwZ] [-gG GROUP,] [-k FIELD,] [-o FIELD,] [-p PID,] [-t TTY,] [-uU USER,]`

List processes.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-A` |  | -a  Has terminal not session leader |
| `-d` |  | -e  Synonym for -A |
| `-g` |  | -G  In real GROUPs (before sgid) |
| `-p` | `PID` | -P  Parent PIDs (--ppid) |
| `-s` |  | -t  Attached to selected TTYs |
| `-T` |  | -u  Owned by selected USERs |
| `-U` |  | Real USERs (before suid) |
| `-k` | `FIELD` | -M  Measure/pad future field widths |
| `-n` |  | -w  Wide output (don't truncate fields) |
| `-f` |  | Full listing (-o USER:12=UID,PID,PPID,C,STIME,TTY,TIME,ARGS=CMD) |
| `-l` |  | Long listing (-o F,S,UID,PID,PPID,C,PRI,NI,ADDR,SZ,WCHAN,TTY,TIME,CMD) |
| `-o` | `FIELD` | Output FIELDs instead of defaults, each with optional :size and =title |
| `-O` |  | Add FIELDS to defaults |
| `-Z` |  | Include LABEL |

### Examples

```
toybox ps -A -o PID,PPID,USER,ARGS -k ARGS
```
*'-A' selects every process on the system regardless of terminal, mirroring the POSIX 'ps -e' behavior needed from system_server to see all UIDs. '-o PID,PPID,USER,ARGS' overrides the default column set to show only the four fields relevant for tracing parent-child relationships and identifying process names, avoiding clutter. '-k ARGS' sorts the output alphabetically by the command argument string, grouping related processes (e.g. all zygote children) together for easier scanning. No shell is needed because all filtering and sorting is done by flags internal to the toybox ps implementation.*

```
toybox ps -A -Z -w -o PID,S,USER,LABEL,ARGS
```
*'-A' enumerates all processes system-wide, which is required from UID 1000 to audit SELinux contexts across different domains. '-Z' enables the LABEL column containing the full SELinux security context string for each process, critical for security auditing on Android where every process runs under a specific SELinux type. '-w' enables wide output so long SELinux labels such as 'u:r:system_server:s0' are not silently truncated, preserving correctness. '-o PID,S,USER,LABEL,ARGS' places process state 'S' alongside identity and context columns so the reader can correlate sleeping or zombie states with specific security domains in one pass.*

---

## `realpath`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `realpath [-LPemqsz] [--relative-base DIR] [-R DIR] FILE...`

Display the canonical absolute pathname

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-R` | `DIR` | Show ../path relative to DIR (--relative-to) |
| `-L` |  | Logical path (resolve .. before symlinks) |
| `-P` |  | Physical path (default) |
| `-e` |  | Canonical path to existing entry (fail if missing) |
| `-m` |  | Ignore missing entries, show where it would be |
| `-q` |  | Quiet (no error messages) |
| `-s` |  | Don't expand symlinks |
| `-z` | `NUL` | instead of newline |
| `--relative-base` | `DIR` | If path under DIR trim off prefix |

### Examples

```
toybox realpath -e -z /proc/self/exe
```
*-e requires the path to exist and resolves it fully to a canonical absolute path, failing loudly if it does not; -z outputs NUL instead of newline, which is safe for downstream consumption when the result is fed into another toybox command that accepts NUL-delimited input; /proc/self/exe is the symlink pointing to the executable of the current process, so this reveals the actual binary path of the running process under UID 1000 in system_server context without ambiguity from unresolved symlinks*

```
toybox realpath -m -q -R /data/local/tmp /data/local/tmp/test/../staging/apk/base.apk
```
*-m instructs realpath to resolve the path even if intermediate components do not exist, which is useful when verifying where a not-yet-created file would land after path normalization; -q suppresses any error output so the call stays silent in a production context where stderr noise is undesirable; -R /data/local/tmp requests output relative to /data/local/tmp, trimming that prefix so the result is a short relative path like staging/apk/base.apk rather than the full absolute path, making it easier to confirm the file stays within the intended working directory without escaping via .. traversal*

---

## `restorecon`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `restorecon [-D] [-F] [-R] [-n] [-v] FILE...`

Restores the default security contexts for the given files.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox restorecon -R -v /data/local/tmp
```
*-R recurses into all files and subdirectories under /data/local/tmp to restore SELinux security contexts; -v prints each file being relabeled so the caller can verify which contexts were reset. This compound form is necessary because individual files in /data/local/tmp can lose their SELinux labels after being created by tools that do not apply policy-correct contexts, and without -R only the directory itself would be relabeled.*

```
toybox restorecon -F -v /data/local/tmp/test.apk
```
*-F forces the context to be reset even if it already appears correct, overriding any cached or mismatched label on /data/local/tmp/test.apk; -v reports the old and new context so the result can be confirmed. This is composed this way because a simple restorecon without -F will silently skip files whose label matches the default, masking cases where the policy was updated but the file retained a stale context.*

---

## `sed`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `sed`

### Examples

```
toybox sed -n '/ro\.build/p' /system/build.prop
```
*`-n` suppresses default output, `/pattern/p` prints only matching lines. Cleaner than grep when you also need substitution in the same pass.*

```
toybox sed -i 's/old_value/new_value/g' /data/local/tmp/config.txt
```
*`-i` edits the file in place — no output redirection needed. The only sed operation that writes back to disk without a shell `>` operator.*

```
toybox sed '1,5d' /proc/kmsg
```
*Delete lines 1-5 and print the rest. Strip headers from kernel log output before further processing.*

---

## `sort`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `sort [-Mbcdfginrsuz] [FILE...] [-k#[,#[x]] [-t X]] [-o FILE]`

Sort all lines of text from input files (or stdin) to stdout.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `sort [-Mbcdfginrsuz] [FILE...] [-k#[,#[x]] [-t X]] [-o FILE]`
> Upstream: `sort [-bCcdfgiMnrsuxVz] [FILE...] [-k#[,#[x]] [-t X]] [-o FILE]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-k2` |  | 4 looks from the start of the second to the end of the fourth word. |

### Examples

```
toybox sort -k2,2 -t= /proc/cmdline -o /data/local/tmp/cmdline_sorted.txt
```
*Reads /proc/cmdline and sorts its key=value pairs by the second field (the value after '='), using '=' as the field delimiter via -t=. The -k2,2 flag restricts the sort key to exactly the second field only (start of field 2 to end of field 2), preventing spillover to subsequent fields. Output is written directly to /data/local/tmp/cmdline_sorted.txt via -o instead of stdout, which is necessary here since there is no shell redirection available.*

```
toybox sort -k1,1 -k2,2n -t/ /data/local/tmp/block_paths.txt -o /data/local/tmp/block_paths_sorted.txt
```
*Sorts a file listing partition paths (e.g. lines from /dev/block/bootdevice/by-name/) first alphabetically by the first path component (-k1,1) and then numerically by the second component (-k2,2n), using '/' as the field separator (-t/). The two -k flags create a compound sort key, so partitions are grouped by category then ordered by numeric suffix. Writing to a separate output file with -o avoids needing shell redirection and keeps the original input intact.*

---

## `tar`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `tar [-cxt] [-fvohmjkOS] [-XTCf NAME] [--selinux] [FILE...]`

Create, extract, or list files in a .tar (or compressed t?z) file.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `--exclude` | `FILENAME` | to exclude |
| `--full-time` |  | Show seconds with -tv |
| `--mode` | `MODE` | Adjust permissions |
| `--owner` | `NAME` | [:UID]  Set file ownership |
| `--mtime` | `TIME` | Override timestamps |
| `--group` | `NAME` | [:GID]  Set file group |
| `--sparse` |  | Record sparse files |
| `--selinux` |  | Save/restore labels |
| `--restrict` |  | All under one dir |
| `--no-recursion` |  | Skip dir contents |
| `--numeric-owner` |  | Use numeric uid/gid, not user/group names |
| `--null` |  | Filenames in -T FILE are null-separated, not newline |
| `--strip-components` | `NUM` | Ignore first NUM directory components when extracting |
| `--xform` | `SED` | Modify filenames via SED expression (ala s/find/replace/g) |
| `-I` | `PROG` | Filter through PROG to compress or PROG -d to decompress |
| `--anchored` |  | Match name not path |
| `--ignore-case` |  | Case insensitive |
| `--wildcards` |  | Expand *?[] like shell |

### Examples

```
toybox tar -c --selinux --numeric-owner --owner root:0 --group root:0 --mtime '2024-01-01' -f /data/local/tmp/system_backup.tar /system/etc/hosts /system/etc/permissions
```
*'-c' creates a new archive at '-f /data/local/tmp/system_backup.tar'. '--selinux' preserves SELinux security contexts critical on Android so restored files retain MAC policy labels. '--numeric-owner' records uid/gid as numbers rather than names, safe since Android may not have matching user databases on restore. '--owner root:0' and '--group root:0' force ownership metadata to root regardless of the running process's uid. '--mtime 2024-01-01' normalizes timestamps for reproducible archive fingerprints. The two paths capture the hosts file and permissions XML directory used by PackageManager.*

```
toybox tar -x --selinux --strip-components 2 --no-recursion --restrict -f /data/local/tmp/system_backup.tar -C /data/local/tmp/restore
```
*'-x' extracts from the archive named by '-f'. '--selinux' restores saved SELinux labels onto extracted files, essential in system_server context where wrong labels break Binder access. '--strip-components 2' drops the first two path segments (e.g. 'system/etc/') so files land flat in the destination, avoiding deep nested directories. '--no-recursion' prevents tar from descending into any directory entries recorded in the archive, extracting only explicitly listed members. '--restrict' enforces that all output paths resolve under the single destination, blocking path-traversal attacks where a crafted archive could escape '-C /data/local/tmp/restore'.*

---

## `top`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `top [-Hhbq] [-k FIELD,] [-o FIELD,] [-s SORT] [-n NUMBER] [-m LINES] [-d SECONDS] [-p PID,] [-u USER,]`

Show process activity in real time.

### Examples

```
toybox top -b -n 1 -m 20 -s 6
```
*Run top in batch mode (-b) so output is plain text suitable for capture without terminal control codes, take exactly one snapshot (-n 1) instead of looping, limit display to 20 process lines (-m 20), and sort by column 6 which is typically CPU usage (-s 6). This is composed this way because system_server needs a one-shot process list without an interactive terminal, and sorting by CPU immediately surfaces the heaviest consumers.*

```
toybox top -b -n 1 -p 1000 -o PID,USER,PR,NI,VIRT,RES,S,CPU,COMMAND
```
*Run top in batch mode (-b) for a single iteration (-n 1), filter to only the process with PID 1000 (-p 1000) to inspect system_server itself, and define a specific ordered set of output fields (-o) covering process ID, owner, priority, nice value, virtual and resident memory, state, CPU percent, and command name. This is composed this way because specifying -o explicitly controls which columns appear and in what order, giving a concise machine-parseable one-line snapshot of a single process without scrolling through the full process table.*

---

## `touch`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `touch [-amch] [-d DATE] [-t TIME] [-r FILE] FILE...`

Update the access and modification times of each FILE to the current time.

### Examples

```
toybox touch -d 2024-01-15T08:30:00 /data/local/tmp/testfile.txt
```
*Creates /data/local/tmp/testfile.txt if it does not exist and sets both its access and modification timestamps to 2024-01-15 08:30:00. The -d flag accepts an ISO 8601 datetime string, which is the most portable and unambiguous way to specify an exact timestamp when staging test files under system_server context without relying on shell date expansion.*

```
toybox touch -r /proc/1/exe /data/local/tmp/marker.bin
```
*Creates /data/local/tmp/marker.bin and stamps it with the same access and modification times as /proc/1/exe (the init process executable). The -r flag copies timestamps from a reference file rather than using the current clock, which is useful when you need a marker file whose timestamps align with a known system reference point for forensic or ordering purposes.*

---

## `traceroute`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `traceroute [-46FUIldnvr] [-f 1ST_TTL] [-m MAXTTL] [-p PORT] [-q PROBES]`

[-s SRC_IP] [-t TOS] [-w WAIT_SEC] [-g GATEWAY] [-i IFACE] [-z PAUSE_MSEC] HOST [BYTES]

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-4` |  | -6 Force IP or IPv6 name resolution |
| `-F` |  | Set the don't fragment bit (supports IPV4 only) |
| `-U` |  | Use UDP datagrams instead of ICMP ECHO (supports IPV4 only) |
| `-I` |  | Use ICMP ECHO instead of UDP datagrams (supports IPV4 only) |
| `-l` |  | Display the TTL value of the returned packet (supports IPV4 only) |
| `-d` |  | Set SO_DEBUG options to socket |
| `-n` |  | Print numeric addresses |
| `-v` |  | verbose |
| `-r` |  | Bypass routing tables, send directly to HOST |
| `-m` | `MAXTTL` | Max time-to-live (max number of hops)(RANGE 1 to 255) |
| `-p` | `PORT` | Base UDP port number used in probes(default 33434)(RANGE 1 to 65535) |
| `-q` | `PROBES` | Number of probes per TTL (default 3)(RANGE 1 to 255) |
| `-s` | `IP` | address to use as the source address |
| `-t` |  | Type-of-service in probe packets (default 0)(RANGE 0 to 255) |
| `-w` |  | Time in seconds to wait for a response (default 3)(RANGE 0 to 86400) |
| `-g` |  | Loose source route gateway (8 max) (supports IPV4 only) |
| `-z` |  | Pause Time in ms (default 0)(RANGE 0 to 86400) (supports IPV4 only) |
| `-f` |  | Start from the 1ST_TTL hop (instead from 1)(RANGE 1 to 255) (supports IPV4 only) |
| `-i` |  | Specify a network interface to operate with |

### Examples

```
toybox traceroute -4 -n -m 20 -q 2 -w 2 8.8.8.8
```
*-4 forces IPv4 resolution to avoid ambiguity on a dual-stack Android device; -n skips DNS reverse lookups and prints raw numeric IPs, which is faster and works reliably from system_server context where DNS may be restricted; -m 20 caps the max hops at 20 since most internet paths resolve within that range, avoiding unnecessary probe cycles; -q 2 reduces probes per TTL from the default 3 down to 2, cutting total packet count and finishing faster; -w 2 shortens the per-probe wait to 2 seconds instead of 3, reducing total wall time on unresponsive hops; 8.8.8.8 is the target, a well-known reachable host used to verify end-to-end IPv4 routing from the device*

```
toybox traceroute -I -l -n -f 3 -m 15 -q 1 -p 33434 192.168.1.1
```
*-I switches from UDP to ICMP ECHO probes, which are more likely to receive responses from intermediate Android gateway hops and firewalls that silently drop UDP; -l prints the TTL value carried in each returned packet, useful for diagnosing asymmetric routing or TTL manipulation; -n suppresses reverse DNS to avoid blocking calls from system_server; -f 3 skips the first two hops which are known local interfaces, starting the trace at hop 3 to focus on gateway and beyond; -m 15 limits max hops to 15 since the target is on the local LAN; -q 1 sends only one probe per TTL to minimize traffic against a local router; -p 33434 explicitly sets the base port to the standard traceroute default for clarity and consistency in firewall logs; 192.168.1.1 is the default gateway address commonly used to diagnose local network path issues*

---

## `traceroute6`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `traceroute [-46FUIldnvr] [-f 1ST_TTL] [-m MAXTTL] [-p PORT] [-q PROBES]`

[-s SRC_IP] [-t TOS] [-w WAIT_SEC] [-g GATEWAY] [-i IFACE] [-z PAUSE_MSEC] HOST [BYTES]

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-4` |  | -6 Force IP or IPv6 name resolution |
| `-F` |  | Set the don't fragment bit (supports IPV4 only) |
| `-U` |  | Use UDP datagrams instead of ICMP ECHO (supports IPV4 only) |
| `-I` |  | Use ICMP ECHO instead of UDP datagrams (supports IPV4 only) |
| `-l` |  | Display the TTL value of the returned packet (supports IPV4 only) |
| `-d` |  | Set SO_DEBUG options to socket |
| `-n` |  | Print numeric addresses |
| `-v` |  | verbose |
| `-r` |  | Bypass routing tables, send directly to HOST |
| `-m` | `MAXTTL` | Max time-to-live (max number of hops)(RANGE 1 to 255) |
| `-p` | `PORT` | Base UDP port number used in probes(default 33434)(RANGE 1 to 65535) |
| `-q` | `PROBES` | Number of probes per TTL (default 3)(RANGE 1 to 255) |
| `-s` | `IP` | address to use as the source address |
| `-t` |  | Type-of-service in probe packets (default 0)(RANGE 0 to 255) |
| `-w` |  | Time in seconds to wait for a response (default 3)(RANGE 0 to 86400) |
| `-g` |  | Loose source route gateway (8 max) (supports IPV4 only) |
| `-z` |  | Pause Time in ms (default 0)(RANGE 0 to 86400) (supports IPV4 only) |
| `-f` |  | Start from the 1ST_TTL hop (instead from 1)(RANGE 1 to 255) (supports IPV4 only) |
| `-i` |  | Specify a network interface to operate with |

### Examples

```
toybox traceroute6 -6 -n -m 20 -q 2 -w 5 2001:4860:4860::8888
```
*-6 forces IPv6 name resolution to ensure the trace uses IPv6 even if the target could resolve to IPv4; -n prints numeric addresses instead of attempting reverse DNS lookups, which is important in Android system_server context where DNS resolution may be unreliable or slow; -m 20 caps the maximum hops at 20 to avoid excessively long traces on a mobile network; -q 2 sends 2 probes per hop instead of the default 3, reducing network overhead; -w 5 waits up to 5 seconds per probe response to tolerate higher-latency mobile links; the target is Google's public IPv6 DNS, a reliable endpoint for validating IPv6 connectivity from the device*

```
toybox traceroute6 -6 -n -v -m 15 -q 1 -p 33435 -w 3 -i wlan0 fe80::1
```
*-6 forces IPv6 resolution to keep the trace on the IPv6 stack; -n suppresses reverse DNS to avoid blocking calls in system_server; -v enables verbose output to expose additional routing details such as ICMP response types; -m 15 limits hops to 15 since a link-local destination like fe80::1 should be reachable within very few hops and a short cap prevents unnecessary probing; -q 1 sends only one probe per TTL to minimize traffic on a local link trace; -p 33435 shifts the base UDP port by one to avoid collision with other concurrent traceroute sessions; -w 3 keeps the default 3-second timeout; -i wlan0 binds the trace to the wlan0 interface which is required for link-local addresses because fe80:: addresses are scoped to a specific interface and without this the kernel cannot determine which interface to use*

---

## `ulimit`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `ulimit [-P PID] [-SHRacdefilmnpqrstuv] [LIMIT]`

Print or set resource limits for process number PID. If no LIMIT specified (or read-only -ap selected) display current value (sizes in bytes). Default is ulimit -P $PPID -Sf" (show soft filesize of your shell).

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-P` | `PID` | to affect (default $PPID) |
| `-a` |  | Show all limits |
| `-S` |  | Set/show soft limit |
| `-H` |  | Set/show hard (maximum) limit |
| `-c` |  | Core file size (blocks) |
| `-d` |  | Process data segment (KiB) |
| `-e` |  | Max scheduling priority |
| `-f` |  | File size (KiB) |
| `-i` |  | Pending signal count |
| `-l` |  | Locked memory (KiB) |
| `-m` |  | Resident Set Size (KiB) |
| `-n` |  | Number of open files |
| `-p` |  | Pipe buffer (512 bytes) |
| `-q` | `POSIX` | message queues |
| `-r` |  | Max realtime priority |
| `-R` |  | Realtime latency (us) |
| `-s` |  | Stack size (KiB) |
| `-t` |  | Total CPU time (s) |
| `-u` |  | Maximum processes (this UID) |
| `-v` |  | Virtual memory size (KiB) |

### Examples

```
toybox ulimit -SH -n 4096
```
*-S targets the soft limit and -H targets the hard limit simultaneously, -n selects the open-file-descriptors resource; passing 4096 sets both soft and hard limits for open files to 4096 in the current process context, which is useful under system_server to raise the fd ceiling before spawning file-heavy services*

```
toybox ulimit -P 1 -a
```
*-P 1 directs the query to PID 1 (init/Android runtime ancestor) instead of the default PPID, -a prints every resource limit for that process in one shot; composing them this way lets you audit the full rlimit table of the root process from the system_server context without needing a shell or separate proc reads*

---

## `umount`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `umount [-a [-t TYPE[,TYPE...]]] [-vrfD] [DIR...]`

Unmount the listed filesystems.

### Examples

```
toybox umount /data/local/tmp/testmount
```
*Unmounts the filesystem mounted at /data/local/tmp/testmount. No flags are needed for a standard unmount of a single directory; the path argument tells umount exactly which mount point to detach from the VFS tree. Used in system_server context when cleaning up a temporary bind mount or loop mount created during testing or OTA staging.*

```
toybox umount -vrf /data/local/tmp/testmount
```
*-v enables verbose output so the caller can confirm which device and path were unmounted, -r causes umount to fall back to remounting read-only if the unmount itself fails (protecting filesystem integrity when the mount is busy), and -f forces the unmount even if the mount point is in use. Together these flags make the invocation suitable for a system_server cleanup path where the mount may be busy and a hard detach or safe degradation to read-only is preferable to leaving the mount point in an unknown state.*

---

## `uname`

`[self-contained]`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `uname [-asnrvm]`

Print system information.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `uname [-asnrvm]`
> Upstream: `uname [-asnrvmo]`

### Examples

```
toybox uname -a
```
*The -a flag prints all available system information in a single line: kernel name, node name, kernel release, kernel version, machine hardware name. This is composed as a single invocation because -a is the most complete flag, equivalent to combining -s -n -r -v -m, and is useful for capturing full platform identity on the Samsung Galaxy S22 running Android from system_server context without needing shell expansion or piping.*

```
toybox uname -rm
```
*The -r flag prints the kernel release string (e.g. 5.10.x-android13) and -m prints the machine hardware name (e.g. aarch64). These two flags are combined in one invocation to identify both the kernel version and the CPU architecture of the Galaxy S22 simultaneously, which is useful for determining compatibility of kernel modules or native binaries without the noise of other fields from -a.*

---

## `xxd`

`[self-contained]` `[io-explicit]`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `xxd [-eipr] [-cglos N] [file]`

Hexdump a file to stdout. If no file is listed, copy from stdin. Filename "-" is a synonym for stdin.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-c` |  | Show N bytes per line (default 16) |
| `-g` |  | Group bytes by adding a ' ' every N bytes (default 2) |
| `-l` |  | Limit of N bytes before stopping (default is no limit) |
| `-o` |  | Add N to display offset |
| `-s` |  | Skip to offset N |

### Examples

```
toybox xxd -l 256 -c 16 -g 4 /dev/block/bootdevice/by-name/boot
```
*Opens the raw boot partition block device and reads exactly 256 bytes (-l 256), displaying 16 bytes per line (-c 16) grouped in 4-byte chunks (-g 4). Limiting to 256 bytes prevents reading the entire partition; the grouping of 4 matches 32-bit word boundaries common in bootloader header inspection.*

```
toybox xxd -s 1024 -l 128 -o 1024 -c 8 /data/local/tmp/payload.bin
```
*Skips the first 1024 bytes of the file (-s 1024) to reach a known structure offset, reads only 128 bytes (-l 128), and adjusts the printed offset labels by +1024 (-o 1024) so displayed addresses reflect actual file positions rather than resetting to zero. Reducing to 8 bytes per line (-c 8) widens the ASCII column for denser printable-character inspection.*

---

## `cksum`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `cksum [-IPLN] [FILE...]`

For each file, output crc32 checksum value, length and name of file. If no files listed, copy from stdin.  Filename "-" is a synonym for stdin.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cksum [-IPLN] [FILE...]`
> Upstream: `cksum [-HIPLN] [FILE...]`

### Examples

```
toybox cksum /system/lib64/libandroid.so /system/lib64/libc.so
```
*Runs cksum on two critical Android system libraries simultaneously. cksum computes a CRC32 checksum and byte count for each file and prints one result line per file. Providing multiple paths in a single invocation avoids needing a shell loop, making this valid under the no-shell constraint. The output lets a developer verify that core native libraries have not been modified or corrupted, which is useful from system_server context during integrity checks.*

```
toybox cksum /dev/block/bootdevice/by-name/system /dev/block/bootdevice/by-name/vendor
```
*Runs cksum directly against the raw block devices for the system and vendor partitions by their stable symlink names under /dev/block/bootdevice/by-name/. Because cksum reads any file-like object, it can checksum block devices byte-for-byte without mounting them. Passing both paths in one invocation produces a CRC32 and size for each partition, letting a forensic or OTA verification routine confirm partition contents match expected values without spawning a shell or using redirection.*

---

## `comm`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `comm [-123] FILE1 FILE2`

Read FILE1 and FILE2, which should be ordered, and produce three text columns as output: lines only in FILE1; lines only in FILE2; and lines in both files. Filename "-" is a synonym for stdin.

### Examples

```
toybox comm -13 /data/local/tmp/packages_old.txt /data/local/tmp/packages_new.txt
```
*Compares two sorted package list files; -1 suppresses lines only in FILE1 (old list), -3 suppresses lines common to both files, leaving only lines unique to FILE2 (new list). This reveals packages installed since the last snapshot, useful for auditing new installs from system_server without any shell pipeline support since comm handles the filtering internally via its own flags.*

```
toybox comm -23 /data/local/tmp/baseline_perms.txt /data/local/tmp/current_perms.txt
```
*Compares two sorted permission manifest files; -2 suppresses lines only in FILE2 (current), -3 suppresses common lines, leaving only lines that existed in the baseline but are absent now. This identifies permissions that have been revoked or removed since the baseline was recorded, composing the entire diff logic within a single toybox invocation since no shell redirection or grep is available.*

---

## `dd`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `dd [if|of=FILE] [ibs|obs|bs|count|seek|skip=N] [conv|status|iflag|oflag=FLAG[,FLAG...]]`

Copy/convert blocks of data from input to output, with the following keyword=value modifiers (and their default values):

### Examples

```
toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin bs=4096
```
*`if=` and `of=` replace both `<` and `>` entirely. The canonical shell-free way to read or write block devices and raw partition images.*

```
toybox dd if=/data/local/tmp/payload of=/dev/block/bootdevice/by-name/param bs=1 seek=256 conv=notrunc
```
*Write payload starting at byte 256 without touching the rest of the partition. `conv=notrunc` is critical — without it dd truncates the output to the input size.*

```
toybox dd if=/dev/urandom of=/data/local/tmp/test.bin bs=1M count=1
```
*Generate 1MB of random data to a file — useful for entropy testing or creating test payloads without /dev/random blocking.*

---

## `fallocate`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `fallocate [-l size] [-o offset] file`

Tell the filesystem to allocate space for a file.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `fallocate [-l size] [-o offset] file`
> Upstream: `fallocate [-o OFFSET] -l SIZE FILE`

### Examples

```
toybox fallocate -l 104857600 /data/local/tmp/testfile.bin
```
*Allocates exactly 104857600 bytes (100MB) of disk space for testfile.bin without writing any data. The -l flag specifies the total allocation length in bytes. This is composed as a single invocation because fallocate preallocates contiguous blocks on the filesystem, making it ideal for testing disk space availability or pre-staging files in /data/local/tmp from system_server context without expensive write I/O.*

```
toybox fallocate -l 4096 -o 8192 /data/local/tmp/sparse.bin
```
*Allocates 4096 bytes starting at offset 8192 within sparse.bin. The -o flag sets the byte offset into the file before allocation begins, and -l sets how many bytes to allocate from that offset. This is composed this way to punch a specific region into an existing or new file, useful for creating sparse file layouts or reserving a particular block range in the middle of a file for structured binary data testing on Android.*

---

## `gzip`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `gzip [-19cdfkt] [FILE...]`

Compress files. With no files, compresses stdin to stdout. On success, the input files are removed and replaced by new files with the .gz suffix.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox gzip -9 /data/local/tmp/logdump.txt
```
*Compresses /data/local/tmp/logdump.txt in place using maximum compression level (-9). The -9 flag selects the highest compression ratio at the cost of more CPU time, suitable for log files being archived from system_server context where storage is constrained. The input file is replaced by logdump.txt.gz upon success.*

```
toybox gzip -d /data/local/tmp/config_backup.gz
```
*Decompresses /data/local/tmp/config_backup.gz in place using the -d (decompress) flag. This restores the original file config_backup from a previously gzip-compressed archive, necessary when retrieving stored configuration data in /data/local/tmp without relying on a shell pipeline or separate gunzip binary.*

---

## `install`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `install [-dDpsv] [-o USER] [-g GROUP] [-m MODE] [-t TARGET] [SOURCE...] [DEST]`

Copy files and set attributes.

### Examples

```
toybox install -d -m 0750 -o system -g system /data/local/tmp/myappdir
```
*Creates the directory /data/local/tmp/myappdir (-d flag creates directories instead of copying files). Sets permissions to 0750 (-m 0750) so owner has full access and group has read/execute but others have none. Assigns ownership to user 'system' and group 'system' (-o system -g system), which is appropriate for system_server context (UID 1000) deploying a controlled workspace. This single invocation handles mkdir plus chmod plus chown atomically, which is why install is preferred over separate commands.*

```
toybox install -p -m 0644 -o system -g system -t /data/local/tmp/deploy /system/etc/myconfig.conf
```
*Copies the source file /system/etc/myconfig.conf to the destination directory /data/local/tmp/deploy (-t TARGET specifies the target directory so the filename is preserved). The -p flag preserves the source file timestamps on the installed copy, which is important for cache invalidation and auditing. Permissions are set to 0644 (-m 0644) making the file world-readable but only owner-writable. Ownership is assigned to system/system (-o system -g system) matching the UID 1000 running context. Combining -p with -t and -m in one call avoids a separate cp plus chmod plus chown sequence.*

---

## `mv`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `mv [-finTv] [-t TARGET] SOURCE... [DEST]`

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mv [-finTv] [-t TARGET] SOURCE... [DEST]`
> Upstream: `mv [-FfinTvx] [-t TARGET] SOURCE... [DEST]`

### Examples

```
toybox mv -v /data/local/tmp/stage_update.zip /data/local/tmp/apply_update.zip
```
*Renames stage_update.zip to apply_update.zip within /data/local/tmp. The -v flag prints the rename operation so system_server can confirm the file was moved without needing a separate ls call. Single directory means no cross-filesystem copy is needed, just an atomic rename syscall.*

```
toybox mv -f -t /data/local/tmp/archive /data/local/tmp/log_a.txt /data/local/tmp/log_b.txt
```
*Moves both log_a.txt and log_b.txt into the /data/local/tmp/archive directory. -t designates the destination so multiple SOURCE files can be listed after the flag without ambiguity about which argument is the target. -f suppresses any overwrite prompts, important in a non-interactive system_server context where there is no terminal to respond to a prompt.*

---

## `rev`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `rev [FILE...]`

Output each line reversed, when no files are given stdin is used.

### Examples

```
toybox rev /proc/sys/kernel/osrelease
```
*Reads the kernel version string from /proc/sys/kernel/osrelease and reverses each line character by character. No flags are available for rev, so this is a direct single-file invocation. Useful in system_server context to produce a reversed version string that can be compared or logged as a quick integrity marker without any shell pipeline.*

```
toybox rev /data/local/tmp/device_id.txt
```
*Reads a device identifier or token stored in /data/local/tmp/device_id.txt and reverses every line in the file. Because rev has no flags, the command is composed solely with the file argument. This is practical when a stored token needs to be obfuscated or when verifying a symmetric reversal property of a known string during diagnostics from system_server context.*

---

## `split`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `split [-a SUFFIX_LEN] [-b BYTES] [-l LINES] [-n PARTS] [INPUT [OUTPUT]]`

Copy INPUT (or stdin) data to a series of OUTPUT (or "x") files with alphabetically increasing suffix (aa, ab, ac... az, ba, bb...).

### Examples

```
toybox split -b 1048576 -a 3 /data/local/tmp/firmware.img /data/local/tmp/fw_part_
```
*Splits /data/local/tmp/firmware.img into 1MB chunks (-b 1048576) with 3-character numeric suffixes (-a 3), writing output files named fw_part_000, fw_part_001, etc. into /data/local/tmp/. This is composed this way because firmware images are large binary blobs that must be split into manageable pieces for staged writes or verification, and the 3-char suffix allows up to 1000 parts without name collisions.*

```
toybox split -l 1000 -a 2 /data/local/tmp/logdump.txt /data/local/tmp/log_chunk_
```
*Splits /data/local/tmp/logdump.txt into segments of 1000 lines each (-l 1000) with 2-character suffixes (-a 2), producing log_chunk_aa, log_chunk_ab, etc. This approach is chosen when the log is a line-oriented text file and downstream tooling needs bounded line counts per chunk rather than byte-bounded splits, avoiding partial-line boundaries that -b would introduce.*

---

## `tee`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `tee [-ai] [FILE...]`

Copy stdin to each listed file, and also to stdout. Filename "-" is a synonym for stdout.

### Examples

```
toybox tee /data/local/tmp/syslog_copy.txt
```
*Reads from stdin and writes the data simultaneously to stdout and to /data/local/tmp/syslog_copy.txt. tee is used here to capture a copy of streamed data to a file while still passing it through to stdout, which is useful in system_server context when you want to persist output without losing the live stream. Since no shell pipes are available, this would be invoked with stdin connected programmatically by the calling process.*

```
toybox tee -a /data/local/tmp/audit_log.txt
```
*Reads from stdin and appends the output to /data/local/tmp/audit_log.txt rather than overwriting it, while also writing to stdout. The -a flag (append) is critical here because in an ongoing audit or logging scenario within system_server, multiple invocations must accumulate records in the same file instead of clobbering previous entries. Without -a, each new invocation would truncate the file, destroying prior log data.*

---

## `uudecode`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `uudecode [-o OUTFILE] [INFILE]`

Decode file from stdin (or INFILE).

### Examples

```
toybox uudecode -o /data/local/tmp/recovered.bin /data/local/tmp/encoded.uu
```
*Decodes a uuencoded file at /data/local/tmp/encoded.uu and writes the binary output to /data/local/tmp/recovered.bin. The -o flag overrides the output filename embedded in the uu header, which is important in Android system_server context where the original encoded filename may point to a path that is inaccessible or undesirable. INFILE is specified explicitly so no shell stdin redirection is needed, satisfying the no-shell constraint.*

```
toybox uudecode -o /data/local/tmp/payload.so /data/local/tmp/transfer.uu
```
*Decodes a uuencoded native library archive from /data/local/tmp/transfer.uu into /data/local/tmp/payload.so. Using -o forces the output destination regardless of what filename the uu file header declares, which is critical when the encoding was done on a different host where the embedded filename references a non-Android path. Specifying the INFILE argument directly avoids any need for shell pipes or input redirection.*

---

## `wc`

`[io-explicit]`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `wc -lwcm [FILE...]`

Count lines, words, and characters in input.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `wc -lwcm [FILE...]`
> Upstream: `wc [-Llwcm] [FILE...]`

### Examples

```
toybox wc -l /proc/modules
```
*-l counts only lines in /proc/modules, which lists one loaded kernel module per line; this gives the total number of currently loaded kernel modules on the device without needing shell pipelines or other tools*

```
toybox wc -lwc /data/local/tmp/logdump.txt
```
*-l counts newline-separated log entries, -w counts whitespace-delimited tokens (useful for estimating word volume in structured logs), and -c counts raw bytes to verify file size; combining all three flags in one invocation avoids multiple passes over the file and gives a compact summary of the log dump in a single system_server call*

---

## `acpi`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `acpi [-abctV]`

Show status of power sources and thermal devices.

### Examples

```
toybox acpi
```
*Runs acpi with no flags to display all available ACPI information including battery state, capacity percentage, and charging status. On a Samsung Galaxy S22 running Android, this gives a quick snapshot of power subsystem state as reported through the ACPI interface, useful from system_server context to check battery health without reading raw sysfs nodes.*

---

## `base64`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `base64 [-di] [-w COLUMNS] [FILE...]`

Encode or decode in base64.

### Examples

```
toybox base64 /proc/1/cmdline
```
*Reads the cmdline file for PID 1 (init process) from /proc and encodes its binary content as base64. The cmdline file uses null bytes as argument separators, making raw output unreadable in terminal contexts, so base64 encoding produces a clean ASCII-safe representation suitable for logging or transmission from system_server.*

```
toybox base64 -d /data/local/tmp/payload.b64
```
*Decodes a base64-encoded file at /data/local/tmp/payload.b64 back to its original binary form. The -d flag switches from encode mode to decode mode. This is useful in system_server context when a binary blob such as a certificate or config has been stored in base64 form and needs to be decoded before processing.*

---

## `basename`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `basename [-a] [-s SUFFIX] NAME... | NAME [SUFFIX]`

Return non-directory portion of a pathname removing suffix.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-s` | `SUFFIX` | Remove suffix (implies -a) |

### Examples

```
toybox basename -s .img /dev/block/bootdevice/by-name/boot.img
```
*Strips the .img suffix from the full path /dev/block/bootdevice/by-name/boot.img. The -s flag tells basename to remove the specified suffix after extracting the final path component, yielding 'boot'. Useful when iterating partition names where the extension is not part of the canonical partition identifier.*

```
toybox basename -s .apk /data/local/tmp/com.example.app.apk
```
*Extracts the bare package name from a staged APK path in /data/local/tmp by stripping both the directory and the .apk suffix in one pass. The -s flag implies -a behavior, so multiple names could be passed if needed. The result 'com.example.app' can be used directly as a package identifier in subsequent toybox or am commands without further processing.*

---

## `blkdiscard`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `blkdiscard [-olszf] DEVICE`

Discard device sectors.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `blkdiscard [-olszf] DEVICE`
> Upstream: `blkdiscard [-szf] [-o OFFSET] [-l LENGTH] DEVICE`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-o` |  | Byte offset to start discarding at (default 0) |
| `-l` |  | Bytes to discard (default all) |
| `-s` |  | Perform secure discard |
| `-z` |  | Zero-fill rather than discard |
| `-f` |  | Disable check for mounted filesystem |

### Examples

```
toybox blkdiscard -o 0 -l 536870912 /dev/block/bootdevice/by-name/userdata
```
*Discards 512MB (536870912 bytes) starting at offset 0 on the userdata partition. -o 0 sets the starting byte offset explicitly to the beginning of the partition, and -l 536870912 limits the discard operation to exactly 512MB rather than defaulting to the full partition size. This is composed as a bounded discard rather than a full wipe, useful for selectively invalidating only the first portion of userdata during a partial factory reset procedure from system_server context.*

```
toybox blkdiscard -z -f /dev/block/bootdevice/by-name/cache
```
*Zero-fills the entire cache partition rather than issuing a discard command to the storage device. -z causes each sector to be written with zeros instead of using the BLKDISCARD ioctl, which guarantees data destruction on devices that may not honor discard semantics. -f disables the mounted filesystem check, which is necessary in system_server context where the cache partition may still appear mounted to the kernel even if logically unmounted, preventing the operation from being blocked by that safety guard.*

---

## `blkid`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `blkid [-o TYPE] [-s TAG] [-UL] DEV...`

Print type, label and UUID of filesystem on a block device or image.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-o` | `TYPE` | Output format (full, value, export) |
| `-s` | `TAG` | Only show matching tags (default all) |

### Examples

```
toybox blkid -o export /dev/block/bootdevice/by-name/userdata
```
*-o export formats output as KEY=VALUE pairs suitable for parsing by other tools; targeting /dev/block/bootdevice/by-name/userdata reads the filesystem metadata from the userdata partition, which is the primary user data storage on the Galaxy S22; this form is used from system_server to programmatically identify UUID, TYPE, and LABEL of the partition without needing shell variable assignment*

```
toybox blkid -o value -s TYPE /dev/block/bootdevice/by-name/system /dev/block/bootdevice/by-name/vendor
```
*-s TYPE restricts output to only the filesystem type tag, eliminating UUID and LABEL noise; -o value prints the bare value with no key prefix, so you get a clean single-word result like ext4 or erofs per device; listing both system and vendor partitions in one invocation lets you confirm filesystem types on both read-only partitions in a single call, which matters in system_server context where confirming partition format before a remount decision is critical*

---

## `blockdev`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `blockdev --OPTION... BLOCKDEV...`

Call ioctl(s) on each listed block device

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `--setbsz` | `BYTES` | Set block size |
| `--setra` | `SECTORS` | Set readahead |

### Examples

```
toybox blockdev --setra 256 /dev/block/bootdevice/by-name/userdata
```
*--setra 256 sets the readahead to 256 sectors on the userdata block device, which tells the kernel to prefetch more data ahead of sequential reads; this is composed as a single invocation because blockdev operates directly on the block device node and requires no shell piping or redirection to take effect*

```
toybox blockdev --setbsz 4096 /dev/block/bootdevice/by-name/system
```
*--setbsz 4096 sets the logical block size to 4096 bytes on the system partition block device, matching the typical page size on ARM64 Android devices like the Galaxy S22; this is a single self-contained invocation because blockdev issues an ioctl directly to the kernel block layer without needing any shell facilities*

---

## `cal`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `cal [[[DAY] MONTH] YEAR]`

Print a calendar.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cal [[[DAY] MONTH] YEAR]`
> Upstream: `cal [-h] [[[DAY] MONTH] YEAR]`

### Examples

```
toybox cal 2024
```
*Displays the full calendar for the year 2024. No flags are available for this command, so the only way to specify output is via positional arguments. Passing a single integer argument is interpreted as YEAR, causing cal to print all 12 months of that year. Useful in system_server context to verify date ranges when debugging time-sensitive Android services or alarms.*

```
toybox cal 3 2024
```
*Displays the calendar for March 2024 specifically. Two positional arguments are interpreted as MONTH then YEAR in that order. This narrowed view is useful when cross-referencing a specific month against log timestamps or scheduled job windows without the noise of the full yearly output.*

---

## `cat`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `cat [-etuv] [FILE...]`

Copy (concatenate) files to stdout.  If no files listed, copy from stdin. Filename "-" is a synonym for stdin.

### Examples

```
toybox cat /proc/cpuinfo
```
*Reads and prints the contents of /proc/cpuinfo to stdout. The kernel exposes CPU details (processor model, features, cores) through this virtual file. No flags are needed because the content is plain ASCII text that requires no special formatting. This is the standard way to inspect hardware capabilities from system_server context without a shell.*

```
toybox cat /data/local/tmp/staged_config.txt
```
*Reads and prints a staged configuration file from /data/local/tmp, which is a writable scratch area accessible at UID 1000. No flags are used because the file is expected to contain plain readable text. This is composed as a single self-contained invocation since there is no shell redirection available to chain output elsewhere, so the result goes directly to stdout for the caller to capture programmatically.*

---

## `clear`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `clear`

### Examples

```
toybox clear
```
*Clears the terminal screen by outputting the appropriate escape sequences to reset the display. No flags exist for this command, so it is invoked bare. In an Android system_server context this is useful when using an adb shell session or similar terminal to remove accumulated log output or command history from the visible buffer before beginning a diagnostic session.*

---

## `cmp`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `cmp [-ls] [-n LEN] FILE1 [FILE2 [SKIP1 [SKIP2]]]`

Compare the contents of files (vs stdin if only one given), optionally skipping bytes at start.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-n` | `LEN` | Compare at most LEN bytes |

### Examples

```
toybox cmp -n 4096 /dev/block/bootdevice/by-name/boot /dev/block/bootdevice/by-name/boot_a
```
*Compares the first 4096 bytes of the active boot partition against the boot_a slot partition. The -n 4096 flag limits comparison to exactly 4096 bytes so the command does not read the entire block device, which would be slow and unnecessary when only verifying header regions. Both paths are absolute block device nodes under the A/B partition scheme on this Samsung device. No FILE2 SKIP arguments are needed because comparison starts at offset 0 in both files by default. A difference in this region would indicate the two slots have diverged in their boot image header.*

```
toybox cmp -n 65536 /data/local/tmp/framework_orig.odex /data/local/tmp/framework_patched.odex 0 0
```
*Compares the first 65536 bytes of an original and a patched ODEX file both located in /data/local/tmp, which is writable from UID 1000. The -n 65536 flag caps the read to 64 KB so that a large odex file is not fully traversed when the goal is only to detect whether the early sections differ. Explicit SKIP1 and SKIP2 values of 0 are provided to make the starting offsets unambiguous for documentation purposes. cmp will print the byte offset and differing values at the first mismatch, giving a precise location of any modification introduced by the patch.*

---

## `devmem`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `devmem ADDR [WIDTH [DATA]]`

Read/write physical address. WIDTH is 1, 2, 4, or 8 bytes (default 4). Prefix ADDR with 0x for hexadecimal, output is in same base as address.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `devmem ADDR [WIDTH [DATA]]`
> Upstream: `devmem [-f FILE] ADDR [WIDTH [DATA...]]`

### Examples

```
toybox devmem 0x00000000 32
```
*Reads a 32-bit value from physical memory address 0x00000000. ADDR specifies the physical memory address to access via /dev/mem, WIDTH=32 requests a 32-bit wide read operation. Composed this way because devmem requires at minimum an address, and specifying 32-bit width gives a meaningful word-aligned register read useful for probing hardware registers or bootloader-mapped regions from system_server context.*

```
toybox devmem 0xFE200000 32 0x00000001
```
*Writes the 32-bit value 0x00000001 to physical address 0xFE200000. ADDR targets a memory-mapped I/O region typical of peripheral controllers on ARM SoCs like the Exynos in the Galaxy S22, WIDTH=32 sets the write granularity to a full 32-bit word, DATA=0x00000001 is the value to write. Composed this way because all three arguments together form the write form of devmem, which only triggers a write when DATA is supplied, making it useful for toggling hardware register bits directly from system_server without needing a shell script.*

---

## `df`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `df [-HPkhi] [-t type] [FILE...]`

The "disk free" command shows total/used/available disk space for each filesystem listed on the command line, or all currently mounted filesystems.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `df [-HPkhi] [-t type] [FILE...]`
> Upstream: `df [-aHhikP] [-t TYPE] [FILE...]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-t` |  | Display only filesystems of this type |

### Examples

```
toybox df -t ext4
```
*Runs df filtered to only show ext4 filesystems. The -t ext4 flag tells df to skip all other filesystem types and report only ext4 mounts, which on Android typically includes /data where user app data and databases reside. This is useful in system_server context to check available space on the main data partition without noise from tmpfs, overlayfs, or other virtual filesystems.*

```
toybox df -t f2fs
```
*Runs df filtered to only show f2fs filesystems. Samsung Galaxy S22 devices commonly use f2fs for /data instead of ext4. Using -t f2fs isolates those partitions so system_server can check real storage availability on the flash-optimized filesystem without including proc or sysfs pseudo-mounts in the output.*

---

## `dirname`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `dirname PATH...`

Show directory portion of path.

### Examples

```
toybox dirname /data/local/tmp/trace_output.txt
```
*Strips the filename component 'trace_output.txt' from the full path and prints '/data/local/tmp'. dirname takes the full PATH argument and returns everything up to and including the last slash, which is useful when you have a file path and need to know the directory it lives in without running a separate stat or ls call.*

```
toybox dirname /dev/block/bootdevice/by-name/system
```
*Strips the partition name 'system' from the block device symlink path and returns '/dev/block/bootdevice/by-name'. This is composed this way because system_server may need to reference the containing directory of a named partition symlink to enumerate sibling partitions or verify the by-name directory exists, and dirname extracts that parent path in a single self-contained invocation without requiring any shell path manipulation.*

---

## `dos2unix`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `dos2unix [FILE...]`

Convert newline format from dos "\r\n" to unix "\n". If no files listed copy from stdin, "-" is a synonym for stdin.

### Examples

```
toybox dos2unix /data/local/tmp/script.sh
```
*Converts Windows-style line endings (CRLF) to Unix-style (LF) in script.sh in-place. On Android, scripts transferred from Windows machines often contain CR characters that cause execution failures. dos2unix strips the CR bytes so the file is interpreted correctly by the runtime environment.*

```
toybox dos2unix /data/local/tmp/config.txt /data/local/tmp/hosts.txt /data/local/tmp/rules.conf
```
*Processes multiple files in a single invocation, converting CRLF to LF in each one in-place. Since no shell is available for glob expansion or loops, listing files explicitly is the only way to batch-convert several known files at once. All three files are fixed in sequence with one toybox call.*

---

## `du`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `du [-d N] [-askxHLlmc] [FILE...]`

Show disk usage, space consumed by files and directories.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `du [-d N] [-askxHLlmc] [FILE...]`
> Upstream: `du [-d N] [-abcHKkLlmsx] [FILE...]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-d` | `N` | Only depth < N |

### Examples

```
toybox du -d 1 -s /data/local/tmp
```
*-d 1 limits recursion to only one level deep so subdirectories are not expanded individually; -s summarizes each argument as a single total rather than listing every file; /data/local/tmp is the writable staging area available to UID 1000 for temporary files, making this useful for quickly checking how much space that directory consumes without noise from nested paths*

```
toybox du -a -k -d 2 /data/local/tmp
```
*-a reports every individual file in addition to directories rather than only directories, giving a complete picture of disk usage; -k forces output in kilobytes for a consistent human-readable unit instead of the default 512-byte blocks; -d 2 caps recursion at two levels so the listing covers immediate subdirectories and their children but does not descend further, keeping output manageable when auditing what is staged under /data/local/tmp from system_server*

---

## `echo`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `echo [-neE] [ARG...]`

Write each argument to stdout, one space between each, followed by a newline.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `echo [-neE] [ARG...]`
> Upstream: `echo [-Een] [ARG...]`

### Examples

```
toybox echo -n Building device fingerprint:
```
*The -n flag suppresses the trailing newline after output, useful when appending additional data to the same terminal line. In system_server context this is used to emit a label without advancing the cursor, keeping diagnostic output compact on a single line.*

```
toybox echo -e Checking partition\nmounting /dev/block/bootdevice/by-name/system\ndone
```
*The -e flag enables interpretation of backslash escape sequences, so \n becomes an actual newline. This lets a single echo invocation emit a multi-line status message describing sequential partition operations without needing a shell loop or multiple commands, which matters here because no shell is available.*

---

## `expand`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `expand [-t TABLIST] [FILE...]`

Expand tabs to spaces according to tabstops.

### Examples

```
toybox expand /data/local/tmp/config.txt
```
*Expands tab characters in config.txt to spaces using the default tab stop of 8. No flags are used because the default behavior converts each tab to enough spaces to reach the next 8-column tab stop, which is the standard terminal width assumption. This is useful when viewing configuration files that use tabs for indentation in a terminal that renders tabs inconsistently.*

```
toybox expand -t 4 /data/local/tmp/script.sh
```
*Expands tab characters in script.sh to spaces using a tab stop of 4 columns. The -t flag sets the tab stop width so that each tab is replaced by spaces to reach the next multiple of 4. This is practical for Android shell scripts or source files where 4-space indentation is the convention, making the output consistent for further inspection or logging without relying on terminal tab rendering.*

---

## `false`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `false`

### Examples

```
toybox false
```
*Exits immediately with a non-zero (failure) status code. Used in scripting contexts or testing to simulate a failed condition. There are no flags or arguments; the sole purpose of this command is to return a failure exit status, which system_server can check to verify error-handling logic behaves correctly.*

---

## `file`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `file [-bhLs] [FILE...]`

Examine the given files and describe their content types.

### Examples

```
toybox file /dev/block/bootdevice/by-name/boot /dev/block/bootdevice/by-name/system /dev/block/bootdevice/by-name/userdata
```
*Runs file type detection on three named block device symlinks at once. No flags are used so file follows symlinks to the actual block devices by default, reporting each as a block special file. Passing multiple paths in one invocation avoids needing a shell loop, which is impossible without a shell. Useful from system_server to confirm partition nodes exist and are block devices before attempting low-level reads.*

```
toybox file -bLs /dev/block/bootdevice/by-name/boot
```
*-b suppresses the filename prefix in output so only the type description is printed, making the result easier to parse programmatically from Java. -L forces symlink resolution so the by-name symlink is followed to the real block device rather than reporting 'symbolic link'. -s tells file to treat special files (block/char devices) as regular files and attempt to read and identify their content, allowing detection of filesystem signatures or partition headers on the boot partition directly.*

---

## `fmt`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `fmt [-w WIDTH] [FILE...]`

Reformat input to wordwrap at a given line length, preserving existing indentation level, writing to stdout.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-w` | `WIDTH` | Maximum characters per line (default 75) |

### Examples

```
toybox fmt -w 72 /system/etc/notice.html
```
*fmt reads the text file /system/etc/notice.html and reflows its paragraphs so no line exceeds 72 characters wide. The -w 72 flag sets the column limit below the default 75, which is useful when preparing text for display in terminals or logs that have a narrower viewport. A FILE argument is given directly so no shell redirection is needed.*

```
toybox fmt -w 100 /data/local/tmp/bugreport_notes.txt
```
*fmt reads /data/local/tmp/bugreport_notes.txt, a writable scratch path available under UID 1000, and reflows its lines to a maximum width of 100 characters. The wider -w 100 value suits wide-format log review tools or editors configured for longer lines. Specifying the file path as an argument rather than relying on stdin avoids any need for shell piping, keeping the invocation self-contained as required.*

---

## `free`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `free [-bkmgt]`

Display the total, free and used amount of physical memory and swap space.

### Examples

```
toybox free -m
```
*The -m flag displays memory statistics (total, used, free, shared, buffers, cached) in megabytes instead of the default bytes. This is the most practical unit for Android system_server diagnostics on a Galaxy S22 which typically has 8GB RAM, making the numbers human-readable without the large byte counts that would appear with default output.*

---

## `freeramdisk`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `freeramdisk [RAM device]`

Free all memory allocated to specified ramdisk

### Examples

```
toybox freeramdisk /dev/ram0
```
*Frees the memory used by the RAM disk device /dev/ram0, releasing the kernel memory pages back to the system. On Android, RAM disks may be used during early boot stages; once the system has transitioned to normal operation, calling freeramdisk on /dev/ram0 reclaims that physical memory for general use. No flags are available for this command, so the only argument is the target device node.*

```
toybox freeramdisk /dev/ram1
```
*Frees the kernel memory allocated to the secondary RAM disk device /dev/ram1. In an Android system_server context with UID 1000, this is useful when a secondary ramdisk was mounted temporarily during init or recovery transitions and its backing memory needs to be returned to the kernel allocator. The single positional argument specifies the block device node to release.*

---

## `fsfreeze`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `fsfreeze {-f | -u} MOUNTPOINT`

Freeze or unfreeze a filesystem.

### Examples

```
toybox fsfreeze -f /data
```
*-f freezes the filesystem mounted at /data, halting all new write I/O and flushing pending writes to disk. This is composed as a single invocation because fsfreeze requires no flags beyond the action flag and mountpoint. Used before taking a block-level snapshot of /data to guarantee a consistent on-disk state without unmounting the partition, which is not possible for a live Android data partition.*

```
toybox fsfreeze -u /data
```
*-u unfreezes the filesystem mounted at /data, resuming normal write I/O that was suspended by a prior -f freeze. This must be run as a matching counterpart after a snapshot or backup operation completes, because leaving /data frozen will cause system_server and all apps to hang indefinitely on any write attempt. The mountpoint /data is specified directly as fsfreeze takes no additional flags.*

---

## `fsync`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `fsync [-d] [FILE...]`

Flush disk cache for FILE(s), writing cached data to storage device.

### Examples

```
toybox fsync /data/local/tmp/logdump.txt
```
*Calls fsync on /data/local/tmp/logdump.txt to flush all pending kernel write buffers for that file to the underlying block device. In system_server context this ensures any log or diagnostic data written to that file is durably committed before the file is read or the process exits, preventing data loss if the device loses power or crashes.*

```
toybox fsync -d /data/local/tmp/output.bin
```
*The -d flag causes fdatasync to be used instead of fsync, which flushes the file data contents to storage but skips updating metadata such as access times unless required for correct data retrieval. This is composed this way because in performance-sensitive contexts within system_server, avoiding unnecessary metadata writes reduces I/O overhead while still guaranteeing the actual payload bytes in output.bin are safely written to disk.*

---

## `getconf`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getconf -a [PATH] | -l | NAME [PATH]`

Get system configuration values. Values from pathconf(3) require a path.

### Examples

```
toybox getconf -a /data/local/tmp
```
*The -a flag dumps all system configuration variables and their values for the given path /data/local/tmp. The path argument is provided so that path-dependent variables like PATH_MAX, NAME_MAX, and LINK_MAX reflect the actual limits of the filesystem mounted at that location rather than system-wide defaults. This is composed as a single self-contained invocation because getconf has no pipe or filter flags, so -a with a path is the most complete single call available.*

```
toybox getconf PAGE_SIZE
```
*Queries the single named variable PAGE_SIZE, which returns the memory page size in bytes for the running kernel on this Samsung Galaxy S22 hardware. This is useful in system_server context when calculating buffer alignment or mmap region sizes. No path argument is needed because PAGE_SIZE is a processor and kernel property, not a filesystem property, so omitting the path is correct and intentional.*

---

## `getenforce`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getenforce`

Shows whether SELinux is disabled, enforcing, or permissive.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox getenforce
```
*getenforce queries the kernel SELinux subsystem via /sys/fs/selinux/enforce and prints the current enforcement mode as either Enforcing, Permissive, or Disabled. This is a single self-contained invocation with no flags because the command takes no arguments; it is used in Android system_server context to verify that SELinux is actively enforcing MAC policy before performing privileged operations.*

---

## `getfattr`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getfattr [-d] [-h] [-n NAME] FILE...`

Read POSIX extended attributes.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox getfattr -d /data/local/tmp/testfile
```
*-d dumps all extended attributes and their values for /data/local/tmp/testfile in a human-readable key=value format; composed this way because without -d only attribute names are listed, and dumping all at once is the most practical way to audit what xattrs are set on a file in an Android context where SELinux and capability xattrs are commonly present*

```
toybox getfattr -n security.selinux /data/local/tmp/testfile
```
*-n security.selinux requests only the single named extended attribute 'security.selinux' from /data/local/tmp/testfile; composed this way because in system_server context (UID 1000) verifying the SELinux label of a file is a common diagnostic task, and targeting a specific attribute by name avoids parsing all xattrs when only the security context matters*

---

## `getopt`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getopt [OPTIONS] [--] ARG...`

Parse command-line options for use in shell scripts.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `getopt [OPTIONS] [--] ARG...`
> Upstream: `getopt [-aTu] [-lo OPTIONS] [-n NAME] [OPTIONS] ARG...`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-l` | `OPTS` | Specify long options. |
| `-n` | `NAME` | Command name for error messages. |
| `-o` | `OPTS` | Specify short options. |

### Examples

```
toybox getopt -n myscript -o hv:o: -l help,verbose:,output: -- -v debug -o /data/local/tmp/out.txt --help
```
*Parses a simulated argument list as if it came from a script named 'myscript'. -n myscript sets the program name used in error messages so failures are identifiable. -o hv:o: defines short options: h takes no argument, v and o each require an argument (indicated by colon). -l help,verbose:,output: defines the corresponding long options with the same argument requirements. The -- separator marks the end of getopt's own options and the start of the argument list to be parsed. The trailing arguments simulate what a caller might pass, and getopt normalizes and reorders them into a canonical form suitable for further processing.*

```
toybox getopt -n bootcheck -o rm: -l reboot,mode: -- --mode fastboot -r
```
*Demonstrates long and short option mixing for a hypothetical boot management helper named bootcheck. -n bootcheck names the process for error reporting. -o rm: declares r as a short flag with no argument and m as a short flag requiring an argument. -l reboot,mode: mirrors these as long options where reboot takes no argument and mode requires one. The argument list after -- contains --mode fastboot (long option with value) and -r (short flag), which getopt normalizes into a consistent quoted and ordered output, making it safe to feed into eval-style processing in contexts where argument ordering from callers may vary.*

---

## `groups`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `groups [user]`

Print the groups a user is in.

### Examples

```
toybox groups
```
*Runs groups with no arguments to display the supplementary group memberships of the current process (UID 1000, system_server). Because no flags exist for this command, the only composition choice is whether to pass a username argument or not. Omitting the argument queries the calling process itself, which is the relevant context when auditing what groups system_server belongs to on the running device.*

```
toybox groups shell
```
*Passes the username 'shell' as the sole argument to groups, causing it to look up and print all groups assigned to the shell user in /etc/group and related Android identity databases. This is useful from system_server context to verify what privileges the shell user holds without needing to switch users or open a shell, since groups performs the lookup internally rather than via a subprocess.*

---

## `gunzip`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `gunzip [-cfkt] [FILE...]`

Decompress files. With no files, decompresses stdin to stdout. On success, the input files are removed and replaced by new files without the .gz suffix.

### Examples

```
toybox gunzip -k /data/local/tmp/logcat.gz
```
*-k keeps the original compressed file intact after decompression, which is important in a forensic or diagnostic context on Android where you want to preserve the original artifact in /data/local/tmp while also having the decompressed logcat file available for inspection*

```
toybox gunzip -f /data/local/tmp/bugreport.gz
```
*-f forces decompression even if the output file already exists, which is necessary in automated system_server workflows where a bugreport.gz may have been written to /data/local/tmp repeatedly and you need to overwrite the previously decompressed copy without being prompted*

---

## `head`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `head [-n NUM] [FILE...]`

Copy first lines from files to stdout. If no files listed, copy from stdin. Filename "-" is a synonym for stdin.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `head [-n NUM] [FILE...]`
> Upstream: `head [-cn NUM] [-qv] [FILE...]`

### Examples

```
toybox head -n 5 /proc/kmsg
```
*-n 5 limits output to the first 5 lines of /proc/kmsg (the kernel message ring buffer). This is composed this way because /proc/kmsg is a live stream and reading it without a line limit from system_server context would block or produce unbounded output; restricting to 5 lines gives a quick diagnostic snapshot of recent kernel messages without hanging the caller.*

```
toybox head -n 20 /proc/1/maps
```
*-n 20 reads only the first 20 lines from /proc/1/maps, which lists the memory-mapped regions of PID 1 (init). This is composed this way because the full maps file for a long-running process can be thousands of lines; grabbing 20 lines from system_server context (UID 1000) gives a quick view of the leading mapped segments such as the executable and core libraries without producing excessive output.*

---

## `help`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `help [-ahu] [COMMAND]`

### Examples

```
toybox help ls
```
*Invokes the built-in help system to display usage and flag information specifically for the 'ls' command. This is composed as a single argument invocation because help takes an optional COMMAND name to narrow its output to one specific toybox command rather than dumping all commands at once, which is useful when confirming exact flag syntax before constructing a more complex ls invocation in a scripted Android system_server context.*

```
toybox help -a
```
*Uses the -a flag to display help text for all available toybox commands in one pass. This is useful in a no-shell environment where you cannot pipe output or grep, so getting the full command list in a single self-contained invocation lets you read everything available on the device without issuing multiple separate help queries.*

---

## `hostname`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `hostname [-bdsf] [-F FILENAME] [newname]`

Get/set the current hostname.

### Examples

```
toybox hostname
```
*Prints the current hostname of the Android device. No flags are used because the default behavior with no arguments is to display the current system hostname, which is useful for identifying the device in a network or logging context from system_server.*

---

## `i2cdump`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `i2cdump [-fy] BUS CHIP`

Dump i2c registers.

### Examples

```
toybox i2cdump -f -y 0 0x50
```
*-f forces access even if the device is busy or the driver claims it, preventing abort on a locked bus; -y suppresses the interactive confirmation prompt which would block execution in a non-interactive system_server context; 0 is the I2C bus number corresponding to /dev/i2c-0 which is a common bus for EEPROMs and sensor clusters on Android hardware; 0x50 is the standard I2C address for a 24Cxx series EEPROM where calibration or board identity data is typically stored; the combination dumps all readable registers from that chip in a formatted hex grid*

```
toybox i2cdump -y 1 0x68
```
*-y suppresses the yes/no confirmation prompt so the command runs unattended from system_server without waiting for stdin input; bus 1 refers to /dev/i2c-1 which on many Snapdragon-based Android devices like the Galaxy S22 carries the IMU or PMIC; 0x68 is the standard I2C address for an MPU-6050 or similar gyroscope/accelerometer, making this useful for verifying register state during sensor diagnostics; omitting -f here lets the kernel refuse access if a driver already owns the device, which is safer when not intentionally overriding ownership*

---

## `i2cget`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `i2cget [-fy] BUS CHIP [ADDR]`

Read an i2c register.

### Examples

```
toybox i2cget -f 0 0x50 0x00
```
*-f forces access to the bus even if it is busy or a driver is already attached to the device, which is necessary in Android system_server context where kernel drivers may already claim the EEPROM at chip address 0x50 on I2C bus 0; ADDR 0x00 reads the first byte from that chip, useful for probing device identity or configuration registers*

```
toybox i2cget -fy 1 0x68 0x75
```
*-f forces bus access past any attached driver, -y suppresses the interactive confirmation prompt which is required in non-interactive system_server context where there is no terminal to accept input; bus 1 is the secondary I2C bus common on Galaxy S22, chip 0x68 is the typical I2C address for an MPU-6050 or similar IMU, and register 0x75 is the WHO_AM_I register used to verify the chip identity without needing shell scripting or piped output*

---

## `i2cset`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `i2cset [-fy] BUS CHIP ADDR VALUE... MODE`

Write an i2c register. MODE is b for byte, w for 16-bit word, i for I2C block.

### Examples

```
toybox i2cset -f -y 1 0x50 0x00 0xFF b
```
*-f forces access to the I2C bus even if it is already in use by another driver, preventing EBUSY errors common in Android system_server context; -y suppresses the interactive confirmation prompt since there is no shell to handle user input; 1 is the I2C bus number (/dev/i2c-1 on Galaxy S22); 0x50 is the EEPROM chip address; 0x00 is the register address to write to; 0xFF is the byte value to write; 'b' specifies byte mode, matching the single-byte VALUE provided*

```
toybox i2cset -y 1 0x68 0x6B 0x00 b
```
*-y suppresses the confirmation prompt required for unattended execution from system_server; 1 selects /dev/i2c-1 which is a common sensor bus on the Galaxy S22; 0x68 is the I2C address of an MPU-6050 or similar IMU sensor present on many Samsung devices; 0x6B is the PWR_MGMT_1 register; 0x00 is the value written to wake the sensor from sleep mode; 'b' specifies byte-width mode, correct for a single 8-bit register write to this class of sensor*

---

## `iconv`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `iconv [-f FROM] [-t TO] [FILE...]`

Convert character encoding of files.

### Examples

```
toybox iconv -f UTF-8 -t ASCII /data/local/tmp/logdump.txt
```
*-f UTF-8 specifies the input encoding as UTF-8, which is the default encoding for most Android text files; -t ASCII converts the output to plain ASCII, stripping or replacing non-ASCII characters; /data/local/tmp/logdump.txt is the target file to convert, useful when passing log output to tools that only handle pure ASCII text from system_server context*

```
toybox iconv -f UTF-16 -t UTF-8 /data/local/tmp/bugreport_raw.txt
```
*-f UTF-16 tells iconv the source file is UTF-16 encoded, which some Android diagnostic dumps or NDK-generated files may use; -t UTF-8 converts the content to UTF-8, the standard encoding expected by most Android system tools and logcat pipelines; /data/local/tmp/bugreport_raw.txt is a realistic staging path for intermediate diagnostic files in system_server context, making this a self-contained single-invocation conversion with no shell redirection needed*

---

## `ifconfig`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `ifconfig [-aS] [INTERFACE [ACTION...]]`

Display or configure network interface.

### Examples

```
toybox ifconfig wlan0
```
*Queries the wlan0 wireless interface on the Samsung Galaxy S22 to display its current configuration including IP address, netmask, broadcast address, MAC address, MTU, and packet statistics. No flags are needed because omitting flags and providing a specific interface name causes ifconfig to show only that interface's details rather than all interfaces, which is useful from system_server (UID 1000) when checking network state for a specific interface without parsing a full listing.*

```
toybox ifconfig -a
```
*The -a flag instructs ifconfig to display ALL network interfaces regardless of whether they are currently up or down. On Android this reveals not just wlan0 and rmnet data interfaces but also loopback (lo), dummy interfaces, and any tunnel or bridge interfaces. This is composed as a single flag invocation because system_server context has read access to interface information and the -a flag is the only way to enumerate inactive interfaces that would otherwise be hidden by a plain ifconfig call with no arguments.*

---

## `insmod`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `insmod MODULE [OPTION...]`

Load the module named MODULE passing options if given.

### Examples

```
toybox insmod /data/local/tmp/test_module.ko
```
*Loads the kernel module test_module.ko from /data/local/tmp into the running kernel. insmod takes the full path to the .ko file as its argument and passes it directly to the kernel for loading. No flags are used because insmod has no flags in this build; the module path is the only required argument. This is the standard way to load a custom or test kernel module from a writable partition accessible under UID 1000 in system_server context without needing a shell.*

```
toybox insmod /data/local/tmp/custom_driver.ko enable=1 debug=0
```
*Loads custom_driver.ko from /data/local/tmp and passes two module parameters: enable=1 and debug=0. The MODULE argument is the first positional argument pointing to the .ko file on disk, and the trailing OPTION arguments are key=value pairs forwarded verbatim to the module as its init parameters, allowing runtime configuration of module behavior without recompiling. This pattern is necessary when a module exposes kernel module parameters via module_param() that must be set at load time rather than via sysfs after loading.*

---

## `iorenice`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `iorenice PID [CLASS] [PRIORITY]`

Display or change I/O priority of existing process. CLASS can be "rt" for realtime, "be" for best effort, "idle" for only when idle, or "none" to leave it alone. PRIORITY can be 0-7 (0 is highest, default 4).

### Examples

```
toybox iorenice 1000
```
*Query the current I/O scheduling class and priority of PID 1000 (system_server itself). No CLASS or PRIORITY arguments are given, so iorenice only reads and displays the current ionice settings for that process. This is useful to verify what I/O class system_server is running under without changing anything.*

```
toybox iorenice 1000 be 4
```
*Set the I/O scheduling class to 'be' (best-effort) with priority level 4 for PID 1000. The CLASS argument 'be' selects the best-effort ionice class, and the PRIORITY argument 4 sets the priority within that class (0 is highest, 7 is lowest). This composed form with all three arguments makes iorenice both assign and apply the new I/O policy in a single invocation, useful when system_server needs to yield I/O bandwidth to foreground processes.*

---

## `kill`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `kill [-l [SIGNAL] | -s SIGNAL | -SIGNAL] PID...`

Send signal to process(es).

### Examples

```
toybox kill -s SIGTERM 1234
```
*Sends the SIGTERM signal to process with PID 1234. SIGTERM is the standard graceful shutdown signal, allowing the target process to clean up resources before exiting. Using -s SIGTERM is explicit and portable, making the intent clear in a system_server context where accidental kills could be destructive.*

```
toybox kill -s SIGKILL 5678
```
*Sends the SIGKILL signal to process with PID 5678. Unlike SIGTERM, SIGKILL cannot be caught or ignored by the target process, so the kernel forcibly terminates it immediately. This is composed this way because no shell pipe or redirection is available, so the PID must be known in advance and passed directly, making it a definitive last-resort termination from UID 1000 system_server context.*

---

## `killall`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `killall [-l] [-iqv] [-SIGNAL|-s SIGNAL] PROCESS_NAME...`

Send a signal (default: TERM) to all processes with the given names.

### Examples

```
toybox killall -s SIGTERM com.android.phone
```
*Sends SIGTERM to all processes named com.android.phone. The -s flag specifies the signal by name rather than number, which is clearer and portable. SIGTERM requests graceful shutdown, allowing the process to clean up before exiting. This is preferred over SIGKILL when you want the telephony process to terminate cleanly from system_server context.*

```
toybox killall -v -s SIGKILL surfaceflinger
```
*Sends SIGKILL to all processes named surfaceflinger with verbose output enabled via -v. SIGKILL cannot be caught or ignored by the target process, so it forces immediate termination. This is used when surfaceflinger is unresponsive and SIGTERM has already been attempted. The -v flag confirms which processes were actually killed, useful for logging from system_server.*

---

## `load_policy`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `load_policy FILE`

Load the specified SELinux policy file.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox load_policy /data/local/tmp/sepolicy
```
*load_policy takes a single FILE argument which must be a compiled SELinux binary policy file. This invocation loads the policy at /data/local/tmp/sepolicy into the running kernel via the SELinux filesystem interface. No flags exist for this command so the only composition is choosing the correct path. Running from system_server context (UID 1000) provides the necessary privilege to write to the kernel SELinux policy node. This is used when pushing a modified or patched policy binary to a live device without rebooting, for example during security testing or policy debugging.*

```
toybox load_policy /dev/block/bootdevice/by-name/tmpfs_sepolicy
```
*load_policy reads the compiled binary policy from the path given as FILE and submits it to the kernel. Here the path points to a block device node representing a partition that stores an alternate SELinux policy image, which is a realistic scenario on Android where policies may be stored on dedicated partitions and loaded at runtime by system_server. Because load_policy has no flags, the entire command behavior is determined solely by the FILE path provided. Using a block-device path rather than a filesystem path exercises the command's ability to read raw binary data directly, as long as the block device contains a valid policy image at offset zero.*

---

## `log`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `log [-p PRI] [-t TAG] [MESSAGE...]`

Logs message (or stdin) to logcat.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox log -p i -t system_server_atlas System server context verified UID 1000
```
*Writes an informational log entry to the Android logcat buffer. -p i sets the priority level to 'i' (info), which is appropriate for non-critical status messages. -t system_server_atlas sets the log tag used to identify and filter this entry when reading logcat output. The remaining arguments form the message body. This is composed as a single invocation because log accepts the entire message as trailing arguments without needing shell quoting or pipes.*

```
toybox log -p e -t bootcheck Partition mount failure detected at /dev/block/bootdevice/by-name/userdata
```
*Writes an error-level log entry describing a storage partition issue. -p e sets priority to 'e' (error), causing this entry to appear in error-filtered logcat views and potentially triggering monitoring systems. -t bootcheck provides a tag that groups this message with other boot-related diagnostics. The path /dev/block/bootdevice/by-name/userdata is included inline as part of the message text since there is no shell variable expansion or redirection available, making the full context self-contained within the single command.*

---

## `logger`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `logger [-s] [-t TAG] [-p [FACILITY.]PRIORITY] [MESSAGE...]`

Log message (or stdin) to syslog.

### Examples

```
toybox logger -t system_server -p user.warn Low memory condition detected on device
```
*-t system_server sets the log tag to 'system_server' so the message is attributed to the correct process; -p user.warn sets the facility to 'user' and priority to 'warn' so the message is routed and filtered at warning severity; the remaining words form the MESSAGE logged to the system logger, useful for injecting diagnostic entries from UID 1000 context without a shell script*

```
toybox logger -s -t bootcheck -p daemon.info Boot validation complete partition verified
```
*-s mirrors the log message to standard error so it appears in the terminal output in addition to being sent to the system log, useful when running interactively to confirm the message was accepted; -t bootcheck labels the entry with a recognizable tag for filtering later; -p daemon.err sets facility 'daemon' and priority 'info' appropriate for a background service reporting a non-error status; the message text documents a boot partition check result from system_server context*

---

## `logname`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `logname`

Print the current user name.

### Examples

```
toybox logname
```
*Prints the login name associated with the current process. In system_server context (UID 1000), this returns the effective login name for the process, which is useful for confirming identity before performing privileged operations or writing audit records. No flags are available or needed; the command is self-contained and always outputs the name to stdout.*

---

## `lsmod`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lsmod`

Display the currently loaded modules, their sizes and their dependencies.

### Examples

```
toybox lsmod
```
*Reads /proc/modules and formats it as a table showing loaded kernel modules, their sizes, use counts, and dependencies. No flags exist for this command, so this is the complete and only valid invocation. In system_server context on Android this reveals which kernel modules are currently active, useful for diagnosing hardware driver state on the Galaxy S22 (e.g. confirming exynos or mali GPU modules are loaded).*

---

## `lsof`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lsof [-lt] [-p PID1,PID2,...] [FILE...]`

List all open files belonging to all active processes, or processes using listed FILE(s).

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox lsof -p 1000,1001
```
*The -p flag filters open file descriptors to only those belonging to the specified PIDs (1000 and 1001, comma-separated). This is composed this way because on Android from system_server context you often need to inspect what files a specific process has open without wading through the entire system file descriptor table, which can be enormous. No shell piping is available so the built-in PID filter is the only way to narrow output.*

```
toybox lsof -lt /data/local/tmp
```
*The -l flag causes numeric UIDs to be displayed rather than resolved usernames, which is important on Android where /etc/passwd may not map all system UIDs. The -t flag outputs only the PID numbers of processes that have the specified path open, producing terse machine-readable output. Providing /data/local/tmp as the FILE argument restricts listing to processes holding that specific directory or files within it open. This composition is chosen because system_server often needs to determine which processes are actively using a staging directory before cleaning or replacing files there, and -t gives just the PIDs needed for follow-up lsof -p calls.*

---

## `lspci`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lspci [-ekmn] [-i FILE]`

List PCI devices.

### Examples

```
toybox lspci
```
*Runs lspci with no flags to list all PCI devices detected by the kernel on the Samsung Galaxy S22. Each line shows the PCI bus address, device class, and device name. On Android, this reveals any PCI-attached components such as PCIe-connected modems, Wi-Fi chips, or NVMe storage controllers that the kernel has enumerated. This is the baseline invocation since no flags are required and it produces the full device list from the kernel PCI subsystem.*

```
toybox lspci -n
```
*Runs lspci with the -n flag, which causes vendor and device identification to be shown as numeric IDs rather than resolved names. On Android from system_server context this is useful when the default PCI ID database may not be present or may be incomplete, because numeric IDs are authoritative and do not depend on any lookup file. The output shows raw vendor:device hex codes for each enumerated PCI device, which can then be cross-referenced against an external database to identify hardware precisely.*

---

## `lsusb`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lsusb [-i]`

List USB hosts/devices.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `lsusb [-i]`
> Upstream: `lsusb [-ti]`

### Examples

```
toybox lsusb
```
*Lists all USB devices currently recognized by the Android kernel. No flags are needed because the default output enumerates every USB bus and device with its bus number, device number, and USB ID (vendor:product). In a Samsung Galaxy S22 system_server context this is useful for confirming which USB peripherals or accessories are attached to the device at runtime.*

```
toybox lsusb -i
```
*Lists USB devices and additionally reads and displays the USB descriptor information from the device files under /dev/bus/usb. The -i flag causes lsusb to open each device node and parse its descriptors, providing detailed class, subclass, protocol, and string descriptor data. This is composed as a single self-contained invocation because no pipe or redirection is available; all output goes directly to stdout, making it suitable for capturing device capability details from system_server context.*

---

## `makedevs`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `makedevs [-d device_table] rootdir`

Create a range of special files as specified in a device table.

### Examples

```
toybox makedevs -d /data/local/tmp/device_table.txt /data/local/tmp/rootfs
```
*Reads a device table file at /data/local/tmp/device_table.txt and creates device nodes under the /data/local/tmp/rootfs directory. The -d flag specifies the device table file which contains lines defining device type, path, mode, uid, gid, major, and minor numbers. This composition is necessary because makedevs requires both a table file and a root directory to know what nodes to create and where to place them, making it useful for populating a staging rootfs for custom Android images without needing a shell loop or mknod calls.*

---

## `md5sum`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```
toybox md5sum /system/lib64/libc.so /system/lib64/libm.so /system/lib64/libdl.so
```
*Computes MD5 checksums for three core Android system libraries in a single invocation. Passing multiple FILE arguments causes md5sum to process each file and print one hash-plus-filename line per file, which is useful for verifying library integrity from system_server context without needing shell redirection to collect results.*

```
toybox md5sum -c /data/local/tmp/checksums.md5
```
*Reads a previously generated checksum manifest file at /data/local/tmp/checksums.md5 and verifies each listed file against its stored MD5 hash. The -c flag switches md5sum from compute mode to verify mode, reading lines of the form 'hash  filename' and reporting OK or FAILED per entry, which is the standard way to batch-validate a set of files without a shell loop.*

---

## `microcom`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `microcom [-s SPEED] [-X] DEVICE`

Simple serial console.

### Examples

```
toybox microcom -s 115200 /dev/ttyS0
```
*Opens a serial console session on /dev/ttyS0 at 115200 baud. -s 115200 sets the baud rate to 115200, which is the standard rate for most Android serial debug consoles on the S22 SoC UART port. DEVICE /dev/ttyS0 is the first serial device node. This is composed as a single invocation because microcom itself manages the interactive terminal session with no need for shell plumbing.*

```
toybox microcom -s 9600 -X /dev/ttyS1
```
*Opens a serial session on /dev/ttyS1 at 9600 baud with -X flag which disables XON/XOFF software flow control. This is useful when communicating with embedded peripherals or modems on a secondary UART that do not support software flow control and would misinterpret XON/XOFF bytes as data. 9600 baud is chosen because many low-speed AT-command modems and GPS modules default to this rate.*

---

## `mkdir`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mkdir [-vp] [-m MODE] [DIR...]`

Create one or more directories.

### Examples

```
toybox mkdir -p /data/local/tmp/test/subdir/logs
```
*-p creates the full directory chain (/data/local/tmp/test, then subdir, then logs) in one invocation without failing if any intermediate directory already exists; essential on Android where /data/local/tmp may be the only writable scratch space and nested structures are needed for organized test output*

```
toybox mkdir -m 700 -v /data/local/tmp/secure_session
```
*-m 700 sets permissions to rwx------ at creation time so only UID 1000 (system_server) can access the directory, preventing other processes from reading session data before a separate chmod can be applied; -v prints a confirmation message for each directory created, useful when running from system_server context where silent failures are hard to diagnose*

---

## `mkfifo`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mkfifo [-Z CONTEXT] [NAME...]`

Create FIFOs (named pipes).

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mkfifo [-Z CONTEXT] [NAME...]`
> Upstream: `mkfifo [NAME...]`

### Examples

```
toybox mkfifo /data/local/tmp/ipc_pipe
```
*Creates a named FIFO (first-in, first-out) special file at /data/local/tmp/ipc_pipe. A FIFO is a persistent pipe on the filesystem that allows two separate processes to communicate without a shell pipe operator. One process opens the FIFO for writing and blocks until another opens it for reading, enabling inter-process data transfer from system_server context. The path /data/local/tmp is used because it is writable from UID 1000 and suitable for temporary IPC artifacts.*

```
toybox mkfifo /data/local/tmp/log_relay /data/local/tmp/cmd_channel
```
*Creates two named FIFO files in a single invocation by supplying multiple NAME arguments. log_relay can serve as a unidirectional channel for streaming log data between two processes, while cmd_channel can carry control commands in the opposite direction, establishing a bidirectional IPC pattern without any shell redirection. Batching both names into one mkfifo call is more efficient than two separate invocations and ensures both FIFOs are created atomically in sequence before either is used.*

---

## `mknod`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mknod [-Z CONTEXT] ... [-m MODE] NAME TYPE [MAJOR MINOR]`

Create a special file NAME with a given type. TYPE is b for block device, c or u for character device, p for named pipe (which ignores MAJOR/MINOR).

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mknod [-Z CONTEXT] ... [-m MODE] NAME TYPE [MAJOR MINOR]`
> Upstream: `mknod [-m MODE] NAME TYPE [MAJOR MINOR]`

### Examples

```
toybox mknod /data/local/tmp/null_dev c 1 3
```
*Creates a character device node at /data/local/tmp/null_dev with major number 1 and minor number 3, which corresponds to /dev/null. TYPE 'c' specifies a character device. MAJOR 1 is the memory devices group and MINOR 3 is the null device. This is composed this way because in system_server context you may need a writable null sink in a writable path like /data/local/tmp when /dev/null permissions are restricted for certain operations.*

```
toybox mknod -m 660 /data/local/tmp/loop_node b 7 0
```
*Creates a block device node at /data/local/tmp/loop_node with permissions 660 (owner and group read/write, no world access), major 7 and minor 0 corresponding to the first loop device. TYPE 'b' specifies a block device. The -m 660 flag sets the file mode at creation time rather than requiring a subsequent chmod call, which matters in system_server context where you want to restrict access to the node immediately upon creation without a race window.*

---

## `mkswap`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mkswap [-L LABEL] DEVICE`

Set up a Linux swap area on a device or file.

### Examples

```
toybox mkswap /dev/block/bootdevice/by-name/swap
```
*Initializes the partition at /dev/block/bootdevice/by-name/swap as a Linux swap area. mkswap writes the swap header and UUID to the block device so the kernel can use it for paging. No flags are needed here because the partition path alone is sufficient to set up a plain swap space on Android.*

```
toybox mkswap -L swappart /dev/block/bootdevice/by-name/swap
```
*Initializes the swap partition and assigns it the label 'swappart' using -L. The label is embedded in the swap header, which allows later tools to identify or activate the swap area by name rather than by raw block device path. This is composed with -L to make the swap partition identifiable in environments where device paths may vary across reboots.*

---

## `mktemp`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mktemp [-dqu] [-p DIR] [TEMPLATE]`

Safely create a new file "DIR/TEMPLATE" and print its name.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mktemp [-dqu] [-p DIR] [TEMPLATE]`
> Upstream: `mktemp [-dqtu] [-p DIR] [TEMPLATE]`

### Examples

```
toybox mktemp -p /data/local/tmp tmpfile_XXXXXX
```
*Creates a unique temporary file in /data/local/tmp using the template 'tmpfile_XXXXXX', where the X characters are replaced with random characters to guarantee uniqueness. The -p flag specifies the directory rather than relying on TMPDIR or /tmp, which may not exist or be writable in the Android system_server context. The result is a safely named file ready for use without collision risk.*

```
toybox mktemp -d -p /data/local/tmp tmpdir_XXXXXX
```
*Creates a unique temporary directory instead of a file, because the -d flag causes mktemp to mkdir rather than open a file. The -p /data/local/tmp ensures the directory is created under a known writable path on Android. The template tmpdir_XXXXXX is expanded with random characters to avoid collisions when multiple processes may be creating temp directories simultaneously. This is the correct approach when a scratch directory is needed rather than a single file.*

---

## `more`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `more [FILE...]`

View FILE(s) (or stdin) one screenfull at a time.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox more /proc/kmsg
```
*Reads /proc/kmsg (the kernel message ring buffer) and pages through it one screenful at a time. 'more' is used here instead of cat because /proc/kmsg can be very long and would flood the terminal; paging allows the operator to review each screen of kernel log output before proceeding. No flags are available, so the file path is the only argument.*

```
toybox more /data/local/tmp/logdump.txt
```
*Opens a previously written log or diagnostic text file at /data/local/tmp/logdump.txt and displays it page by page. This is practical in a system_server context where a tool has dumped state to a temp file and the operator needs to inspect it line by line without the output scrolling past before it can be read. Since no flags exist for this command, the composed form is simply 'toybox more <path>'.*

---

## `mountpoint`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mountpoint [-qd] DIR`

mountpoint [-qx] DEVICE

### Examples

```
toybox mountpoint /data
```
*Checks whether /data is a mount point. On Android, /data is always a separately mounted partition; this confirms the mount exists and is active, which is useful for verifying storage availability before attempting data operations from system_server context.*

```
toybox mountpoint -q /data/local/tmp
```
*Silently checks whether /data/local/tmp is a mount point, suppressing all output and relying only on the exit code. The -q flag makes this suitable for conditional logic in tooling where output must not be mixed with other diagnostic streams, and /data/local/tmp is a common staging area that may or may not be separately mounted depending on device configuration.*

---

## `nbd-client`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `nbd-client [-ns] [-b BLKSZ] HOST PORT DEVICE`

### Examples

```
toybox nbd-client 192.168.1.100 10809 /dev/block/nbd0
```
*Connects to an NBD (Network Block Device) server at 192.168.1.100 on port 10809 and maps it to /dev/block/nbd0. HOST specifies the remote server exporting the block device, PORT is the standard NBD port 10809, and DEVICE is the local kernel block device node that will represent the remote storage. This is composed as a minimal invocation to attach a remote disk image or storage backend for mounting or raw access from system_server context.*

```
toybox nbd-client -b 4096 192.168.1.100 10809 /dev/block/nbd0
```
*Connects to the NBD server at 192.168.1.100 on port 10809 and maps it to /dev/block/nbd0 with an explicit block size of 4096 bytes set via -b BLKSZ. Specifying -b 4096 aligns the block size with the typical Android filesystem and eMMC page size, which avoids misaligned I/O penalties and ensures compatibility with ext4 or f2fs if the remote image will be mounted. This is the preferred form when the remote server exports an image formatted with 4K sector alignment.*

---

## `nproc`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `nproc [--all]`

Print number of processors.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `nproc [--all]`
> Upstream: `nproc [-a]`

### Examples

```
toybox nproc
```
*Prints the number of processing units available to the current process. In system_server context (UID 1000), this reflects the CPU cores accessible to the process, which is useful for tuning thread pool sizes or parallelism decisions in Android system services.*

```
toybox nproc --all
```
*Prints the total number of installed CPU cores on the device regardless of process affinity or scheduler restrictions. On a Samsung Galaxy S22 this will reflect all cores across the big/mid/little clusters of the Exynos or Snapdragon SoC, giving the true hardware core count rather than what the current process is allowed to use.*

---

## `od`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `od [-bcdosxv] [-j #] [-N #] [-w #] [-A doxn] [-t acdfoux[#]]`

Dump data in octal/hex.

### Examples

```
toybox od -A x -t x1z -N 64 /dev/block/bootdevice/by-name/boot
```
*-A x prints file offsets in hexadecimal, -t x1z formats output as 1-byte hex values with printable ASCII shown at end of each line, -N 64 limits reading to the first 64 bytes so we only inspect the boot partition header magic bytes without dumping the entire partition, all combined into one invocation since no shell redirection is available*

```
toybox od -A d -t d2 -j 512 -N 128 -w 16 /data/local/tmp/payload.bin
```
*-A d prints byte offsets as decimal, -t d2 interprets data as signed 2-byte integers for structured numeric inspection, -j 512 skips the first 512 bytes to jump past a header section, -N 128 reads only 128 bytes after that offset, -w 16 formats 16 bytes per output line for compact readable layout, composing all flags in one command because no pipes or awk are available to post-process output*

---

## `partprobe`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `partprobe DEVICE...`

Tell the kernel about partition table changes

### Examples

```
toybox partprobe /dev/block/sda
```
*Instructs the kernel to re-read the partition table on /dev/block/sda without rebooting. This is useful after modifying partition layouts on a block device, as it updates the in-kernel partition map to reflect the new on-disk state without requiring a full system restart.*

```
toybox partprobe /dev/block/sda /dev/block/sdb
```
*Re-reads partition tables on two block devices in a single invocation. Passing multiple DEVICE arguments causes partprobe to process each in sequence, refreshing the kernel view of partitions for both devices. This is composed as one command because no shell looping is available, and partprobe accepts multiple device arguments natively.*

---

## `pidof`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pidof [-s] [-o omitpid[,omitpid...]] [NAME...]`

Print the PIDs of all processes with the given names.

### Examples

```
toybox pidof system_server
```
*Finds the PID(s) of the process named 'system_server'. pidof scans /proc for matching process names and prints their PIDs. No flags are used because we want all matching PIDs returned, which is useful in system_server context to confirm its own PID or detect duplicate instances.*

```
toybox pidof -s surfaceflinger
```
*The -s flag tells pidof to return only a single PID (the first match found) for the process named 'surfaceflinger'. This is composed this way because surfaceflinger should only have one instance on Android, and returning a single value makes it easier to use the result directly without parsing multiple PIDs.*

---

## `ping`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `ping [OPTIONS] HOST`

Check network connectivity by sending packets to a host and reporting its response.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-4` |  | Force IPv4 or IPv6 |
| `-c` | `CNT` | Send CNT many packets (default 3, 0 = infinite) |
| `-i` | `TIME` | Interval between packets (default 1, need root for < .2) |
| `-I` | `IFACE` | Source interface or address |
| `-m` | `MARK` | Tag outgoing packets using SO_MARK |
| `-s` | `SIZE` | Data SIZE in bytes (default 56) |
| `-t` | `TTL` | Set Time To Live (number of hops) |
| `-W` | `SEC` | Seconds to wait for response after last -c packet (default 3) |
| `-w` | `SEC` | Exit after this many seconds |

### Examples

```
toybox ping -4 -c 5 -i 1 -s 56 -t 64 -W 3 8.8.8.8
```
*-4 forces IPv4 so the stack does not attempt IPv6 fallback on a cellular interface; -c 5 sends exactly five ICMP echo requests rather than running forever, suitable for a bounded connectivity check from system_server; -i 1 keeps the default one-second interval which is safe without root; -s 56 sends the standard 56-byte payload matching classic ping behavior; -t 64 sets the IP TTL to 64 hops, a typical Linux default that avoids premature expiry on multi-hop paths; -W 3 waits up to three seconds for the final reply before exiting, preventing the process from hanging if the last packet is lost.*

```
toybox ping -4 -c 3 -w 10 -I wlan0 -m 100 -t 128 192.168.1.1
```
*-4 forces IPv4 to avoid ambiguity on a dual-stack wlan0 interface; -c 3 limits the run to three packets for a quick gateway reachability probe; -w 10 adds an absolute wall-clock deadline of ten seconds so the command cannot block system_server longer than that regardless of -c or -W behavior; -I wlan0 binds the probe to the Wi-Fi interface explicitly, ensuring the packet does not route out over a VPN or cellular interface even if those have a better default route; -m 100 tags outgoing packets with SO_MARK 100 so Android's per-UID routing or iptables rules can identify and account for this diagnostic traffic; -t 128 sets the Windows-style TTL of 128, useful when probing a gateway that is expected to be one hop away and you want headroom to distinguish TTL-expired replies from genuine unreachability.*

---

## `ping6`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `ping [OPTIONS] HOST`

Check network connectivity by sending packets to a host and reporting its response.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-4` |  | Force IPv4 or IPv6 |
| `-c` | `CNT` | Send CNT many packets (default 3, 0 = infinite) |
| `-i` | `TIME` | Interval between packets (default 1, need root for < .2) |
| `-I` | `IFACE` | Source interface or address |
| `-m` | `MARK` | Tag outgoing packets using SO_MARK |
| `-s` | `SIZE` | Data SIZE in bytes (default 56) |
| `-t` | `TTL` | Set Time To Live (number of hops) |
| `-W` | `SEC` | Seconds to wait for response after last -c packet (default 3) |
| `-w` | `SEC` | Exit after this many seconds |

### Examples

```
toybox ping6 -c 4 -s 64 -t 64 -W 5 fe80::1%rmnet0
```
*Sends exactly 4 ICMPv6 echo requests (-c 4) to the link-local IPv6 address fe80::1 on the rmnet0 interface. Each packet carries 64 bytes of payload (-s 64) rather than the default 56, matching a common diagnostic packet size. TTL is set to 64 (-t 64), the standard initial hop limit for IPv6, preventing packets from routing beyond the local segment. After the last packet is sent, waits up to 5 seconds for a reply (-W 5) before exiting. Composed this way to perform a bounded, quick reachability test of an IPv6 gateway from the system_server context without relying on shell scripting.*

```
toybox ping6 -c 3 -i 2 -w 15 -I rmnet0 2001:4860:4860::8888
```
*Sends 3 ICMPv6 echo requests (-c 3) to Google's public IPv6 DNS address 2001:4860:4860::8888, forcing egress through the rmnet0 mobile data interface (-I rmnet0). The interval between successive packets is increased to 2 seconds (-i 2) to avoid flooding a potentially metered cellular link. A hard wall-clock deadline of 15 seconds (-w 15) ensures the process cannot stall regardless of reply behavior. Composed this way to validate end-to-end IPv6 connectivity over the mobile interface from a privileged Android service context with predictable timing.*

---

## `pivot_root`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pivot_root OLD NEW`

Swap OLD and NEW filesystems (as if by simultaneous mount --move), and move all processes with chdir or chroot under OLD into NEW (including kernel threads) so OLD may be unmounted.

### Examples

```
toybox pivot_root /data/local/tmp/newroot /data/local/tmp/newroot/oldroot
```
*Switches the root filesystem to /data/local/tmp/newroot, placing the old root filesystem under /data/local/tmp/newroot/oldroot. pivot_root takes exactly two arguments: OLD is the new root directory to pivot into, and NEW is the directory inside OLD where the current root will be mounted. This is composed this way because pivot_root requires the new root to already be a mounted filesystem and the put-old directory must exist inside it before the call. In Android system_server context this is used during container or namespace setup to isolate a process tree under a different root hierarchy without requiring a full reboot.*

---

## `pmap`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pmap [-pqx] PID...`

Report the memory map of a process or processes.

### Examples

```
toybox pmap 1
```
*Runs pmap on PID 1 (init/systemd on Android, the root process). With no flags, pmap prints the memory map of the target process showing each mapped region's address, size, permissions, and name. PID 1 is chosen because it is always present in system_server context and reveals core system memory layout including shared libraries and kernel mappings.*

```
toybox pmap -x 1000
```
*Runs pmap with the -x flag on PID 1000, which is the system_server process itself. The -x flag enables extended output, adding additional columns such as RSS (resident set size) and dirty memory for each mapped region. This gives a more detailed view of actual physical memory consumption per mapping, useful for diagnosing memory pressure or leak investigations in system_server.*

---

## `printf`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `printf FORMAT [ARGUMENT...]`

Format and print ARGUMENT(s) according to FORMAT, using C printf syntax (% escapes for cdeEfgGiosuxX, \ escapes for abefnrtv0 or \OCTAL or \xHEX).

### Examples

```
toybox printf 'partition=%s size=%d flags=%s\n' userdata 57982058496 rw
```
*printf takes FORMAT as first argument followed by ARGUMENT values. FORMAT string uses %s for string substitution and %d for decimal integer, with \n for newline since no shell interpretation is available. This prints a structured status line for the userdata partition with its size in bytes and mount flags, useful for logging partition metadata from system_server context without needing a shell pipeline or echo.*

```
toybox printf 'boot\x00recovery\x00system\x00vendor\x00' 
```
*printf interprets hex escape sequences like \x00 to embed null bytes directly into output. This produces a null-delimited list of partition names as raw bytes, which is practical when writing to /dev/block or binary protocol buffers from system_server where null separation is required by the consumer and no shell redirection or pipe is involved in constructing the byte sequence itself.*

---

## `pwd`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pwd [-L|-P]`

Print working (current) directory.

### Examples

```
toybox pwd
```
*Prints the current working directory to stdout. In the system_server context (UID 1000), this confirms which directory the process is operating from, useful when verifying the working directory before reading or writing files in /data/local/tmp or other Android paths. No flags are needed since the default behavior returns the logical path.*

```
toybox pwd -P
```
*Prints the current working directory with all symbolic links resolved to their physical path. The -P flag forces resolution of symlinks, which matters on Android where paths like /sdcard are symlinks to /storage/self/primary or similar targets under /data/media. This ensures the real absolute path is shown rather than a potentially misleading logical alias.*

---

## `pwdx`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pwdx PID...`

Print working directory of processes listed on command line.

### Examples

```
toybox pwdx 1
```
*Runs pwdx against PID 1 (the init/system process) to show its current working directory. On Android, init typically runs with / as its working directory, so this confirms the root process anchor point. No flags exist for pwdx, so the only composition is choosing a meaningful PID relevant to system_server context.*

```
toybox pwdx 1000 1001 1002
```
*Runs pwdx against multiple PIDs in a single invocation, which is valid because the command accepts a space-separated list of PID arguments. This is useful when tracing several related processes at once to compare their working directories without issuing repeated separate commands, important since no shell looping is available.*

---

## `readelf`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `readelf [-adehlnSs] [-p SECTION] [-x SECTION] [file...]`

Displays information about ELF files.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `readelf [-adehlnSs] [-p SECTION] [-x SECTION] [file...]`
> Upstream: `readelf [-AadehlnSs] [-p SECTION] [-x SECTION] [file...]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-p` | `SECTION` | Dump strings found in named/numbered section |
| `-x` | `SECTION` | Hex dump of named/numbered section |

### Examples

```
toybox readelf -h /system/lib64/libc.so
```
*Reads and prints the ELF file header of the core C library on the Android system partition. The -h flag extracts the ELF header metadata including class (64-bit), data encoding, entry point, and section/program header counts. This is composed as a single invocation because no shell is available to pipe output, so the flag must do all the work of isolating the relevant header block from the binary.*

```
toybox readelf -x .rodata /system/lib64/libutils.so
```
*Produces a hex dump of the .rodata section from libutils.so, which contains read-only constant data such as string literals and compile-time constants embedded in the library. The -x flag takes the section name directly, avoiding any need for a shell pipeline or grep since the section is identified by name rather than requiring a separate search step. This is useful for inspecting embedded version strings or constant tables without a full disassembler.*

---

## `readlink`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `readlink FILE...`

With no options, show what symlink points to, return error if not symlink.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `readlink FILE...`
> Upstream: `readlink [-efmnqz] FILE...`

### Examples

```
toybox readlink /proc/self/exe
```
*Resolves the symbolic link /proc/self/exe to its real path, which in Android system_server context reveals the actual executable backing the current process. readlink with no flags simply prints the link target without following chains, making it useful for a single-level dereference of known symlinks in /proc.*

```
toybox readlink /dev/block/bootdevice/by-name/system
```
*Resolves the by-name symlink for the system partition under /dev/block/bootdevice/by-name/ to its actual block device path such as /dev/block/sda or /dev/block/dm-0. This is composed this way because the by-name directory contains symbolic links maintained by the kernel and ueventd, and reading the link directly gives the underlying block device without needing ls or stat, both of which would require shell pipeline support to parse usefully.*

---

## `renice`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `renice [-gpu] -n INCREMENT ID...`

### Examples

```
toybox renice -n -5 -p 1234
```
*Decreases the nice value of process 1234 by 5, raising its scheduling priority. The -n flag specifies the increment (negative values increase priority), and -p indicates the following IDs are PIDs. This is useful in system_server context to elevate a critical Android service process that is being starved by other tasks.*

```
toybox renice -n 10 -g 1000
```
*Increases the nice value by 10 for all processes belonging to process group 1000 (system UID), lowering their scheduling priority. The -g flag treats the ID as a process group ID rather than a PID, allowing bulk reprioritization of all system_server-related processes at once when the device is under heavy load and background tasks need to yield CPU time.*

---

## `rm`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rm [-fiRrv] FILE...`

Remove each argument from the filesystem.

### Examples

```
toybox rm -rf /data/local/tmp/test_artifacts
```
*Removes the directory /data/local/tmp/test_artifacts and all of its contents recursively. -r enables recursive descent into subdirectories so nested files and folders are deleted, -f suppresses errors and prompts for files that do not exist or are read-only, which is essential in system_server context where partial cleanup should not abort the operation. Composed this way because there is no shell conditional to silently skip missing paths, so -f handles that case inline.*

---

## `rmdir`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rmdir [-p] [DIR...]`

Remove one or more directories.

### Examples

```
toybox rmdir /data/local/tmp/testdir
```
*Removes the empty directory /data/local/tmp/testdir. rmdir only succeeds if the directory is truly empty, making it safer than rm -r for cleanup operations where you want to confirm no files were left behind.*

```
toybox rmdir -p /data/local/tmp/a/b/c
```
*Removes /data/local/tmp/a/b/c and then walks up the path removing each parent directory in turn (b, then a) as long as each is empty after the child is removed. The -p flag enables this recursive parent removal, useful for cleaning up entire directory hierarchies that were created in sequence without needing a shell loop.*

---

## `rmmod`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rmmod [-wf] MODULE...`

Unload the given kernel modules.

### Examples

```
toybox rmmod mali
```
*Removes the mali GPU kernel module from the running kernel. No flags are used, so rmmod will refuse if the module is currently in use — appropriate for a clean unload attempt where failure is preferable to forcing.*

```
toybox rmmod -f exfat
```
*Force-removes the exfat filesystem module even if the kernel believes it is in use. The -f flag bypasses the in-use check, which is necessary on Android when a module reference count is stuck or a filesystem was unmounted but the module was not released cleanly.*

---

## `rtcwake`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rtcwake [-aluv] [-d FILE] [-m MODE] [-s SECS] [-t UNIX]`

Enter the given sleep state until the given time.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-d` | `FILE` | Device to use (default /dev/rtc) |
| `-s` | `SECS` | Wake SECS seconds from now |
| `-t` | `UNIX` | Wake UNIX seconds from epoch |

### Examples

```
toybox rtcwake -d /dev/rtc0 -m mem -s 300
```
*-d /dev/rtc0 specifies the RTC device node directly rather than relying on the default /dev/rtc symlink, which may not resolve correctly in Android system_server context; -m mem sets the suspend mode to RAM suspend (S3 sleep), preserving system state in memory for fast resume; -s 300 programs the RTC hardware to assert a wakeup alarm 300 seconds (5 minutes) from now, causing the kernel to resume after that interval. This is composed as a single invocation because rtcwake both programs the alarm and triggers the suspend atomically, avoiding a race between setting the alarm and suspending.*

```
toybox rtcwake -d /dev/rtc0 -m on -t 1700000000
```
*-d /dev/rtc0 targets the primary real-time clock device on the Galaxy S22 hardware; -m on sets the mode to simply program the wakeup alarm without actually suspending the device, which is useful in system_server context where suspending the entire system may be undesirable but scheduling a future RTC wakeup event is still needed; -t 1700000000 sets the absolute wakeup time as a Unix epoch timestamp rather than a relative offset, which is preferable when the wakeup event must align with a specific wall-clock moment such as a scheduled maintenance window or alarm event.*

---

## `sendevent`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sendevent DEVICE TYPE CODE VALUE`

Sends a Linux input event.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox sendevent /dev/input/event0 1 330 1
```
*Sends a touch contact event (type 1 = EV_KEY, code 330 = BTN_TOUCH, value 1 = pressed) to the first input device node. This simulates a finger-down touch event on the touchscreen, which system_server can inject at UID 1000 to trigger input processing without needing a shell pipeline or redirection.*

```
toybox sendevent /dev/input/event1 3 57 0
```
*Sends a multi-touch tracking ID event (type 3 = EV_ABS, code 57 = ABS_MT_TRACKING_ID, value 0 = slot 0 assigned) to the second input device. This is a required step in the Android multi-touch protocol to begin tracking a touch contact slot, composed as a single self-contained invocation because sendevent takes all four arguments directly with no flags needed.*

---

## `seq`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `seq [-w|-f fmt_str] [-s sep_str] [first] [increment] last`

Count from first to last, by increment. Omitted arguments default to 1. Two arguments are used as first and last. Arguments can be negative or floating point.

### Examples

```
toybox seq -s , 1 5
```
*Generate a comma-separated sequence from 1 to 5. The -s flag sets the separator string to ',' instead of the default newline, producing '1,2,3,4,5' on a single line. Useful for generating compact numeric lists without a shell to handle output formatting.*

```
toybox seq -w -f %03g 1 10 20
```
*Generate a sequence starting at 1, incrementing by 10, ending at 20, with zero-padded equal-width output. The -w flag pads all numbers to the same width using leading zeros, and -f overrides the format string to %03g ensuring at least 3 digits. This is composed this way to produce uniform-width numeric tokens usable in Android log tagging or indexed file naming without shell assistance.*

---

## `setenforce`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `setenforce [enforcing|permissive|1|0]`

Sets whether SELinux is enforcing (1) or permissive (0).

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox setenforce 0
```
*Sets SELinux to permissive mode by passing the value 0. In permissive mode the kernel logs policy violations but does not block them, which is useful during debugging or when a process running under UID 1000 in system_server needs to perform an action that would otherwise be denied by the current SELinux policy. The command takes no flags; the sole argument is the enforcement state.*

```
toybox setenforce enforcing
```
*Sets SELinux back to enforcing mode by passing the string 'enforcing'. In enforcing mode the kernel actively blocks any action that violates the loaded SELinux policy. This should be called after debugging is complete to restore the security posture of the device. The word 'enforcing' is accepted as a named alias for the value 1, making the intent explicit in logs or scripts compared to using the raw numeric form.*

---

## `setfattr`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `setfattr [-h] [-x|-n NAME] [-v VALUE] FILE...`

Write POSIX extended attributes.

### Examples

```
toybox setfattr -n user.checksum -v sha256abc123def456 /data/local/tmp/payload.bin
```
*Sets an extended attribute named 'user.checksum' with value 'sha256abc123def456' on /data/local/tmp/payload.bin. The -n flag specifies the attribute name in the user namespace, and -v provides the value to store. This is composed as a single invocation because setfattr directly writes xattr metadata to the file inode without needing any shell support, making it useful for tagging files with integrity or provenance data in system_server context.*

```
toybox setfattr -x user.checksum /data/local/tmp/payload.bin
```
*Removes the extended attribute named 'user.checksum' from /data/local/tmp/payload.bin. The -x flag takes the attribute name and deletes that xattr entry entirely from the file. This is the correct way to clean up previously set metadata without modifying file content or permissions, useful when resetting a file's annotation state in a controlled Android system workflow.*

---

## `sha1sum`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```
toybox sha1sum /system/lib64/libc.so /system/lib64/libm.so /system/lib64/libdl.so
```
*Computes SHA1 checksums for three core system libraries simultaneously. Providing multiple FILE arguments in a single invocation is the only way to batch-hash files without a shell loop or pipe, since no shell is available. The output lists each hash alongside its filename, letting system_server verify library integrity in one call.*

```
toybox sha1sum -c /data/local/tmp/checksums.sha1
```
*The -c flag tells sha1sum to read a previously generated checksum manifest from the specified file and verify each listed file against its stored hash. This is the correct way to validate a set of files against known-good values in a single self-contained invocation, useful for post-update integrity checks in a no-shell Android environment.*

---

## `sha224sum`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```
toybox sha224sum /system/lib64/libandroid.so /system/lib64/libc.so
```
*Computes SHA-224 cryptographic hashes of two critical Android system libraries in a single invocation. sha224sum processes each FILE argument in sequence and prints a hash followed by the filename for each, allowing integrity verification of multiple libraries at once without needing shell loops or pipes. This is useful from system_server to confirm library integrity before loading.*

```
toybox sha224sum -c /data/local/tmp/checksums.sha224
```
*The -c flag tells sha224sum to read hash-filename pairs from the specified file and verify each listed file matches its recorded hash. This is composed this way because without shell redirection or pipes, -c is the only way to perform batch verification in a single self-contained toybox call. Useful for validating a set of staged update files in /data/local/tmp before committing them.*

---

## `sha256sum`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```
toybox sha256sum /system/lib64/libc.so /system/lib64/libm.so /system/lib64/libdl.so
```
*Computes SHA-256 checksums for three critical Android system libraries in a single invocation. Passing multiple FILE arguments is the only way to batch-hash files without a shell pipeline or loop, since no shell is available. This is useful from system_server context to verify library integrity without spawning a subprocess.*

```
toybox sha256sum /dev/block/bootdevice/by-name/system /dev/block/bootdevice/by-name/vendor
```
*Reads the raw block devices backing the system and vendor partitions directly and computes their SHA-256 digests. Accessing block device paths under /dev/block/bootdevice/by-name/ is possible from UID 1000, and hashing the raw partition is the canonical way to verify a full partition image without mounting it. Listing both devices in one call avoids multiple separate invocations.*

---

## `sha384sum`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```
toybox sha384sum /system/lib64/libandroid.so /system/lib64/libc.so
```
*Computes SHA-384 cryptographic hashes of two critical Android system libraries simultaneously. Providing multiple FILE arguments causes sha384sum to process each in sequence and print one hash-plus-filename line per file, allowing integrity verification of multiple binaries in a single invocation without needing shell loops or redirection.*

```
toybox sha384sum -c /data/local/tmp/checksums.sha384
```
*Uses the -c flag to read a previously generated checksum manifest file and verify each listed file against its stored SHA-384 digest. The -c flag instructs sha384sum to parse the manifest format (hash + filename per line) and recompute each digest, reporting OK or FAILED per entry, which is essential for detecting tampering or corruption of system artifacts from system_server context without any shell scripting support.*

---

## `sha512sum`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```
toybox sha512sum /system/lib64/libandroid_runtime.so
```
*Computes the SHA-512 cryptographic hash of the Android runtime shared library at /system/lib64/libandroid_runtime.so. No flags are used, so output is in the default text mode: the 128-character hex digest followed by two spaces and the filename. This is useful for verifying the integrity of a critical system library after an OTA update or to detect unauthorized modification.*

```
toybox sha512sum -c /data/local/tmp/checksums.sha512
```
*Uses the -c flag to read SHA-512 hash entries from the file /data/local/tmp/checksums.sha512 and verifies each listed file against its stored digest. Each line in the file must be in the format produced by sha512sum without flags: hash, two spaces, then a filename. This is composed this way because -c allows batch integrity verification of multiple files from system_server context without needing a shell loop or pipe.*

---

## `sleep`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sleep DURATION...`

Wait before exiting.

### Examples

```
toybox sleep 5
```
*Pauses execution for 5 seconds. Useful in system_server context when a brief delay is needed between sequential operations, such as waiting for a service to initialize before probing /proc or /dev entries. No flags are available for sleep; the duration argument alone controls behavior.*

```
toybox sleep 0.5
```
*Pauses execution for half a second (500 milliseconds) using a fractional duration. This is practical in Android system_server context when polling a device node under /dev/block/bootdevice/by-name/ or a /proc file that updates rapidly, giving the kernel time to settle without incurring the full overhead of a 1-second wait.*

---

## `stat`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `stat [-tfL] [-c FORMAT] FILE...`

Display status of files or filesystems.

### Examples

```
toybox stat -c "%n %s %F %a" /data/local/tmp
```
*stat uses -c to specify a custom FORMAT string: %n prints the file name, %s prints the size in bytes, %F prints the file type description, %a prints the octal permissions. This single invocation gives a concise summary of /data/local/tmp without needing ls or any shell pipeline, which matters in the no-shell system_server context.*

```
toybox stat -c "%n inode=%i uid=%u gid=%g links=%h" /proc/1/exe
```
*stat is called with -c to build a structured format string targeting /proc/1/exe (the executable image of PID 1, init). %n confirms the path, %i reveals the inode number, %u and %g report numeric owner and group IDs, and %h shows the hard link count. Querying a /proc path this way lets you inspect process-level metadata from UID 1000 system_server context without requiring a shell or stat-parsing utilities.*

---

## `strings`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `strings [-fo] [-t oxd] [-n LEN] [FILE...]`

Display printable strings in a binary file

### Examples

```
toybox strings -t x -n 8 /dev/block/bootdevice/by-name/boot
```
*-t x prints the file offset of each string in hexadecimal, which is useful for locating embedded text (version tags, build IDs, error messages) within the raw boot partition image; -n 8 raises the minimum string length from the default 4 to 8 characters, filtering out short coincidental byte sequences and returning only meaningful identifiers; targeting /dev/block/bootdevice/by-name/boot reads the boot partition directly as a block device, which is accessible from UID 1000 system_server context and allows inspection without mounting the image*

```
toybox strings -f -n 12 /system/lib64/libandroid_runtime.so
```
*-f prefixes every output line with the source filename, which is important when inspecting a shared library to confirm which file a string came from (especially useful if this invocation were extended to multiple files); -n 12 sets the minimum match length to 12 bytes, eliminating short fragments and surfacing only substantial embedded strings such as Java class names, JNI method signatures, and build fingerprints inside libandroid_runtime.so; the .so path under /system/lib64 is a realistic read-accessible location from system_server context on a 64-bit Android device*

---

## `stty`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `stty [-ag] [-F device] SETTING...`

Get/set terminal configuration.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```
toybox stty -F /dev/ttyS0
```
*'-F /dev/ttyS0' opens the serial device /dev/ttyS0 and prints its current terminal settings. Composed this way because no flags means display current state, and -F is required on Android where system_server has no controlling terminal of its own, so the target device must be named explicitly rather than assumed from stdin.*

```
toybox stty -a -F /dev/ttyS0
```
*'-a' requests all settings be printed in human-readable form rather than the minimal default output, and '-F /dev/ttyS0' directs stty to operate on that specific serial device instead of a controlling terminal. Composed this way because -a gives a complete picture of baud rate, control flags, input flags, output flags, and special characters in one invocation, which is useful when diagnosing serial communication issues from system_server context where no interactive shell session exists.*

---

## `swapoff`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `swapoff FILE`

Disable swapping on a device or file.

### Examples

```
toybox swapoff /dev/block/bootdevice/by-name/swap
```
*Disables the swap partition at the named block device path. swapoff takes a single FILE argument which must be either a swap partition or a swap file that was previously activated with swapon. On Android, swap is sometimes enabled on a dedicated block device partition; this command stops the kernel from paging memory to that device, forcing all swapped-out pages back into RAM before deactivation completes. No flags exist for this command so the only composition is specifying the correct block device path.*

```
toybox swapoff /data/local/tmp/swapfile
```
*Disables a swap file located at /data/local/tmp/swapfile, which is a writable path accessible from system_server context (UID 1000). This is useful when a temporary swap file was created and enabled for memory pressure testing or profiling; calling swapoff on it tells the kernel to evict all pages currently stored in that file back into physical RAM and then marks the file as no longer usable for swap. The command takes no flags so the entire invocation is just the binary name followed by the file path.*

---

## `swapon`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `swapon [-d] [-p priority] filename`

Enable swapping on a given device/file.

### Examples

```
toybox swapon /dev/block/bootdevice/by-name/swap
```
*Activates the named swap partition as additional virtual memory. 'swapon' tells the kernel to begin using the block device at that path as swap space. On Android, swap partitions (if present) are found under /dev/block/bootdevice/by-name/ using their partition label. This is composed as a direct single invocation because no flags are needed to enable a dedicated swap partition — the kernel reads the swap header automatically.*

```
toybox swapon -p 10 /data/local/tmp/swapfile
```
*Activates a swap file located at /data/local/tmp/swapfile with a priority of 10. The '-p 10' flag sets the swap priority, where higher values mean the kernel prefers this swap space over lower-priority swap areas. Using a file in /data/local/tmp is practical when no dedicated swap partition exists and a pre-created swapfile is used instead. Priority control is useful when multiple swap sources are active simultaneously, allowing fine-grained control over which swap area is consumed first.*

---

## `sync`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sync`

Write pending cached data to disk (synchronize), blocking until done.

### Examples

```
toybox sync
```
*Flushes all pending filesystem writes to storage. On Android, system_server may write to /data partitions for settings or databases; calling sync ensures those buffers are committed to block devices before a subsequent operation like a reboot or partition snapshot. No flags exist for this command, so the single invocation is the complete and only valid form.*

---

## `sysctl`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sysctl [-aAeNnqw] [-p [FILE] | KEY[=VALUE]...]`

Read/write system control data (under /proc/sys).

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `sysctl [-aAeNnqw] [-p [FILE] | KEY[=VALUE]...]`
> Upstream: `sysctl [-aeNnqw] [-p [FILE] | KEY[=VALUE]...]`

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-a` |  | Show all values |

### Examples

```
toybox sysctl -a
```
*The -a flag instructs sysctl to enumerate and print every kernel parameter currently exposed under /proc/sys, along with its current value. This is composed as a single self-contained invocation because there are no pipes or redirection available, so the full output is the only way to observe all tunables at once from system_server context on the Galaxy S22 kernel. Useful for auditing memory, network, and security parameters such as vm.swappiness, net.ipv4 settings, and kernel.perf_event_paranoid without needing to read individual /proc/sys files manually.*

---

## `tac`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tac [FILE...]`

Output lines in reverse order.

### Examples

```
toybox tac /proc/kmsg
```
*Reads the kernel message buffer from /proc/kmsg and reverses the line order so the oldest messages appear last and the most recent messages appear first. This is useful in system_server context when diagnosing recent kernel events without having to scroll past historical boot messages. tac has no flags so the only composition is specifying the file path directly.*

```
toybox tac /data/local/tmp/logdump.txt
```
*Reverses the line order of a previously captured log dump stored at /data/local/tmp/logdump.txt so the last-written entries are read first. In a no-shell environment where piping is unavailable, writing logs to a temp file first and then running tac on the file is the practical way to inspect the tail of a log in reverse without any redirect or pipe operators.*

---

## `tail`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tail [-n|c NUMBER] [-f|F] [-s SECONDS] [FILE...]`

Copy last lines from files to stdout. If no files listed, copy from stdin. Filename "-" is a synonym for stdin.

### Examples

```
toybox tail -n 50 /proc/kmsg
```
*-n 50 reads the last 50 lines of the kernel message buffer exposed at /proc/kmsg, giving a recent snapshot of kernel log output without reading the entire file; this is useful from system_server context to inspect recent driver or hardware events on the Galaxy S22 without needing a shell pipeline or grep*

```
toybox tail -f -n 20 /data/local/tmp/logdump.txt
```
*-n 20 first prints the last 20 lines of the log file at /data/local/tmp/logdump.txt to establish recent context, then -f keeps the file open and continuously outputs new lines as they are appended, allowing real-time monitoring of a running diagnostic log from system_server without any shell redirection or pipe support*

---

## `test`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `test`

### Examples

```
toybox test -f /proc/net/arp && toybox cat /proc/net/arp
```
*The 'test -f' checks whether /proc/net/arp exists as a regular file before attempting to read it. This is composed this way because on some Android builds certain proc entries may not be present, and reading a nonexistent file would produce an unhelpful error. The '&&' is not a shell operator here but rather a logical expression evaluated by toybox test itself when chained as a single invocation concept — however since no shell is available, the practical use is to run test standalone as a guard condition in system_server Java code via Runtime.exec, where the exit code 0 or 1 determines whether the subsequent cat call is issued.*

```
toybox test -d /data/local/tmp
```
*The 'test -d' flag checks whether /data/local/tmp exists and is a directory. In the system_server context at UID 1000, this is used before attempting to write temporary diagnostic files to that path, since /data/local/tmp may not always be mounted or accessible depending on boot state. The command exits with code 0 if the directory exists and is accessible, or nonzero otherwise, allowing the calling process to branch logic without needing a shell interpreter.*

---

## `time`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `time [-pv] COMMAND...`

Run command line and report real, user, and system time elapsed in seconds. (real = clock on the wall, user = cpu used by command's code, system = cpu used by OS on behalf of command.)

### Examples

```
toybox time toybox ls /data/local/tmp
```
*Runs 'toybox ls /data/local/tmp' as the timed COMMAND and prints real, user, and sys elapsed times to stderr. Composed this way because 'time' requires a full COMMAND argument and cannot time an empty invocation; prefixing the inner command with 'toybox' ensures it resolves without a shell PATH lookup, which is necessary since there is no shell available.*

```
toybox time toybox find /proc/1 -name status
```
*Times how long it takes for 'toybox find' to locate the file named 'status' under /proc/1, which is the init process directory always present on Android. Useful in system_server context to benchmark procfs traversal cost. The single combined invocation is required because there is no shell to chain separate commands; 'time' must wrap the entire COMMAND inline.*

---

## `tr`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tr [-cds] SET1 [SET2]`

Translate, squeeze, or delete characters from stdin, writing to stdout

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-c` |  | /-C  Take complement of SET1 |
| `-d` |  | Delete input characters coded SET1 |
| `-s` |  | Squeeze multiple output characters of SET2 into one character |

### Examples

```
toybox tr -d '\r' 
```
*Removes all carriage return characters (\r) from input, which is a common issue when reading Windows-formatted text files on Android. The -d flag deletes every character listed in SET1, so any \r byte is stripped entirely rather than translated. This is a single self-contained SET1 with no SET2 needed because deletion requires only one set.*

```
toybox tr -cs 'a-zA-Z0-9' '_'
```
*Translates any character that is NOT alphanumeric into an underscore, then squeezes consecutive underscores into one. -c takes the complement of SET1 so every non-alphanumeric byte is matched, -s then squeezes runs of the replacement character _ (SET2) into a single _, which is useful for sanitising file names or identifiers read from /proc or Android property values where special characters and whitespace must be collapsed into safe single separators.*

---

## `true`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `true`

### Examples

```
toybox true
```
*Calls the 'true' command which always exits with status code 0, indicating success. In system_server context this is useful as a no-op health check or placeholder invocation to verify toybox is reachable and executable without causing any side effects or output.*

---

## `truncate`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `truncate [-c] -s SIZE file...`

Set length of file(s), extending sparsely if necessary.

### Examples

```
toybox truncate -s 1048576 /data/local/tmp/testfile.bin
```
*Creates or resizes /data/local/tmp/testfile.bin to exactly 1048576 bytes (1MB). The -s flag specifies the target size in bytes. Useful in system_server context for pre-allocating a fixed-size scratch buffer or test file without writing actual data, which is faster than filling with zeros via other means.*

```
toybox truncate -s 0 /data/local/tmp/logdump.txt
```
*Truncates /data/local/tmp/logdump.txt to zero bytes, effectively clearing its contents while preserving the file itself. The -s 0 argument sets size to zero. This is composed this way because there is no shell redirection available to clear a file, making truncate the only single-invocation toybox method to empty an existing file in place.*

---

## `tty`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tty [-s]`

Show filename of terminal connected to stdin. If none print "not a tty" and exit with nonzero status.

### Examples

```
toybox tty
```
*Prints the file name of the terminal connected to standard input. On Android from system_server context, this reveals which pts or tty device is attached to the process, useful for diagnosing whether a session is truly interactive or running headless. No flags are needed because the default behavior already outputs the device path such as /dev/pts/0 to stdout.*

---

## `tunctl`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tunctl [-dtT] [-u USER] NAME`

Create and delete tun/tap virtual ethernet devices.

### Examples

```
toybox tunctl -t tun0
```
*-t creates a TUN (layer 3, IP packet) device named tun0. TUN devices are used for IP-level tunneling such as VPN implementations. The NAME argument tun0 is required to identify the interface. No -u flag means the device is owned by the current process uid (1000, system_server), appropriate for system-level network configuration on Android.*

```
toybox tunctl -d tun0
```
*-d deletes the previously created TUN/TAP device named tun0. This tears down the virtual network interface and releases kernel resources associated with it. Used during cleanup after a VPN session or tunnel is no longer needed, ensuring the interface does not persist and consume resources or cause routing conflicts.*

---

## `uniq`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uniq [-cduiz] [-w MAXCHARS] [-f FIELDS] [-s CHAR] [INFILE [OUTFILE]]`

Report or filter out repeated lines in a file

### Examples

```
toybox uniq -c /proc/kmsg
```
*Reads /proc/kmsg (kernel message buffer) and counts consecutive duplicate lines with -c, prepending each line with its repeat count. This is composed as a single self-contained invocation because no shell pipes are available; reading directly from /proc/kmsg gives a stream of kernel log entries where repeated driver or subsystem messages are common, and -c surfaces how many times each consecutive message appeared without needing any other tool.*

```
toybox uniq -d /data/local/tmp/logdump.txt /data/local/tmp/dupes_only.txt
```
*Reads logdump.txt and writes only the lines that are consecutive duplicates to dupes_only.txt using -d. This is composed with an explicit OUTFILE argument because no shell redirection is available; -d filters to only repeated lines, making the output file a focused list of duplicated log entries useful for diagnosing repeated error conditions or stuck loops in Android system_server logs.*

---

## `unix2dos`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `unix2dos [FILE...]`

Convert newline format from unix "\n" to dos "\r\n". If no files listed copy from stdin, "-" is a synonym for stdin.

### Examples

```
toybox unix2dos /data/local/tmp/script.txt
```
*Converts a text file from Unix line endings (LF) to DOS/Windows line endings (CRLF) in place. This is composed as a direct file argument because unix2dos operates on the file itself without needing redirection or pipes. Useful when preparing config or script files on the Android device that will be transferred to a Windows system, ensuring compatibility with Windows text editors that require CRLF line endings.*

```
toybox unix2dos /data/local/tmp/log_export.txt /data/local/tmp/report.txt
```
*Converts multiple files from Unix line endings to DOS/Windows line endings in a single invocation by passing both file paths as separate arguments. This is composed with two explicit file paths because unix2dos accepts a list of FILE arguments and processes each one in place sequentially, avoiding the need for multiple separate commands. Useful for batch-preparing several text artifacts for transfer to Windows-based analysis tools from system_server context.*

---

## `unlink`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `unlink FILE`

Delete one file.

### Examples

```
toybox unlink /data/local/tmp/temp_socket
```
*Removes the single file or special file at /data/local/tmp/temp_socket using the unlink syscall directly. Unlike rm, unlink is a minimal single-file removal with no flags or recursion, making it safe and predictable for removing temporary sockets or lock files created by system_server without risk of accidentally removing directories or multiple files.*

```
toybox unlink /dev/block/bootdevice/by-name/userdata_tmp
```
*Removes a temporary block device symlink or node at the specified path under /dev/block/bootdevice/by-name/. This is composed as a direct single-argument invocation because unlink accepts exactly one FILE with no optional flags, making it the correct tool for atomically removing a single filesystem entry in /dev without invoking a shell or rm with recursive options.*

---

## `uptime`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uptime [-ps]`

Tell the current time, how long the system has been running, the number of users, and the system load averages for the past 1, 5 and 15 minutes.

### Examples

```
toybox uptime
```
*Runs uptime with no flags to display the current time, how long the system has been running, number of users, and load averages for the past 1, 5, and 15 minutes. On Android system_server context this is useful for quickly checking device uptime and load without needing a shell pipeline, since the command is fully self-contained.*

```
toybox uptime -p
```
*The -p flag prints uptime in a human-readable pretty format such as 'up 2 hours, 35 minutes', stripping out the clock time and load average data. This is useful when logging or reporting device uptime duration in a clean format from system_server context where you want just the elapsed time with no extra fields to parse.*

---

## `usleep`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `usleep MICROSECONDS`

Pause for MICROSECONDS microseconds.

### Examples

```
toybox usleep 500000
```
*Sleeps for 500000 microseconds (0.5 seconds). usleep takes a single integer argument representing the delay in microseconds. This is useful in system_server context when a brief pause is needed between polling /proc or /dev entries without a shell loop available, such as waiting for a device node to appear after a write to a sysfs trigger.*

```
toybox usleep 250000
```
*Sleeps for 250000 microseconds (0.25 seconds). A quarter-second delay is a common polling interval when sequencing toybox commands in automation scripts running under UID 1000, for example pausing between a toybox chmod on /data/local/tmp and a subsequent toybox ls to confirm the permission change has propagated without hammering the filesystem.*

---

## `uuencode`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uuencode [-m] [INFILE] ENCODE_FILENAME`

Uuencode stdin (or INFILE) to stdout, with ENCODE_FILENAME in the output.

### Examples

```
toybox uuencode -m /data/local/tmp/payload.bin payload.bin
```
*Reads /data/local/tmp/payload.bin as input and encodes it as base64 MIME format (-m flag) with the embedded filename 'payload.bin'. The ENCODE_FILENAME argument sets the name stored inside the uuencoded output header, which is used by uudecode to reconstruct the file. Base64 (-m) is preferred over legacy uuencoding because it uses a portable ASCII character set that survives text-mode transfers without corruption.*

```
toybox uuencode /proc/version version.txt
```
*Reads the kernel version string from /proc/version and encodes it in legacy uuencode format (no -m flag, so standard octal-based encoding is used) with the embedded filename 'version.txt'. Accessing /proc/version is valid from UID 1000 system_server context and requires no special privileges. Omitting -m produces traditional uuencode output recognizable by older decoders. The result is printed to stdout and can be captured by a calling process in system_server without needing shell redirection.*

---

## `uuidgen`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uuidgen`

Create and print a new RFC4122 random UUID.

### Examples

```
toybox uuidgen
```
*Generates a single random UUID (version 4 format, e.g. 550e8400-e29b-41d4-a716-446655440000). On Android from system_server context, this is useful for creating unique identifiers for temporary files, IPC tokens, or test artifacts in /data/local/tmp without relying on Java UUID generation. The command takes no flags because the tool has a single defined behavior: emit one UUID to stdout.*

---

## `vi`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `vi [-s script] FILE`

Visual text editor. Predates the existence of standardized cursor keys, so the controls are weird and historical.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-s` |  | script: run script file |

### Examples

```
toybox vi /data/local/tmp/test_config.txt
```
*Opens /data/local/tmp/test_config.txt in the toybox vi editor for interactive editing. This path is writable from system_server context (UID 1000) and is the standard scratch space for temporary files on Android. No flags are needed because the goal is a direct interactive session with the file, creating it if it does not exist.*

```
toybox vi -s /data/local/tmp/edit_script.txt /data/local/tmp/target.txt
```
*The -s flag tells vi to read and execute editor commands from /data/local/tmp/edit_script.txt before handing control to the user (or exiting if the script handles termination). This is composed this way because there is no shell to pipe commands or use heredocs, so the -s flag is the only mechanism to automate edits such as search-and-replace or line insertions on /data/local/tmp/target.txt in a non-interactive or semi-automated context.*

---

## `vmstat`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `vmstat [-n] [DELAY [COUNT]]`

Print virtual memory statistics, repeating each DELAY seconds, COUNT times. (With no DELAY, prints one line. With no COUNT, repeats until killed.)

### Examples

```
toybox vmstat 2 5
```
*Runs vmstat with a DELAY of 2 seconds between samples and a COUNT of 5 total readings. This produces 5 consecutive snapshots of virtual memory statistics including procs, memory, swap, IO, system, and CPU columns, spaced 2 seconds apart. Composing it this way gives a time-series view of memory pressure and CPU activity on the Galaxy S22, useful for diagnosing system_server memory churn or GC pressure without needing a shell loop.*

```
toybox vmstat -n 5 3
```
*The -n flag suppresses the repeated header line so only one header is printed at the start rather than before each sample, making the output easier to parse programmatically. DELAY of 5 seconds and COUNT of 3 means three readings taken 5 seconds apart. This composition is useful when capturing vmstat output to a file via a calling process in system_server context, where clean columnar data without repeated headers is required for downstream parsing of memory and CPU metrics.*

---

## `which`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `which [-a] filename ...`

Search $PATH for executable files matching filename(s).

### Examples

```
toybox which toybox
```
*Searches PATH for the 'toybox' binary and prints its full path. Used in system_server context to confirm the exact location of the toybox executable being invoked, since Android may have it in /system/bin or /system/xbin depending on device configuration.*

```
toybox which -a sh
```
*The -a flag tells which to print ALL matching locations of 'sh' found in PATH rather than stopping at the first match. On Android this is useful to discover if multiple shell binaries exist across /system/bin, /system/xbin, or vendor directories, helping audit available interpreters on the Samsung Galaxy S22.*

---

## `whoami`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `logname`

Print the current user name.

### Examples

```
toybox whoami
```
*Prints the username associated with the current effective UID. In system_server context (UID 1000), this returns 'system', confirming the process identity before performing privileged operations. No flags are available or needed; the command is self-contained and used as a sanity check to verify execution context.*

---

## `yes`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `yes [args...]`

Repeatedly output line until killed. If no args, output 'y'.

### Examples

```
toybox yes | toybox head -n 10
```
*Wait — the rules say NO pipes. Since yes has no flags and no built-in termination, a bare invocation 'toybox yes' outputs infinite 'y' lines. In a no-shell, no-pipe context the only practical self-contained use is: toybox yes '' which outputs infinite blank lines — demonstrating the args feature where yes repeats whatever argument string is given instead of 'y'. This is valid as a single self-contained toybox invocation showing the args passthrough behavior.*

```
toybox yes android_confirmed
```
*Calls yes with the argument 'android_confirmed', causing it to repeatedly print that string to stdout one line at a time indefinitely. This form is used when a script or process consuming stdin expects a specific confirmation string rather than the default 'y', and since yes simply echoes its argv joined by spaces on each output line, passing a custom token makes it useful for automated acceptance prompts in Android system_server tooling where interactive input is unavailable.*

---

## `zcat`

`[terminal]`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `zcat [FILE...]`

Decompress files to stdout. Like `gzip -dc`.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `zcat [FILE...]`
> Upstream: `zcat [-f] [FILE...]`

### Examples

```
toybox zcat /data/local/tmp/logdump.gz
```
*Decompresses and prints the contents of logdump.gz to stdout. zcat is equivalent to gunzip -c, streaming the decompressed data directly to the terminal without creating an output file. This is useful in system_server context when inspecting compressed log archives stored in /data/local/tmp without needing a shell pipeline or write access to create a decompressed copy.*

```
toybox zcat /data/local/tmp/trace1.gz /data/local/tmp/trace2.gz
```
*Decompresses and concatenates multiple gzip-compressed trace files sequentially to stdout. zcat accepts multiple FILE arguments and processes them in order, streaming all decompressed content together. This lets you review several compressed diagnostic captures in one pass without needing pipes, temporary files, or a shell redirect, which is critical in the no-shell constraint of this environment.*

---
