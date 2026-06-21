# Toybox Capability Atlas

A reference for every command available in Samsung's toybox build, classified by what it can do **without a shell, pipes, redirection, or wildcards**.

Generated from Samsungs crappy toybox on my device (Samsung Galaxy S22, Toybox 0.8.9-android) and cross-referenced against [https://landley.net/toybox/help.html](https://landley.net/toybox/help.html) by Rob @landley here on github, thank you for your website good sir.

## Capability Classes

| Class | Meaning |
|-------|---------|
|  `exec-capable` | Can spawn another command as part of its job — these are your shell replacement primitives |
|  `self-contained` | Has its own filter or search engine — no pipe into grep or awk needed |
|  `io-explicit` | Uses named file flags or args instead of shell redirection |
|  `terminal` | Produces output only — limited composition, but may feed exec-capable commands |

## Table of Contents

###  exec-capable (24)

[`brctl`](#brctl) · [`chroot`](#chroot) · [`chrt`](#chrt) · [`env`](#env) · [`find`](#find)
[`flock`](#flock) · [`inotifyd`](#inotifyd) · [`ionice`](#ionice) · [`nc`](#nc) · [`netcat`](#netcat)
[`nice`](#nice) · [`nohup`](#nohup) · [`nsenter`](#nsenter) · [`prlimit`](#prlimit) · [`rfkill`](#rfkill)
[`runcon`](#runcon) · [`setsid`](#setsid) · [`taskset`](#taskset) · [`timeout`](#timeout) · [`uclampset`](#uclampset)
[`unshare`](#unshare) · [`vconfig`](#vconfig) · [`watch`](#watch) · [`xargs`](#xargs)

###  self-contained (47)

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

###  io-explicit (12)

[`cksum`](#cksum) · [`comm`](#comm) · [`dd`](#dd) · [`fallocate`](#fallocate) · [`gzip`](#gzip)
[`install`](#install) · [`mv`](#mv) · [`rev`](#rev) · [`split`](#split) · [`tee`](#tee)
[`uudecode`](#uudecode) · [`wc`](#wc)

###  terminal (118)

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

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `brctl COMMAND [BRIDGE [INTERFACE]]`

Manage ethernet bridges

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox brctl --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `chroot`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `chroot NEWROOT [COMMAND [ARG...]]`

Run command within a new root directory. If no command, run /bin/sh. chroot: -h: No such file or directory

### Examples

```sh
toybox chroot /data/local/tmp toybox ls /
```
*Change root to /data/local/tmp and run ls. From ls's perspective `/` IS `/data/local/tmp` — useful for inspecting a staged filesystem or a pulled partition image.*

---

## `chrt`

` exec-capable` ` self-contained`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `chrt [-Rmofrbi] {-p PID [PRIORITY] | [PRIORITY COMMAND...]}`

Get/set a process' real-time scheduling policy and priority.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-o` | `SCHED_OTHER` | -f  SCHED_FIFO    -r  SCHED_RR |
| `-b` | `SCHED_BATCH` | -i  SCHED_IDLE |

### Examples

```sh
toybox chrt -f 99 toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Run dd at `SCHED_FIFO` realtime priority 99 — highest possible CPU scheduling. Gets your operation done before anything else touches the CPU.*

```sh
toybox chrt -i 0 toybox find /data -name '*.apk' -type f
```
*Run find at `SCHED_IDLE` — only runs when the CPU is completely free. Safe background scan that won't compete with foreground processes.*

```sh
toybox chrt -p <PID>
```
*Show the current scheduling policy and priority of a running process without modifying it.*

---

## `env`

` exec-capable`

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

```sh
toybox env LD_PRELOAD=/data/local/tmp/hook.so toybox grep pattern /data/local/tmp/target
```
*Inject a shared library into grep's process before it starts. `LD_PRELOAD` interception without a shell wrapper — env sets up the environment then execs the child.*

```sh
toybox env -i PATH=/system/bin toybox find /data -name '*.apk'
```
*`-i` clears the entire inherited environment first, then sets only what you specify. Gives the child process a clean known state with no leaked variables.*

---

## `find`

` exec-capable` ` self-contained`

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

```sh
toybox find /data/local/tmp -type f -name '*.bin' -exec toybox xxd {} ;
```
*For every .bin file under /data/local/tmp, run xxd on it individually. `-exec` with `;` means one xxd call per file — safe for filenames with spaces.*

```sh
toybox find /proc -maxdepth 3 -name status -exec toybox grep TracerPid {} +
```
*Scan /proc 3 levels deep for every `status` file, batch them all into a single grep call. `+` batching is faster than `;` when you have many matches.*

```sh
toybox find /dev -type c -newer /data/local/tmp/ref -exec toybox stat {} ;
```
*Find character devices modified more recently than your reference file — detects newly created device nodes after a kernel event.*

```sh
toybox find /data -maxdepth 5 -size +1M -type f -exec toybox ls -la {} ;
```
*List every file over 1MB with full permissions and timestamps. Replaces `find ... | xargs ls` entirely — no pipe needed.*

```sh
toybox find /proc -maxdepth 2 -name cmdline -exec toybox cat {} ;
```
*Dump the command line of every running process by reading /proc directly. Useful when ps output is restricted.*

---

## `flock`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `flock [-sxun] fd`

Manage advisory file locks.

### Examples

```sh
toybox flock /data/local/tmp/mylock toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Acquire an exclusive lock before running dd. Prevents two processes from writing the same block device simultaneously — critical for concurrent operations from system_server.*

---

## `inotifyd`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `inotifyd PROG FILE[:MASK] ...`

When a filesystem event matching MASK occurs to a FILE, run PROG as:

### Examples

```sh
toybox inotifyd toybox cat /data/local/tmp:w
```
*Watch /data/local/tmp for close-write events (file finished writing) and run cat on it each time. Event-driven execution with zero shell involvement.*

```sh
toybox inotifyd toybox strings /data/local/tmp/incoming:c
```
*Every time a new file is created in /data/local/tmp, run strings on it automatically. Useful for watching a drop directory from system_server context.*

```sh
toybox inotifyd toybox stat /data/local/tmp:dmv
```
*Fire stat on every delete, move, or close-write event — a live audit trail of file activity without polling. Event codes: `c`=create `d`=delete `m`=move `w`=close-write `r`=open `a`=access.*

---

## `ionice`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `ionice [-t] [-c CLASS] [-n LEVEL] [COMMAND...|-p PID]`

Change the I/O scheduling priority of a process. With no arguments (or just -p), display process' existing I/O class/priority.

### Examples

```sh
toybox ionice -c 1 -n 0 toybox find /data -type f -name '*.db'
```
*Run find at realtime I/O class, highest priority (`-n 0`). Use when storage contention is causing your operation to stall behind other processes.*

```sh
toybox ionice -c 3 toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Run dd at idle I/O priority — only runs when nothing else needs the disk. Safe background partition dump that won't impact the rest of the system.*

```sh
toybox ionice -p <PID>
```
*Display the current I/O class and priority of an existing process without modifying it.*

---

## `nc`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`

Forward stdin/stdout to a file or network connection.

### Examples

```sh
toybox nc -l -p 9999
```
*Listen on port 9999 for an incoming connection. From system_server this can receive data from another process on-device — a raw IPC channel without Binder overhead.*

```sh
toybox nc 127.0.0.1 9999
```
*Connect to the listener on localhost port 9999 and send data. Pair with the listener above for a simple two-process communication channel.*

---

## `netcat`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`

Forward stdin/stdout to a file or network connection.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `netcat [-46ElLtUu] [-wpq #] [-s addr] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`
> Upstream: `netcat [-46ELlntUu] [-pqWw #] [-s addr] [-o FILE] {IPADDR PORTNUM|-f FILENAME|COMMAND...}`

### Examples

```sh
toybox netcat --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `nice`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `nice [-n PRIORITY] COMMAND...`

Run a command line at an increased or decreased scheduling priority.

### Examples

```sh
toybox nice -n 19 toybox find /data -type f -name '*.so'
```
*Run find at lowest CPU niceness (19). The OS schedules it only when nothing else wants the CPU — background work that won't cause UI jank.*

```sh
toybox nice -n -20 toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Run dd at highest CPU priority (niceness -20, requires privilege). Gets the dump done as fast as possible regardless of system load.*

---

## `nohup`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `nohup COMMAND...`

Run a command that survives the end of its terminal.

### Examples

```sh
toybox nohup toybox inotifyd toybox strings /data/local/tmp/incoming:c
```
*Run inotifyd immune to `SIGHUP` so it keeps watching even if the parent process or session ends. Stack nohup + inotifyd for a persistent file-watch daemon with no shell.*

---

## `nsenter`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `nsenter [-t pid] [-F] [-i] [-m] [-n] [-p] [-u] [-U] COMMAND...`

Run COMMAND in an existing (set of) namespace(s).

### Examples

```sh
toybox nsenter -t <PID> -m toybox ls /proc/<PID>/root
```
*Enter the mount namespace of another process and run ls from inside it. Lets you see the filesystem exactly as that process sees it — useful for inspecting sandboxed app namespaces.*

---

## `prlimit`

` exec-capable` ` self-contained`

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

```sh
toybox prlimit --nofile=1024 toybox find /data -type f
```
*Cap the number of open file descriptors the child process can have. Prevents fd exhaustion when scanning large trees from within system_server's process space.*

```sh
toybox prlimit -p <PID>
```
*Display all current resource limits for an existing process without modifying them.*

---

## `rfkill`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `rfkill COMMAND [DEVICE]`

Enable/disable wireless devices.

### Examples

```sh
toybox rfkill --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `runcon`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `runcon CONTEXT COMMAND [ARGS...]`

Run a command in a specified security context.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox runcon u:r:shell:s0 toybox find /data -name '*.db'
```
*Execute find under the shell SELinux context. Changes what MAC policy allows the child process to access — useful for testing what a given context can reach without escalating permanently.*

---

## `setsid`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `setsid [-cdw] command [args...]`

Run process in a new session.

### Examples

```sh
toybox setsid toybox inotifyd toybox cat /data/local/tmp:w
```
*Run inotifyd in a new session, completely detached from the controlling terminal. Combined with nohup this gives you a proper background daemon from system_server.*

---

## `taskset`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `taskset [-ap] [mask] [PID | cmd [args...]]`

Launch a new task which may only run on certain processors, or change the processor affinity of an existing PID.

### Examples

```sh
toybox taskset 0x1 toybox find /data -type f -name '*.so'
```
*Pin find to CPU core 0 only (bitmask `0x1`). Isolates your operation to a specific core and avoids cache thrashing with other processes.*

```sh
toybox taskset 0xf toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin
```
*Allow dd to run on cores 0-3 (`0xf` = `1111` binary). On the S22's Snapdragon the first 4 are efficiency cores — lower power for background work.*

```sh
toybox taskset -p <PID>
```
*Show the current CPU affinity mask of a running process.*

---

## `timeout`

` exec-capable`

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

```sh
toybox timeout 5 toybox ping -c 1 8.8.8.8
```
*Kill ping after 5 seconds if it hasn't returned. Prevents any command from hanging indefinitely when called from system_server where you can't wait forever.*

```sh
toybox timeout 30 toybox find /data -name '*.db' -exec toybox strings {} ;
```
*Hard 30-second limit on the entire find+strings chain. Essential when scanning unknown directory trees from a privileged context — you need a kill switch.*

---

## `uclampset`

` exec-capable` ` self-contained`

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

```sh
toybox uclampset --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `unshare`

` exec-capable` ` self-contained`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `unshare [-imnpuUr] COMMAND...`

Create new container namespace(s) for this process and its children, allowing the new set of processes to have a different view of the system than the parent process.

### Examples

```sh
toybox unshare -m toybox mount --bind /data/local/tmp /data/local/tmp2
```
*Create a new private mount namespace then bind-mount inside it. The mount is invisible to every other process — clean temporary namespace manipulation.*

---

## `vconfig`

` exec-capable` ` self-contained`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `vconfig COMMAND [OPTIONS]`

Create and remove virtual ethernet devices

### Examples

```sh
toybox vconfig --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `watch`

` exec-capable`

> Can spawn other toybox commands — core shell replacement primitive.

**Usage:** `watch [-teb] [-n SEC] PROG ARGS`

Run PROG every -n seconds, showing output. Hit q to quit.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `watch [-teb] [-n SEC] PROG ARGS`
> Upstream: `watch [-tebx] [-n SEC] COMMAND...`

### Examples

```sh
toybox watch --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `xargs`

` exec-capable` ` self-contained`

> Spawns other commands AND has its own filter engine — maximum shell replacement value.

**Usage:** `xargs [-0prt] [-snE STR] COMMAND...`

Run command line one or more times, appending arguments from stdin.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `xargs [-0prt] [-snE STR] COMMAND...`
> Upstream: `xargs [-0Pprt] [-snE STR] [-a FILE] COMMAND...`

### Examples

```sh
toybox find /data/local/tmp -name '*.log' -print0 | toybox xargs -0 toybox grep -l ERROR
```
*`-print0` and `-0` pair together to safely handle filenames with spaces. xargs batches the file list into as few grep calls as possible rather than one per file.*

```sh
toybox find /proc -maxdepth 2 -name maps -print | toybox xargs toybox grep '/system'
```
*Grep every process memory map for system library loads. The pipe here is between two toybox commands you control — no shell involved.*

---

## `chattr`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chattr [-R] [-+=AacDdijsStTu] [-p PROJID] [-v VERSION] [FILE...]`

Change file attributes on a Linux file system.

### Examples

```sh
toybox chattr --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `chcon`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chcon [-hRv] CONTEXT FILE...`

Change the SELinux security context of listed file[s].

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox chcon --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `chgrp`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chgrp/chown [-RHLP] [-fvh] GROUP FILE...`

Change group of one or more files.

### Examples

```sh
toybox chgrp --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `chmod`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chmod [-R] MODE FILE...`

Change mode of listed file[s] (recursively with -R).

### Examples

```sh
toybox chmod --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `chown`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `chgrp/chown [-RHLP] [-fvh] GROUP FILE...`

Change group of one or more files.

### Examples

```sh
toybox chown --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cp`

` self-contained` ` io-explicit`

> Self-filtering with named file I/O — no pipes or redirection needed.

**Usage:** `cp [-adfHiLlnPpRrsTv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]`

Copy files from SOURCE to DEST.  If more than one SOURCE, DEST must be a directory.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cp [-adfHiLlnPpRrsTv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]`
> Upstream: `cp [-aDdFfHiLlnPpRrsTuv] [--preserve=motcxa] [-t TARGET] SOURCE... [DEST]`

### Examples

```sh
toybox cp --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cpio`

` self-contained` ` io-explicit`

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

```sh
toybox cpio --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cut`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `cut [-Ds] [-bcCfF LIST] [-dO DELIM] [FILE...]`

Print selected parts of lines from each FILE to standard output.

### Examples

```sh
toybox cut --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `date`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `date [-u] [-I RES] [-r FILE] [-d DATE] [+DISPLAY_FORMAT] [-D SET_FORMAT] [SET]`

Set/get the current date/time. With no SET shows the current date.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-I` | `RES` | ISO 8601 with RESolution d=date/h=hours/m=minutes/s=seconds/n=ns |
| `-s` | `DATE` | Set the system clock to DATE. |

### Examples

```sh
toybox date --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `diff`

` self-contained` ` io-explicit`

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

```sh
toybox diff --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `dmesg`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `dmesg [-Cc] [-r|-t|-T] [-n LEVEL] [-s SIZE] [-w]`

Print or control the kernel ring buffer.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `dmesg [-Cc] [-r|-t|-T] [-n LEVEL] [-s SIZE] [-w]`
> Upstream: `dmesg [-Cc] [-r|-t|-T] [-n LEVEL] [-s SIZE] [-w|-W]`

### Examples

```sh
toybox dmesg --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `egrep`

` self-contained` ` io-explicit`

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

```sh
toybox egrep --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `expr`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `expr ARG1 OPERATOR ARG2...`

Evaluate expression and print result. For example, "expr 1 + 2".

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox expr --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `fgrep`

` self-contained` ` io-explicit`

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

```sh
toybox fgrep --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `grep`

` self-contained` ` io-explicit`

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

```sh
toybox grep -r 'ro\.build' /system/etc
```
*Recursively search every file under /system/etc for the pattern. `-r` means grep walks the directory tree itself — no find needed.*

```sh
toybox grep -rl 'knox' /system
```
*`-l` prints only filenames that match, not the matching lines. Useful first pass to find which files are worth reading in full — keeps output manageable.*

```sh
toybox grep -a 'samsung' /dev/block/bootdevice/by-name/param
```
*`-a` treats a binary file as text so grep can scan raw block devices for ASCII strings — replaces `strings | grep` in one command.*

```sh
toybox grep -rn 'FactoryMode' /system/framework
```
*`-n` adds line numbers. Scanning unpacked framework jars for factory mode references without a shell pipeline.*

---

## `hwclock`

` self-contained`

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

```sh
toybox hwclock --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `i2cdetect`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `i2cdetect [-aqry] BUS [FIRST LAST]`

Detect i2c devices.

### Examples

```sh
toybox i2cdetect --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `id`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `id [-GZgnru] [USER...]`

Print user and group ID.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `id [-GZgnru] [USER...]`
> Upstream: `id [-Ggnru] [USER...]`

### Examples

```sh
toybox id --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `iotop`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `iotop [-AaKObq] [-n NUMBER] [-d SECONDS] [-p PID,] [-u USER,]`

Rank processes by I/O.

### Examples

```sh
toybox iotop --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ln`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `ln [-sfnv] [-t DIR] [FROM...] TO`

Create a link between FROM and TO. One/two/many arguments work like "mv" or "cp".

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `ln [-sfnv] [-t DIR] [FROM...] TO`
> Upstream: `ln [-fnrsTv] [-t DIR] [FROM...] TO`

### Examples

```sh
toybox ln --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `losetup`

` self-contained` ` io-explicit`

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

```sh
toybox losetup --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ls`

` self-contained`

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

```sh
toybox ls --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `lsattr`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `lsattr [-Radlpv] [FILE...]`

List file attributes on a Linux file system. Flag letters are defined in chattr help.

### Examples

```sh
toybox lsattr --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `modinfo`

` self-contained`

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

```sh
toybox modinfo --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `modprobe`

` self-contained`

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

```sh
toybox modprobe --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mount`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `mount [-afFrsvw] [-t TYPE] [-o OPTION,] [[DEVICE] DIR]`

Mount new filesystem(s) on directories. With no arguments, display existing mounts.

### Examples

```sh
toybox mount --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `netstat`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `netstat [-pWrxwutneal]`

Display networking information. Default is netstat -tuwx

### Examples

```sh
toybox netstat --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `nl`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `nl [-E] [-l #] [-b MODE] [-n STYLE] [-s SEPARATOR] [-v #] [-w WIDTH] [FILE...]`

Number lines of input.

### Examples

```sh
toybox nl --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `paste`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `paste [-s] [-d DELIMITERS] [FILE...]`

Merge corresponding lines from each input file.

### Examples

```sh
toybox paste --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `patch`

` self-contained`

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

```sh
toybox patch --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pgrep`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `pgrep [-clfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`

Search for process(es). PATTERN is an extended regular expression checked against command names.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `pgrep [-clfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`
> Upstream: `pgrep [-aclfnovx] [-d DELIM] [-L SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`

### Examples

```sh
toybox pgrep --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pkill`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `pkill [-fnovx] [-SIGNAL|-l SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]`

### Examples

```sh
toybox pkill --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `printenv`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `printenv [-0] [env_var...]`

Print environment variables.

### Examples

```sh
toybox printenv --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ps`

` self-contained`

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

```sh
toybox ps --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `realpath`

` self-contained`

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

```sh
toybox realpath --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `restorecon`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `restorecon [-D] [-F] [-R] [-n] [-v] FILE...`

Restores the default security contexts for the given files.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox restorecon --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sed`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `sed`

### Examples

```sh
toybox sed -n '/ro\.build/p' /system/build.prop
```
*`-n` suppresses default output, `/pattern/p` prints only matching lines. Cleaner than grep when you also need substitution in the same pass.*

```sh
toybox sed -i 's/old_value/new_value/g' /data/local/tmp/config.txt
```
*`-i` edits the file in place — no output redirection needed. The only sed operation that writes back to disk without a shell `>` operator.*

```sh
toybox sed '1,5d' /proc/kmsg
```
*Delete lines 1-5 and print the rest. Strip headers from kernel log output before further processing.*

---

## `sort`

` self-contained` ` io-explicit`

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

```sh
toybox sort --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tar`

` self-contained`

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

```sh
toybox tar --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `top`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `top [-Hhbq] [-k FIELD,] [-o FIELD,] [-s SORT] [-n NUMBER] [-m LINES] [-d SECONDS] [-p PID,] [-u USER,]`

Show process activity in real time.

### Examples

```sh
toybox top --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `touch`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `touch [-amch] [-d DATE] [-t TIME] [-r FILE] FILE...`

Update the access and modification times of each FILE to the current time.

### Examples

```sh
toybox touch --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `traceroute`

` self-contained`

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

```sh
toybox traceroute --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `traceroute6`

` self-contained`

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

```sh
toybox traceroute6 --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ulimit`

` self-contained`

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

```sh
toybox ulimit --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `umount`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `umount [-a [-t TYPE[,TYPE...]]] [-vrfD] [DIR...]`

Unmount the listed filesystems.

### Examples

```sh
toybox umount --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `uname`

` self-contained`

> Has its own filter/search engine — no pipe into grep or awk needed.

**Usage:** `uname [-asnrvm]`

Print system information.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `uname [-asnrvm]`
> Upstream: `uname [-asnrvmo]`

### Examples

```sh
toybox uname --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `xxd`

` self-contained` ` io-explicit`

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

```sh
toybox xxd --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cksum`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `cksum [-IPLN] [FILE...]`

For each file, output crc32 checksum value, length and name of file. If no files listed, copy from stdin.  Filename "-" is a synonym for stdin.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cksum [-IPLN] [FILE...]`
> Upstream: `cksum [-HIPLN] [FILE...]`

### Examples

```sh
toybox cksum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `comm`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `comm [-123] FILE1 FILE2`

Read FILE1 and FILE2, which should be ordered, and produce three text columns as output: lines only in FILE1; lines only in FILE2; and lines in both files. Filename "-" is a synonym for stdin.

### Examples

```sh
toybox comm --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `dd`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `dd [if|of=FILE] [ibs|obs|bs|count|seek|skip=N] [conv|status|iflag|oflag=FLAG[,FLAG...]]`

Copy/convert blocks of data from input to output, with the following keyword=value modifiers (and their default values):

### Examples

```sh
toybox dd if=/dev/block/bootdevice/by-name/param of=/data/local/tmp/param.bin bs=4096
```
*`if=` and `of=` replace both `<` and `>` entirely. The canonical shell-free way to read or write block devices and raw partition images.*

```sh
toybox dd if=/data/local/tmp/payload of=/dev/block/bootdevice/by-name/param bs=1 seek=256 conv=notrunc
```
*Write payload starting at byte 256 without touching the rest of the partition. `conv=notrunc` is critical — without it dd truncates the output to the input size.*

```sh
toybox dd if=/dev/urandom of=/data/local/tmp/test.bin bs=1M count=1
```
*Generate 1MB of random data to a file — useful for entropy testing or creating test payloads without /dev/random blocking.*

---

## `fallocate`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `fallocate [-l size] [-o offset] file`

Tell the filesystem to allocate space for a file.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `fallocate [-l size] [-o offset] file`
> Upstream: `fallocate [-o OFFSET] -l SIZE FILE`

### Examples

```sh
toybox fallocate --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `gzip`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `gzip [-19cdfkt] [FILE...]`

Compress files. With no files, compresses stdin to stdout. On success, the input files are removed and replaced by new files with the .gz suffix.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox gzip --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `install`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `install [-dDpsv] [-o USER] [-g GROUP] [-m MODE] [-t TARGET] [SOURCE...] [DEST]`

Copy files and set attributes.

### Examples

```sh
toybox install --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mv`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `mv [-finTv] [-t TARGET] SOURCE... [DEST]`

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mv [-finTv] [-t TARGET] SOURCE... [DEST]`
> Upstream: `mv [-FfinTvx] [-t TARGET] SOURCE... [DEST]`

### Examples

```sh
toybox mv --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `rev`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `rev [FILE...]`

Output each line reversed, when no files are given stdin is used.

### Examples

```sh
toybox rev --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `split`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `split [-a SUFFIX_LEN] [-b BYTES] [-l LINES] [-n PARTS] [INPUT [OUTPUT]]`

Copy INPUT (or stdin) data to a series of OUTPUT (or "x") files with alphabetically increasing suffix (aa, ab, ac... az, ba, bb...).

### Examples

```sh
toybox split --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tee`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `tee [-ai] [FILE...]`

Copy stdin to each listed file, and also to stdout. Filename "-" is a synonym for stdout.

### Examples

```sh
toybox tee --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `uudecode`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `uudecode [-o OUTFILE] [INFILE]`

Decode file from stdin (or INFILE).

### Examples

```sh
toybox uudecode --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `wc`

` io-explicit`

> All I/O via named flags or args — replaces shell redirection.

**Usage:** `wc -lwcm [FILE...]`

Count lines, words, and characters in input.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `wc -lwcm [FILE...]`
> Upstream: `wc [-Llwcm] [FILE...]`

### Examples

```sh
toybox wc --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `acpi`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `acpi [-abctV]`

Show status of power sources and thermal devices.

### Examples

```sh
toybox acpi --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `base64`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `base64 [-di] [-w COLUMNS] [FILE...]`

Encode or decode in base64.

### Examples

```sh
toybox base64 --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `basename`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `basename [-a] [-s SUFFIX] NAME... | NAME [SUFFIX]`

Return non-directory portion of a pathname removing suffix.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-s` | `SUFFIX` | Remove suffix (implies -a) |

### Examples

```sh
toybox basename --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `blkdiscard`

` terminal`

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

```sh
toybox blkdiscard --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `blkid`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `blkid [-o TYPE] [-s TAG] [-UL] DEV...`

Print type, label and UUID of filesystem on a block device or image.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-o` | `TYPE` | Output format (full, value, export) |
| `-s` | `TAG` | Only show matching tags (default all) |

### Examples

```sh
toybox blkid --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `blockdev`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `blockdev --OPTION... BLOCKDEV...`

Call ioctl(s) on each listed block device

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `--setbsz` | `BYTES` | Set block size |
| `--setra` | `SECTORS` | Set readahead |

### Examples

```sh
toybox blockdev --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cal`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `cal [[[DAY] MONTH] YEAR]`

Print a calendar.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `cal [[[DAY] MONTH] YEAR]`
> Upstream: `cal [-h] [[[DAY] MONTH] YEAR]`

### Examples

```sh
toybox cal --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cat`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `cat [-etuv] [FILE...]`

Copy (concatenate) files to stdout.  If no files listed, copy from stdin. Filename "-" is a synonym for stdin.

### Examples

```sh
toybox cat --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `clear`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `clear`

### Examples

```sh
toybox clear --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `cmp`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `cmp [-ls] [-n LEN] FILE1 [FILE2 [SKIP1 [SKIP2]]]`

Compare the contents of files (vs stdin if only one given), optionally skipping bytes at start.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-n` | `LEN` | Compare at most LEN bytes |

### Examples

```sh
toybox cmp --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `devmem`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `devmem ADDR [WIDTH [DATA]]`

Read/write physical address. WIDTH is 1, 2, 4, or 8 bytes (default 4). Prefix ADDR with 0x for hexadecimal, output is in same base as address.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `devmem ADDR [WIDTH [DATA]]`
> Upstream: `devmem [-f FILE] ADDR [WIDTH [DATA...]]`

### Examples

```sh
toybox devmem --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `df`

` terminal`

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

```sh
toybox df --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `dirname`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `dirname PATH...`

Show directory portion of path.

### Examples

```sh
toybox dirname --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `dos2unix`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `dos2unix [FILE...]`

Convert newline format from dos "\r\n" to unix "\n". If no files listed copy from stdin, "-" is a synonym for stdin.

### Examples

```sh
toybox dos2unix --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `du`

` terminal`

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

```sh
toybox du --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `echo`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `echo [-neE] [ARG...]`

Write each argument to stdout, one space between each, followed by a newline.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `echo [-neE] [ARG...]`
> Upstream: `echo [-Een] [ARG...]`

### Examples

```sh
toybox echo --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `expand`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `expand [-t TABLIST] [FILE...]`

Expand tabs to spaces according to tabstops.

### Examples

```sh
toybox expand --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `false`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `false`

### Examples

```sh
toybox false --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `file`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `file [-bhLs] [FILE...]`

Examine the given files and describe their content types.

### Examples

```sh
toybox file --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `fmt`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `fmt [-w WIDTH] [FILE...]`

Reformat input to wordwrap at a given line length, preserving existing indentation level, writing to stdout.

### Flags

| Flag | Arg | Meaning |
|------|-----|---------|
| `-w` | `WIDTH` | Maximum characters per line (default 75) |

### Examples

```sh
toybox fmt --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `free`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `free [-bkmgt]`

Display the total, free and used amount of physical memory and swap space.

### Examples

```sh
toybox free --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `freeramdisk`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `freeramdisk [RAM device]`

Free all memory allocated to specified ramdisk

### Examples

```sh
toybox freeramdisk --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `fsfreeze`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `fsfreeze {-f | -u} MOUNTPOINT`

Freeze or unfreeze a filesystem.

### Examples

```sh
toybox fsfreeze --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `fsync`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `fsync [-d] [FILE...]`

Flush disk cache for FILE(s), writing cached data to storage device.

### Examples

```sh
toybox fsync --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `getconf`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getconf -a [PATH] | -l | NAME [PATH]`

Get system configuration values. Values from pathconf(3) require a path.

### Examples

```sh
toybox getconf --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `getenforce`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getenforce`

Shows whether SELinux is disabled, enforcing, or permissive.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox getenforce --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `getfattr`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `getfattr [-d] [-h] [-n NAME] FILE...`

Read POSIX extended attributes.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox getfattr --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `getopt`

` terminal`

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

```sh
toybox getopt --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `groups`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `groups [user]`

Print the groups a user is in.

### Examples

```sh
toybox groups --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `gunzip`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `gunzip [-cfkt] [FILE...]`

Decompress files. With no files, decompresses stdin to stdout. On success, the input files are removed and replaced by new files without the .gz suffix.

### Examples

```sh
toybox gunzip --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `head`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `head [-n NUM] [FILE...]`

Copy first lines from files to stdout. If no files listed, copy from stdin. Filename "-" is a synonym for stdin.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `head [-n NUM] [FILE...]`
> Upstream: `head [-cn NUM] [-qv] [FILE...]`

### Examples

```sh
toybox head --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `help`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `help [-ahu] [COMMAND]`

### Examples

```sh
toybox help --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `hostname`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `hostname [-bdsf] [-F FILENAME] [newname]`

Get/set the current hostname.

### Examples

```sh
toybox hostname --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `i2cdump`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `i2cdump [-fy] BUS CHIP`

Dump i2c registers.

### Examples

```sh
toybox i2cdump --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `i2cget`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `i2cget [-fy] BUS CHIP [ADDR]`

Read an i2c register.

### Examples

```sh
toybox i2cget --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `i2cset`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `i2cset [-fy] BUS CHIP ADDR VALUE... MODE`

Write an i2c register. MODE is b for byte, w for 16-bit word, i for I2C block.

### Examples

```sh
toybox i2cset --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `iconv`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `iconv [-f FROM] [-t TO] [FILE...]`

Convert character encoding of files.

### Examples

```sh
toybox iconv --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ifconfig`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `ifconfig [-aS] [INTERFACE [ACTION...]]`

Display or configure network interface.

### Examples

```sh
toybox ifconfig --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `insmod`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `insmod MODULE [OPTION...]`

Load the module named MODULE passing options if given.

### Examples

```sh
toybox insmod --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `iorenice`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `iorenice PID [CLASS] [PRIORITY]`

Display or change I/O priority of existing process. CLASS can be "rt" for realtime, "be" for best effort, "idle" for only when idle, or "none" to leave it alone. PRIORITY can be 0-7 (0 is highest, default 4).

### Examples

```sh
toybox iorenice --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `kill`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `kill [-l [SIGNAL] | -s SIGNAL | -SIGNAL] PID...`

Send signal to process(es).

### Examples

```sh
toybox kill --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `killall`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `killall [-l] [-iqv] [-SIGNAL|-s SIGNAL] PROCESS_NAME...`

Send a signal (default: TERM) to all processes with the given names.

### Examples

```sh
toybox killall --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `load_policy`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `load_policy FILE`

Load the specified SELinux policy file.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox load_policy --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `log`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `log [-p PRI] [-t TAG] [MESSAGE...]`

Logs message (or stdin) to logcat.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox log --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `logger`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `logger [-s] [-t TAG] [-p [FACILITY.]PRIORITY] [MESSAGE...]`

Log message (or stdin) to syslog.

### Examples

```sh
toybox logger --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `logname`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `logname`

Print the current user name.

### Examples

```sh
toybox logname --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `lsmod`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lsmod`

Display the currently loaded modules, their sizes and their dependencies.

### Examples

```sh
toybox lsmod --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `lsof`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lsof [-lt] [-p PID1,PID2,...] [FILE...]`

List all open files belonging to all active processes, or processes using listed FILE(s).

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox lsof --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `lspci`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lspci [-ekmn] [-i FILE]`

List PCI devices.

### Examples

```sh
toybox lspci --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `lsusb`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `lsusb [-i]`

List USB hosts/devices.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `lsusb [-i]`
> Upstream: `lsusb [-ti]`

### Examples

```sh
toybox lsusb --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `makedevs`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `makedevs [-d device_table] rootdir`

Create a range of special files as specified in a device table.

### Examples

```sh
toybox makedevs --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `md5sum`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```sh
toybox md5sum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `microcom`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `microcom [-s SPEED] [-X] DEVICE`

Simple serial console.

### Examples

```sh
toybox microcom --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mkdir`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mkdir [-vp] [-m MODE] [DIR...]`

Create one or more directories.

### Examples

```sh
toybox mkdir --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mkfifo`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mkfifo [-Z CONTEXT] [NAME...]`

Create FIFOs (named pipes).

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mkfifo [-Z CONTEXT] [NAME...]`
> Upstream: `mkfifo [NAME...]`

### Examples

```sh
toybox mkfifo --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mknod`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mknod [-Z CONTEXT] ... [-m MODE] NAME TYPE [MAJOR MINOR]`

Create a special file NAME with a given type. TYPE is b for block device, c or u for character device, p for named pipe (which ignores MAJOR/MINOR).

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mknod [-Z CONTEXT] ... [-m MODE] NAME TYPE [MAJOR MINOR]`
> Upstream: `mknod [-m MODE] NAME TYPE [MAJOR MINOR]`

### Examples

```sh
toybox mknod --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mkswap`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mkswap [-L LABEL] DEVICE`

Set up a Linux swap area on a device or file.

### Examples

```sh
toybox mkswap --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mktemp`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mktemp [-dqu] [-p DIR] [TEMPLATE]`

Safely create a new file "DIR/TEMPLATE" and print its name.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `mktemp [-dqu] [-p DIR] [TEMPLATE]`
> Upstream: `mktemp [-dqtu] [-p DIR] [TEMPLATE]`

### Examples

```sh
toybox mktemp --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `more`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `more [FILE...]`

View FILE(s) (or stdin) one screenfull at a time.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox more --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `mountpoint`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `mountpoint [-qd] DIR`

mountpoint [-qx] DEVICE

### Examples

```sh
toybox mountpoint --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `nbd-client`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `nbd-client [-ns] [-b BLKSZ] HOST PORT DEVICE`

### Examples

```sh
toybox nbd-client --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `nproc`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `nproc [--all]`

Print number of processors.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `nproc [--all]`
> Upstream: `nproc [-a]`

### Examples

```sh
toybox nproc --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `od`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `od [-bcdosxv] [-j #] [-N #] [-w #] [-A doxn] [-t acdfoux[#]]`

Dump data in octal/hex.

### Examples

```sh
toybox od --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `partprobe`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `partprobe DEVICE...`

Tell the kernel about partition table changes

### Examples

```sh
toybox partprobe --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pidof`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pidof [-s] [-o omitpid[,omitpid...]] [NAME...]`

Print the PIDs of all processes with the given names.

### Examples

```sh
toybox pidof --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ping`

` terminal`

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

```sh
toybox ping --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `ping6`

` terminal`

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

```sh
toybox ping6 --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pivot_root`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pivot_root OLD NEW`

Swap OLD and NEW filesystems (as if by simultaneous mount --move), and move all processes with chdir or chroot under OLD into NEW (including kernel threads) so OLD may be unmounted.

### Examples

```sh
toybox pivot_root --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pmap`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pmap [-pqx] PID...`

Report the memory map of a process or processes.

### Examples

```sh
toybox pmap --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `printf`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `printf FORMAT [ARGUMENT...]`

Format and print ARGUMENT(s) according to FORMAT, using C printf syntax (% escapes for cdeEfgGiosuxX, \ escapes for abefnrtv0 or \OCTAL or \xHEX).

### Examples

```sh
toybox printf --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pwd`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pwd [-L|-P]`

Print working (current) directory.

### Examples

```sh
toybox pwd --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `pwdx`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `pwdx PID...`

Print working directory of processes listed on command line.

### Examples

```sh
toybox pwdx --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `readelf`

` terminal`

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

```sh
toybox readelf --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `readlink`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `readlink FILE...`

With no options, show what symlink points to, return error if not symlink.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `readlink FILE...`
> Upstream: `readlink [-efmnqz] FILE...`

### Examples

```sh
toybox readlink --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `renice`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `renice [-gpu] -n INCREMENT ID...`

### Examples

```sh
toybox renice --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `rm`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rm [-fiRrv] FILE...`

Remove each argument from the filesystem.

### Examples

```sh
toybox rm --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `rmdir`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rmdir [-p] [DIR...]`

Remove one or more directories.

### Examples

```sh
toybox rmdir --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `rmmod`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `rmmod [-wf] MODULE...`

Unload the given kernel modules.

### Examples

```sh
toybox rmmod --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `rtcwake`

` terminal`

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

```sh
toybox rtcwake --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sendevent`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sendevent DEVICE TYPE CODE VALUE`

Sends a Linux input event.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox sendevent --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `seq`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `seq [-w|-f fmt_str] [-s sep_str] [first] [increment] last`

Count from first to last, by increment. Omitted arguments default to 1. Two arguments are used as first and last. Arguments can be negative or floating point.

### Examples

```sh
toybox seq --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `setenforce`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `setenforce [enforcing|permissive|1|0]`

Sets whether SELinux is enforcing (1) or permissive (0).

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox setenforce --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `setfattr`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `setfattr [-h] [-x|-n NAME] [-v VALUE] FILE...`

Write POSIX extended attributes.

### Examples

```sh
toybox setfattr --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sha1sum`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```sh
toybox sha1sum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sha224sum`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```sh
toybox sha224sum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sha256sum`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```sh
toybox sha256sum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sha384sum`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```sh
toybox sha384sum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sha512sum`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `???sum [-bcs] [FILE]...`

Calculate hash for each input file, reading from stdin if none, writing hexadecimal digits to stdout for each input file (md5=32 hex digits, sha1=40, sha224=56, sha256=64, sha384=96, sha512=128) followed by filename.

### Examples

```sh
toybox sha512sum --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sleep`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sleep DURATION...`

Wait before exiting.

### Examples

```sh
toybox sleep --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `stat`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `stat [-tfL] [-c FORMAT] FILE...`

Display status of files or filesystems.

### Examples

```sh
toybox stat --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `strings`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `strings [-fo] [-t oxd] [-n LEN] [FILE...]`

Display printable strings in a binary file

### Examples

```sh
toybox strings --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `stty`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `stty [-ag] [-F device] SETTING...`

Get/set terminal configuration.

> [!NOTE]
> This command is **not in upstream toybox** — it is a Samsung addition.

### Examples

```sh
toybox stty --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `swapoff`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `swapoff FILE`

Disable swapping on a device or file.

### Examples

```sh
toybox swapoff --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `swapon`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `swapon [-d] [-p priority] filename`

Enable swapping on a given device/file.

### Examples

```sh
toybox swapon --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sync`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `sync`

Write pending cached data to disk (synchronize), blocking until done.

### Examples

```sh
toybox sync --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `sysctl`

` terminal`

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

```sh
toybox sysctl --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tac`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tac [FILE...]`

Output lines in reverse order.

### Examples

```sh
toybox tac --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tail`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tail [-n|c NUMBER] [-f|F] [-s SECONDS] [FILE...]`

Copy last lines from files to stdout. If no files listed, copy from stdin. Filename "-" is a synonym for stdin.

### Examples

```sh
toybox tail --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `test`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `test`

### Examples

```sh
toybox test --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `time`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `time [-pv] COMMAND...`

Run command line and report real, user, and system time elapsed in seconds. (real = clock on the wall, user = cpu used by command's code, system = cpu used by OS on behalf of command.)

### Examples

```sh
toybox time --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tr`

` terminal`

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

```sh
toybox tr --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `true`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `true`

### Examples

```sh
toybox true --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `truncate`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `truncate [-c] -s SIZE file...`

Set length of file(s), extending sparsely if necessary.

### Examples

```sh
toybox truncate --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tty`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tty [-s]`

Show filename of terminal connected to stdin. If none print "not a tty" and exit with nonzero status.

### Examples

```sh
toybox tty --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `tunctl`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `tunctl [-dtT] [-u USER] NAME`

Create and delete tun/tap virtual ethernet devices.

### Examples

```sh
toybox tunctl --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `uniq`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uniq [-cduiz] [-w MAXCHARS] [-f FIELDS] [-s CHAR] [INFILE [OUTFILE]]`

Report or filter out repeated lines in a file

### Examples

```sh
toybox uniq --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `unix2dos`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `unix2dos [FILE...]`

Convert newline format from unix "\n" to dos "\r\n". If no files listed copy from stdin, "-" is a synonym for stdin.

### Examples

```sh
toybox unix2dos --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `unlink`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `unlink FILE`

Delete one file.

### Examples

```sh
toybox unlink --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `uptime`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uptime [-ps]`

Tell the current time, how long the system has been running, the number of users, and the system load averages for the past 1, 5 and 15 minutes.

### Examples

```sh
toybox uptime --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `usleep`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `usleep MICROSECONDS`

Pause for MICROSECONDS microseconds.

### Examples

```sh
toybox usleep --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `uuencode`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uuencode [-m] [INFILE] ENCODE_FILENAME`

Uuencode stdin (or INFILE) to stdout, with ENCODE_FILENAME in the output.

### Examples

```sh
toybox uuencode --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `uuidgen`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `uuidgen`

Create and print a new RFC4122 random UUID.

### Examples

```sh
toybox uuidgen --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `vi`

` terminal`

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

```sh
toybox vi --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `vmstat`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `vmstat [-n] [DELAY [COUNT]]`

Print virtual memory statistics, repeating each DELAY seconds, COUNT times. (With no DELAY, prints one line. With no COUNT, repeats until killed.)

### Examples

```sh
toybox vmstat --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `which`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `which [-a] filename ...`

Search $PATH for executable files matching filename(s).

### Examples

```sh
toybox which --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `whoami`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `logname`

Print the current user name.

### Examples

```sh
toybox whoami --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `yes`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `yes [args...]`

Repeatedly output line until killed. If no args, output 'y'.

### Examples

```sh
toybox yes --help
```
*No composed example written yet — see flags above and build from the usage line.*

---

## `zcat`

` terminal`

> Output only — limited composition, but may feed exec-capable commands.

**Usage:** `zcat [FILE...]`

Decompress files to stdout. Like `gzip -dc`.

> [!WARNING]
> **Samsung's version differs from upstream toybox.**
> Samsung: `zcat [FILE...]`
> Upstream: `zcat [-f] [FILE...]`

### Examples

```sh
toybox zcat --help
```
*No composed example written yet — see flags above and build from the usage line.*

---
