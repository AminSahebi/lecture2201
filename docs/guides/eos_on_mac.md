(from an codiMD page of Ilias, https://codimd.web.cern.ch/s/vorpxehxj)

# Using EOS in my Mac

To effectively use my mac for LHC data analysis, I need to have access to EOS repositories: 

- my personal one under `/eos/home-i`
- some project repositories in `/eos/project-l`

From CERN IT there are two solutions proposed: 

- use the CERNBOX client
- mount directly the EOS volumes

I tried and have both running, below my experience from using them.

## Using the CERNBOX client

The installation is straightforward, you can download the package and install it. Then you can configure the account and add folders to synchronize.

### pros
You can have multiple folders synchronized with your Mac. Can be user folders, projects or other shared folders you have access to with the declared account. 

For each folder you can select which sub-folders you want to add to the syncronization.

The program works well and I've very rarely see it crashing or not being able to do the synchronization. 

It is smart and can ignore certain types of files - there is an _Ignored Files_ list that you can edit.

### cons

- Not reliable synchronization:
    - sometimes takes long to trigger the synchronization,
    - I've observed that sometimes some files are not included in the first synch loop,
    - Very often "small" changes to files are not noticed.

    Eventually the synchronization works but is not immediate. For example editing locally the files using a smart editor (like VsCODE) and run my scripts in SWAN becomes a frustrating process.
    
-  No dynamic synchronization: As user I have to select which files to synchronize and since my space in EOS can be as big as 1TB while in my Mac I have only 256GBytes, I need to constantly select and update the folders I synchronize. 
    - A better solution would have been a dynamic allocation of CERNBOX space in my Mac where files are included or removed upon use, as other programs do. 
    - This would also offer an access to the EOS directory structure which presently is limited to the ones selected for synchronization.

## Using FUSE for direct mount

I followed the instructions found in some of the CERN IT pages. 

The installation is relatively easy:

- install OSXFUSE from [osxfuse.github.io](https://osxfuse.github.io/)
- make a directory to be the local mount point for EOS 
    - can be either `/eos` or as in my case `/User/ilias/eos`
    
- then get the kerberos token using: `kinit myuser@CERN.CH`
- define the environment variables to EOS:

```bash
export EOS_MGM_URL=root://eoshome-i.cern.ch
```

or 

```bash
export EOS_MGM_URL=root://eosproject-l.cern.ch
```

- finally do the mount : `eos fuse mount /Users/ilias/eos`.
    
That's it! 
    
In case the mount did not work you can restart it doing:

```bash
killall eosd
eos fuse umount /User/ilias/eos
```

and then try mounting it again.
    
### pros

- Straightforward procedure, typically works 
- You don't have to select directories to synchronize
- Full access to the directory tree
- Fast reaction to changes - the files become almost immediately available to remote
- Could access the EOS directories from my editor (vsCODE).

### cons

- It seems I have to redo the mount once the kerberos tokens expire
- I dit not manage to mount both a user directory and a project EOS space.


Ilias suggested in the mattermost channel  https://mattermost.web.cern.ch/abpcomputing/pl/5p54ieirofdxf8caejuy64emuy to use the following script 
```bash
#!/bin/bash
#
# Script to initialize and mount the EOS
#
# (c) Ilias Efthymiopoulos - Feb 2020
#
# Arguments : [1]  my CERN password
#
#
# -- get access to EOS from previously stored kerberos password

kinit -kt ~/.keytab efthymio@CERN.CH

export EOS_MGM_URL=root://eoshome-e.cern.ch
export EOS_FUSE_MGM_ALIAS=eoshome-e.cern.ch
export EOS_FUSE_MOUNTDIR=/Users/iliasefthymiopoulos/eoshome-e

eos fuse mount  /Users/iliasefthymiopoulos/eoshome-e/

export EOS_MGM_URL=root://eosproject-l.cern.ch
export EOS_FUSE_MGM_ALIAS=eosproject-l.cern.ch
export EOS_FUSE_MOUNTDIR=/Users/iliasefthymiopoulos/eosproject-l

eos fuse mount /Users/iliasefthymiopoulos/eosproject-l

# --- define alias for unmount

alias umounteos='function _umnteos()
{
 killall eosd; eos fuse umount /Users/iliasefthymiopoulos/$1
}; _umnteos'
``` 

and Joschua proposed to use also a function approach to simplify it 

```bash
function umounteos()
{
 killall eosd; eos fuse umount /Users/iliasefthymiopoulos/eos$1
};

alias umounteosall='umounteos project-l; umounteos home-e'
``` 

or even 
```bash
function mounteos()
{
  export EOS_MGM_URL=root://eos$1.cern.ch
  export EOS_FUSE_MGM_ALIAS=eos$1.cern.ch
  export EOS_FUSE_MOUNTDIR=/Users/iliasefthymiopoulos/eos$1
  eos fuse mount /Users/iliasefthymiopoulos/eos$1
};

alias mounteosall='mounteos project-l; mounteos home-e'
```
    
