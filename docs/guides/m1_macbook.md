# M1 Macbook compared to Intel Macbook

*From Hamish Graham*

Useful link to see which MacOs Apps are optmised for M1 Apple Silicon Macbooks: https://isapplesiliconready.com/

### BE-ABP Docker 

I tried to use the docker https://gitlab.cern.ch/abpcomputing/sandbox/be-abp-docker with the M1.

- Docker has not been optimised yet for the M1 chip, at the moment it uses Rosetta 2 to operate

- When running a Docker image, a warning is produced: 
```bash
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
```
- The container will be running but not working properly, for example `tmux` does not work in the container, neither `eos`. 

**In conclusion, I cannot at the moment use the BE-ABP Docker with my M1 Macbook.**

### AFS
- Auristor works on the Macbook M1, however it is a bit more complicated to install vs the Intel Macbook
- This link provides the necessary steps for installing auristor on the Macbook M1: https://blog.auristor.com/2021/01/installing-auristorfs-clients-for-macos.html
- There is a bug for MacOs Big Sur where the Auristor icon does not show a "tick" even if it is running. This bug occurs for M1 and Intel Macbooks running Big Sur.


### Battery Life

- The 13 inch Macbook pro M1 has twice as long of a battery life compared to the Macbook pro Intel, according to Business Insider: https://www.businessinsider.com/macbook-pro-13-2020-m1-vs-macbook-pro-13-2020-intel?r=US&IR=T
- The battery life is estimated to be 20 hours for M1 and 10 hours for Intel (this depends what you are using the computer for, if docker is running  for example, the battery life will be  shorter)
