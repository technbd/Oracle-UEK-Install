## Oracle UEK Install:
Oracle Unbreakable Enterprise Kernel (UEK) is a Linux kernel built and optimized by Oracle to run Oracle software. To install Oracle UEK on Oracle Linux 8 (OEL 8), follow these steps:


_Oracle Linux and Unbreakable Enterprise Kernel (UEK) Releases:_

| OL Release   | Initial UEK kernel             | Initial RHCK kernel        | UEK5 supported  | UEK6 supported	   | UEK7 supported    |
|--------------|--------------------------------|--------------------------- |---------------- | ----------------- | ----------------- | 
| OL9U4        | kernel-uek-5.15.0-205.149.5.1	| kernel-5.14.0-427          | Not Available   | Not Available     | Yes, default      |
| OL9          | kernel-uek-5.15.0-0.30.19      | kernel-5.14.0-70.13.1.0.3  | Not Available   | Not Available     | Yes, default      |
|              |                                |                            |                 |                   |                   |
| OL8U10       | kernel-uek-5.15.0-206.153.7    | kernel-4.18.0-544          | Not Available   | Yes               | Yes, default      |
| OL8U7        | kernel-uek-5.15.0-3.60.5.1	    | kernel-4.18.0-425.3.1      | Not Available   | Yes               | Yes, default      |
| OL8U4        | kernel-uek-5.4.17-2102.201.3   | kernel-4.18.0-305          | Not Available   | Yes, default	   | No. OL8U5 req.    |
| OL8U2        | kernel-uek-5.4.17-2011.1.2     | kernel-4.18.0-193          | Not Available   | Yes, default	   | No. OL8U5 req.    |
| OL8          | Not Available                  | kernel-4.18.0-80           | Not Available   | No. OL8U1 req.	   | No. OL8U5 req.    |
|              |                                |                            |                 |                   |                   |
| OL7U9        | kernel-uek-5.4.17-2011.6.2     | kernel-3.10.0-1160         | Yes	           | Yes, default	   | Not Available     |
| OL7          | kernel-uek-3.8.13-35.3.1       | kernel-3.10.0-123          | No. OL7U5 req.  | No. OL7U7 req.	   | Not Available     |



Here’s the high-level UEK version mapping across Oracle Linux releases:
| Oracle Linux Release | UEK Major Version | Example Kernel Version String                                        |
| -------------------- | ----------------- | -------------------------------------------------------------------- |
| **OEL 5**            | UEK R1            | `2.6.32-300.10.1.el5uek.x86_64`                                      |
| **OEL 6**            | UEK R1 → R4       | `2.6.32-300.el6uek.x86_64` → `4.1.12-124.39.1.el6uek.x86_64`         |
| **OEL 7**            | UEK R3 → R5       | `3.8.13-118.16.4.el7uek.x86_64` → `4.14.35-2047.505.1.el7uek.x86_64` |
| **OEL 8**            | UEK R6 → R7       | `5.4.17-2011.0.7.el8uek.x86_64` → `5.15.x` (in later updates)        |


#### Breakdown by UEK Release:

- UEK R1 → Based on Linux 2.6.32 (OEL 5 & 6 early)
- UEK R2 → Based on Linux 3.0.36 (rarely used widely, OL 6 only)
- UEK R3 → Based on Linux 3.8.13 (OEL 6 late & OEL 7 early)
- UEK R4 → Based on Linux 4.1.12 (OEL 6 late, OEL 7 mid)
- UEK R5 → Based on Linux 4.14.35 (OEL 7 late, OEL 8 early betas)
- UEK R6 → Based on Linux 5.4.17 (OEL 8)
- UEK R7 → Based on Linux 5.15.x (OEL 8 latest updates)


#### Oracle UEK Versions by OEL Release:
| UEK Release | Kernel Version (approx) | Codename | Supported OEL Versions | Notes                                                                                        |
| ----------- | ----------------------- | -------- | ---------------------- | -------------------------------------------------------------------------------------------- |
| **UEK R1**  | 2.6.32.x                | –        | OEL 5, OEL 6           | First UEK release, optimized for Oracle DB workloads.                                        |
| **UEK R2**  | 3.8.x                   | –        | OEL 5, OEL 6, OEL 7    | Major perf improvements, NUMA, DTrace.                                                       |
| **UEK R3**  | 3.8.x → 3.18.x          | –        | OEL 6, OEL 7           | Long-term support, better scalability.                                                       |
| **UEK R4**  | 4.1.x                   | –        | OEL 6, OEL 7           | More Docker/container support, large memory optimization.                                    |
| **UEK R5**  | 4.14.x                  | –        | OEL 6, OEL 7, OEL 8    | Meltdown/Spectre patches, Oracle Cloud optimized.                                            |
| **UEK R6**  | 5.4.x                   | –        | OEL 7, OEL 8           | **Kernel 5.4** base (e.g., 5.4.17-…el8uek), long-term stable, great for modern DB workloads. |
| **UEK R7**  | 6.1.x                   | –        | OEL 8, OEL 9           | Latest long-term kernel, better performance, new hardware support.                           |


### So, is it UEK6 or UEK7?
- **UEK6** is generally based on 5.4.x kernels.
- **UEK7** is based on 6.1.x kernels.
- **5.15.x kernels** in Oracle Linux 8 are part of **UEK R6 Update releases** — Oracle started including 5.15 kernels as part of the UEK6 line as a backport/update for hardware enablement and security.

#### In short:
- `5.15.0-200.131.27.el8uek.x86_64` is a **UEK6 update kernel** with 5.15 base.
- It is **not UEK7** (which is 6.1.x based).


### Check Current Kernel Version:

```
uname -r

5.15.0-3.60.5.1.el8uek.x86_64
```


```
rpm -qa kernel
 
kernel-4.18.0-425.3.1.el8.x86_64
```


```
rpm -qa | grep kernel

kernel-tools-4.18.0-425.3.1.el8.x86_64
kernel-modules-4.18.0-425.3.1.el8.x86_64
kernel-core-4.18.0-425.3.1.el8.x86_64
kernel-headers-4.18.0-425.3.1.el8.x86_64
kernel-uek-5.15.0-3.60.5.1.el8uek.x86_64
kernel-4.18.0-425.3.1.el8.x86_64
kernel-uek-core-5.15.0-3.60.5.1.el8uek.x86_64
kernel-tools-libs-4.18.0-425.3.1.el8.x86_64
kernel-uek-modules-5.15.0-3.60.5.1.el8uek.x86_64
```


```
yum list --installed kernel

Installed Packages
kernel.x86_64                 4.18.0-425.3.1.el8                @anaconda
```


```
yum list --installed | grep kernel

kernel.x86_64                                      4.18.0-425.3.1.el8             @anaconda
kernel-core.x86_64                                 4.18.0-425.3.1.el8             @anaconda
kernel-headers.x86_64                              4.18.0-425.3.1.el8             @anaconda
kernel-modules.x86_64                              4.18.0-425.3.1.el8             @anaconda
kernel-tools.x86_64                                4.18.0-425.3.1.el8             @anaconda
kernel-tools-libs.x86_64                           4.18.0-425.3.1.el8             @anaconda
kernel-uek.x86_64                                  5.15.0-3.60.5.1.el8uek         @anaconda
kernel-uek-core.x86_64                             5.15.0-3.60.5.1.el8uek         @anaconda
kernel-uek-modules.x86_64                          5.15.0-3.60.5.1.el8uek         @anaconda
```


```
ls -R /lib/modules/ uname -r /kernel | less
```




### Check Repositories and Releases:

```
yum repolist all

repo id               repo name                                                                                              status

ol8_MODRHCK           Latest RHCK with fixes from Oracle for Oracle Linux 8 (x86_64)                                         disabled
ol8_UEKR6             Latest Unbreakable Enterprise Kernel Release 6 for Oracle Linux 8 (x86_64)                             enabled
ol8_UEKR6_RDMA        Oracle Linux 8 UEK6 RDMA (x86_64)                                                                      disabled
ol8_UEKR7             Latest Unbreakable Enterprise Kernel Release 7 for Oracle Linux 8 (x86_64)                             enabled
ol8_UEKR7_RDMA        Oracle Linux 8 UEK7 RDMA (x86_64)                                                                      disabled
ol8_addons            Oracle Linux 8 Addons (x86_64)                                                                         enabled
ol8_appstream         Oracle Linux 8 Application Stream (x86_64)                                                             enabled
ol8_automation        Oracle Linux Automation Manager 1.0 based on the open source projects Ansible and AWX (x86_64)         disabled
ol8_automation2       Oracle Linux Automation Manager 2.0 based on the open source projects Ansible and AWX (x86_64)         enabled
ol8_baseos_latest     Oracle Linux 8 BaseOS Latest (x86_64)                                                                  enabled
```


```
yum list --installed | grep oraclelinux-release

oraclelinux-release.x86_64                         8:8.7-1.0.6.el8        @anaconda
oraclelinux-release-el8.x86_64                     1.0-28.el8             @anaconda
```


### Install and Upgrade Oracle Linux Release:

```
dnf install oraclelinux-release-el8
```


```
dnf upgrade oraclelinux-release-el8
```


```
dnf upgrade -y 
```


### Enable Unbreakable Enterprise Kernel Release 7:

```
dnf config-manager --set-disabled ol8_UEKR6

or,

dnf config-manager --disable ol8_UEKR6
```


```
dnf config-manager --enable ol8_UEKR7
```


```
yum repolist all
```


### Install Unbreakable Enterprise Kernel:

```
dnf install kernel-uek
dnf install kernel-uek-devel
```


```
dnf update -y
```


### Reboot the System:

```
systemctl reboot
```


```
uname -r

5.15.0-207.156.6.el8uek.x86_64
```


### Remove UEK Kernel Packages:

```
rpm -qa | grep kernel

dnf remove kernel-uek-5.15.0-207.156.6.el8uek
```


Following these steps will ensure that Oracle UEK is correctly installed and running on Oracle Linux 8.



---
---


## Change default kernel using `grubby`:
To change the default kernel using the `grubby` command, follow these steps:


```
cat /etc/default/grub
```


### List All Installed Kernels:

Use the `grubby` command to list all installed kernels on your system. Look through the output to identify the path of the UEK kernel. For example:

```
grubby --info=ALL


### Output:

index=0
kernel="/boot/vmlinuz-5.15.0-207.156.6.el8uek.x86_64"
...

index=1
kernel="/boot/vmlinuz-5.15.0-3.60.5.1.el8uek.x86_64"
...

index=2
kernel="/boot/vmlinuz-4.18.0-553.5.1.el8_10.x86_64"
...

index=3
kernel="/boot/vmlinuz-4.18.0-425.3.1.el8.x86_64"
...

index=4
kernel="/boot/vmlinuz-0-rescue-6ac0fcf5ae7442eb8d783ef658e364c8"
...

```


```
ll -h /boot/vmlinuz*

-rwxr-xr-x. 1 root root 13M Jun 26 02:40 /boot/vmlinuz-0-rescue-6ac0fcf5ae7442eb8d783ef658e364c8
-rwxr-xr-x. 1 root root 11M Nov  9  2022 /boot/vmlinuz-4.18.0-425.3.1.el8.x86_64
-rwxr-xr-x. 1 root root 11M Jun  6 04:26 /boot/vmlinuz-4.18.0-553.5.1.el8_10.x86_64
-rwxr-xr-x. 1 root root 13M Jun  6 15:47 /boot/vmlinuz-5.15.0-207.156.6.el8uek.x86_64
-rwxr-xr-x. 1 root root 13M Oct 20  2022 /boot/vmlinuz-5.15.0-3.60.5.1.el8uek.x86_64
```



### Check the default kernel:

```
grubby --default-kernel

/boot/vmlinuz-5.15.0-207.156.6.el8uek.x86_64
```


### Set the Default Kernel:

```
grubby --set-default /boot/vmlinuz-4.18.0-553.5.1.el8_10.x86_64

or,

grubby --set-default /boot/vmlinuz-5.15.0-207.156.6.el8uek.x86_64
```


```
grubby --default-kernel

/boot/vmlinuz-4.18.0-553.5.1.el8_10.x86_64
```


### Reboot the System:
_Reboot the system to apply the changes:_
```
reboot
```


```
uname -r

4.18.0-553.5.1.el8_10.x86_64
```


### Install the specific kernel version:

_Enable `ol8_UEKR6` repo:_
```
dnf config-manager --enable ol8_UEKR6
dnf config-manager --disable ol8_UEKR6

dnf repolist all
```


_Install Kernel:_
```
dnf install -y kernel-uek-5.4.17-2136.337.5.el8uek

Or,

dnf install -y kernel-4.18.0-553.16.1.el8_10.x86_64
```


_If remove Kernel:_
```
dnf remove -y kernel-uek-5.4.17-2136.337.5.el8uek
```


```
ll -h /boot/vmlinuz*

-rwxr-xr-x. 1 root root 13M Aug  6 00:23 /boot/vmlinuz-0-rescue-fcae1c255a0d495abdeff2cfa52daa0e
-rwxr-xr-x. 1 root root 11M Nov 16  2023 /boot/vmlinuz-4.18.0-513.5.1.el8_9.x86_64
-rwxr-xr-x  1 root root 11M Aug  8  2024 /boot/vmlinuz-4.18.0-553.16.1.el8_10.x86_64
-rwxr-xr-x. 1 root root 13M Oct  5  2023 /boot/vmlinuz-5.15.0-200.131.27.el8uek.x86_64
-rwxr-xr-x  1 root root 11M Nov  5  2024 /boot/vmlinuz-5.4.17-2136.337.5.el8uek.x86_64
```


_Set the Default Kernel:_
```
grubby --set-default /boot/vmlinuz-5.4.17-2136.337.5.el8uek.x86_64

Or,

grubby --set-default /boot/vmlinuz-4.18.0-553.16.1.el8_10.x86_64
```


_Verify:_
```
grubby --default-kernel


/boot/vmlinuz-5.4.17-2136.337.5.el8uek.x86_64

Or,

/boot/vmlinuz-4.18.0-553.16.1.el8_10.x86_64
```


```
reboot
```


```
uname -r

5.4.17-2136.337.5.el8uek.x86_64
```


By following these steps, you can change the default kernel to the Unbreakable Enterprise Kernel (UEK) using the `grubby` command.


### Ref: 
- [Installing the Unbreakable Kernel](https://www.youtube.com/watch?v=OeFTjC0mqLM)
- [Install Unbreakable Kernel Release 7](https://blogs.oracle.com/scoter/post/uek-7-oracle-linux-8/)
- [UEK Releases List](https://blogs.oracle.com/scoter/post/oracle-linux-and-unbreakable-enterprise-kernel-uek-releases/)
- [Install Unbreakable Linux Kernel](https://linuxhint.com/install-unbreakable-linux-kernel-oracle-8/)





