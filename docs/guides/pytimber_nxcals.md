# PyTIMBER and NXCALS

As of 1 Feb 2021 the old accelerator logging system (CALS) has been made unaccessible and has been replaced by the new NXCALS system.

A quick-start guide to NXCALS is available at this address:  
http://nxcals-docs.web.cern.ch/current/user-guide/data-access/quickstart/ 

To get access to the data you need to request access using this [CCDE form](https://ccde.cern.ch/dashboard/loggingAccessRequest) or writing an e-mail to the logging support (acc-logging-support[AT]cern.ch)

The [pytimber package](../codes/codes_pages/PyTimber.md) has been adapted to work with the new system.

Please note that the latest version of PyTIMBER is not anymore made available on PyPI but needs to be retrieved from the internal CERN package index. A working setup could be obtained as follows (starting from a fresh miniconda installation):

```bash
# Get, install and activate miniconda
 cd /afs/cern.ch/work/l/lhcecld
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p /afs/cern.ch/work/l/lhcecld/miniconda
source miniconda/bin/activate

# Get standard packages 
# (to have all spark functionalities pandas needs to be installed before pytimber)
pip install numpy scipy matplotlib ipython pandas

# Change python package index to CERN index
pip install git+https://gitlab.cern.ch/acc-co/devops/python/acc-py-pip-config.git

# Install pytimber
pip install pytimber

# Change python package index back to default
pip uninstall acc-py-pip-config
```

A pytimber object accessing NXCALS can be instantiated by:
```python
ldb = pytimber.LoggingDB(source="nxcals") 
```