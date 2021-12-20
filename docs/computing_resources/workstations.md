# ABP workstations

## Workstations hosted at CERN

The following workstations are avaiable for development and production. 
 - Access is granted based on the use case. 
 - For further information and to get access please contact abp.computing[AT]cern.ch.


| Host name       | CPU                                   | RAM    | GPU                 |
| --------------- | ------------------------------------- | ------ | ------------------- |
| pcbe-abp-gpu001 | AMD Ryzen Threadripper 2970WX 24-Core | 128 GB | 4x Titan V          |
| pcbe-abp-hpc001 | AMD Ryzen Threadripper 3990X 64-Core  | 256 GB | GeForce GTX 1660 Ti |
| pcbe-abp-hpc002 | AMD Ryzen Threadripper 3990X 64-Core  | 256 GB | GeForce GTX 1660 Ti |
| liupsgpu        | 2x Intel Xeon E5-2630 6-core          | 256 GB | 3x Tesla C2075      |

When possible the [CERN batch system (HTCondor)](cernbatch.md) should be used for production studies while these workstation should be used for special cases (e.g. development, performance benchmarking, computations requiring very large amount of memory etc.).

### For administrators

 - A user can change the password by simply typing 
```
passwd
```
 - An administrator can add a user by:
```bash
sudo adduser username
```
 - An administrator can change the password for a user by typing:
```bash
sudo passwd username
```
- An administrator can give sudo rights to an user by typing:
```bash
usermod -aG sudo username
```



## Workstations hosted at INFN-CNAF

GPUs are available also at CNAF (for users having a CNAF HPC account - more info available [here](hpc_cnaf.md)). You can launch GPU jobs interactively with the following steps:

 1. Connect with SSH into the login server: ```bastion.cnaf.infn.it```;  
 2. Connect wiht SSH to the node that has the 4x Nvidia Tesla V100 GPUs: ```hpc-201-11-35```; 
 3. Enable newer versions of gcc, cmake etc. with ```scl enable devtoolset-7 bash```
