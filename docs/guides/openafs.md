# Installation of OpenAFS

## Installation on Debian/Ubuntu

*(prepared by V. Olsen - 2017-12-06)*

Tested on Debian Stretch

### Install Packages 

`` $ sudo apt install openafs-client openafs-modules-dkms openafs-krb5 krb5-user krb5-config ``

### Issue with obsolete packages

*(R. De Maria)*

Presently (Apr 2021) these packages installed above are obsolete and are incompatible with AFS at CERN (see [Mattermost discussion](https://mattermost.web.cern.ch/abpcomputing/pl/z871mq1agtdgixynbg3ahtj7na). The problem can be solved by downloading a more recent version from the OpenAFS team.

In **Ubuntu 18.04** this can be done as follows:
```bash
sudo apt install init-system-helpers/bionic-backports
sudo add-apt-repository ppa:openafs/stable
sudo apt-get update
sudo apt-get upgrade
```

In  **UBUNTU 20.04.1** it can be done as follows:

```bash
sudo add-apt-repository ppa:openafs/stable
sudo apt-get update
sudo apt-get upgrade
```


###  Configure AFS and Kerberos 

__1. Use "cern.ch" as default AFS cell__

`` $ echo "cern.ch" | sudo tee /etc/openafs/ThisCell ``

__2. Set up Kerberos authentication__

Add the following lines to file `` /etc/krb5.conf ``:

```bash
# settings for CERN.CH realm are taken from file
#   lxplus.cern.ch:/etc/krb5.conf

[libdefaults]
  default_realm = CERN.CH

[realms]
  CERN.CH = {
  default_domain = cern.ch
  kpasswd_server = cerndc.cern.ch
  admin_server = cerndc.cern.ch
  kdc = cerndc.cern.ch
  }

[domain_realm]
  cern.ch = CERN.CH
  .cern.ch = CERN.CH
```

__3. Restart OpenAFS client__

On Ubuntu 16.04 and above:

`` $ sudo systemctl restart openafs-client.service ``

On older versions:

`` $ sudo service openafs-client restart ``

__4. Login (optional, only needed to access protected paths):__

```bash
$ kinit $LOGNAME@CERN.CH     # get kerberos ticket
$ aklog                      # login to AFS cell
```

###  Miscellanea 

Configuration steps 1) and 2) can be done with:

```bash
$ sudo dpkg-reconfigure openafs-client
$ sudo dpkg-reconfigure krb5-config
```

It might be useful to set-up a crontab job (e.g. every 6h) to automatically renew the kerberos token:

```bash
0    -/6    -    -    - kinit -R ; aklog -c cern.ch -k CERN.CH
```

Pay attention that `` kinit -R `` (i.e. renew existing token) won't require any password to be typed in; on the other hand, a token can be renew for a maximum of 5d after its generation, hence a `` kinit `` (with password) is needed. Anyway, if `` kinit `` is issued on Monday morning, so that for the rest of the week you don't have to bother with that.

__Reference:__ <a href="http://akorneev.web.cern.ch/akorneev/howto/openafs.txt" target="_blank">http://akorneev.web.cern.ch/akorneev/howto/openafs.txt</a>



### Possible problems on Ubuntu 

If you have a recent Ubuntu installation, the above procedure might not entirely work as there could be a kernel incompatibility with the latest openafs. This is shown if you try `` aklog ``: it will then give the error

`` aklog: a pioctl failed while obtaining tokens for cell cern.ch ``

Furthermore, also a query of the openafs service with

`` $ sudo systemctl status openafs-client.service ``

will give errors:

```bash
openafs-client-precheck[2963]: modprobe: FATAL: Module openafs not found in directory /lib/modules/4.10.
openafs-client-precheck[2963]: Failed to load openafs.ko.  Does it need to be built?
```

I found a solution that worked for me, by adding a specific repository for openafs:

```bash
$ sudo apt-get purge openafs-client
$ sudo add-apt-repository ppa:openafs/stable
$ sudo apt-get update
$ sudo apt install openafs-client
$ sudo apt install --reinstall openafs-modules-dkms
```

Now we need to restart the service:

```bash
$ sudo systemctl stop openafs-client.service
$ kinit username@CERN.CH
$ sudo systemctl start openafs-client.service
```

You can check that the service is running as it should:

`` $ sudo systemctl status openafs-client.service ``

No more errors! Continue as before, `` aklog `` and possibly a crontab for `` kinit ``.

__Note:__ It may be enough to just run

```bash
$ sudo dpkg-reconfigure openafs-modules-dkms
```

### Within Windows Subsystem Linux (WSL)

The same error as above can occur in WSL, and while the solution is also to 
reconfigure the kernel modules, one needs to download the kernel source first 
and perform some of the build steps.

A guide has been written in [this gist from Joschua](https://gist.github.com/JoschD/194b3f6c6fcc408684a481fd4a2ff4e5).

## Installation on MacOS

(prepared by F. Van Der Veken - 2020-04-01)


Mounting AFS on macOS can be a bit messy and is very poorly supported. In general it is preferred to access AFS via LxPlus and move your files to your local computer with `` scp ``. If you want to try mounting AFS anyway, there are two ways to proceed: using FUSE, or using OpenAFS.

Tested on macOS Sierra (10.12.6) and Catalina (10.15.4).

###  Using OpenAFS 

So far, it is not possible to install OpenAFS on macOS High Sierra (10.13). More importantly, when upgrading macOS to version 10.13 it is extremely important to __deinstall__ OpenAFS completely before making the upgrade, to avoid a never-ending loop of kernel-panics which are due to the AFS local cache being converted to the new Apple File System (APFS).

Installers can be downloaded from:

 - macOS 10.12: <a href="http://download.sinenomine.net/openafs/bins/1.6.20/macos-10.12/" target="_blank">http://download.sinenomine.net/openafs/bins/1.6.20/macos-10.12/</a>
 - macOS 10.11: <a href="http://download.sinenomine.net/openafs/bins/1.6.20/macos-10.11/" target="_blank">http://download.sinenomine.net/openafs/bins/1.6.20/macos-10.11/</a>

These are not officially supported, but third-party binaries provided by Sine Nomine (more information at <a href="https://wiki.openafs.org/archive/BinaryThirdParty/" target="_blank">https://wiki.openafs.org/archive/BinaryThirdParty/</a>).
Older versions of macOS are officially supported and can be downloaded from <a href="http://www.openafs.org/macos.html" target="_blank">http://www.openafs.org/macos.html</a>.

__Update__
Auristor now has installers for later versions of macOS:

- <a href="https://www.auristor.com/openafs/client-installer/" target="_blank">https://www.auristor.com/openafs/client-installer/</a>


This seems to work on Catalina, however, do __not__ upgrade macOS without deinstalling OpenAFS first (which is then named `` Auristor ``) to avoid disk crashes.

During the installation, when asked for the local cell this is `` cern.ch ``. Give the installation permissions in `` System Preferences `` when needed. After installation, a reboot is needed. Luckily macOS comes with Kerberos pre-installed, so that's all. If you want to access protected paths, you'll have to login with Kerberos:

```bash
$ kinit user@CERN.CH     # get kerberos ticket
$ aklog                  # login to AFS cell
```

There is an OpenAFS/Auristor preference pane in your system preferences in which you can change the cell (not needed), auto-renew Kerberos tickets, and let OpenAFS start at boot.

###  Using FUSE and SSHFS 

FUSE for mac and the SSHFS plugin can be downloaded from <a href="http://osxfuse.github.com" target="_blank">http://osxfuse.github.com</a>. 
Alternatively, both can be installed using `` macports ``:

`` $ sudo port install osxfuse ; sudo port install sshfs ``

Verifying if OSXFUSE is installed can be done in the preferences pane, while checking if SSHFS is installed can be done by typing

`` $ sshfs&nbsp; -h ``

in the terminal. To mount the filesystem we have first to create a folder to hold its location. Normally all disks are mounted in `` /Volumes/ ``, however, from macOS 10.12 one needs to have root permissions to write to this location. But this is not really a problem, as a volume can be mounted at any location, so your home folder will do fine. Mounting the volume is then done by:

```bash
$ mkdir ~/DISK_NAME
$ sshfs USER@lxplus.cern.ch:AFSPATH  ~/DISK_NAME -ovolname=DISK_NAME
```

This can be simplified by making an alias in `` .bash_profile ``. Unmounting the volume is done in the usual way in Finder (clicking the unmount icon to the right of the volume). If for some reason unmounting does not work, the volume can be forcefully ejected by typing

`` $ diskutil unmountDisk force ~/DISK_NAME ``

If you want to automatically mount the drive on startup, have a look at:

<a href="http://superuser.com/questions/134140/mount-an-sshfs-via-macfuse-at-boot" target="_blank">http://superuser.com/questions/134140/mount-an-sshfs-via-macfuse-at-boot



</a>.


