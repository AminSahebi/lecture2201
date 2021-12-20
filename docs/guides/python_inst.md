# Install and configure python

*(Prepared by G. Iadarola)*

## Introduction

Some operative systems come equipped with a Python installation. Even in this case, it is often convenient to install a user-managed python environment to have full control of the configuration. 

In this page we describe two methods:

   1. [Setup of a miniconda installation](#install-and-configure-miniconda) (easier)
   2. [Compile and configure python from source code](#compile-and-configure-python-from-source-code) (necessary when thw installation needs to be compiled with a specific compiler, for example to be used with MPI).

None of the two methods requires admin rights.

## Install and configure miniconda

**Step 1:** Download and install the most recent version of Miniconda (from [here](https://repo.anaconda.com/miniconda/))
Something like:
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```
(Provide the path for the installation, in my case /home/giadarol/Desktop/PyFRIENDS_python3/miniconda3
You will be asked whether you want to make this miniconda the default python installation for your computer (this is your choice :-) )

**Step 2:** Activate the miniconda installation
```
source /home/giadarol/Desktop/PyFRIENDS_python3/miniconda3/bin/activate
```

**Step 2a (optional):** Install compilers

To install packages that need to compile code (e.g. PyECLOUD, PyHEADTAIL or Xsuite) you need C and/or FORTRAN compilers. If you don't have compilers available on your system you can install them using conda as discussed in [this guide](https://conda.io/projects/conda-build/en/latest/resources/compiler-tools.html).

For example on Linux you can install C, C++ and FORTRAN compilers by:
```bash
conda install gcc_linux-64
conda install gxx_linux-64
conda install gfortran_linux-64
```

while on MAC you can use:
```bash
conda install clang_osx-64
conda install clangxx_osx-64
conda install gfortran_osx-64
```

**Step 3:** Install useful packages
```
pip install numpy scipy matplotlib pandas ipython
```

Your python installation is ready to be used!

### Virtual environments

Virtual environments can be useful to try different package versions and for developments. A detailed guide to conda's virtual environments can be found here:

https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands



## Compile and configure python from source code


**Step 1:** We move to the folder where we want to place our installation:

    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3

**Step 2:** We download from the [python website](https://www.python.org/downloads/source/), compile and install the latest version of python 3:
```    
mkdir python_src
cd python_src
wget https://www.python.org/ftp/python/3.8.0/Python-3.8.0.tar.xz
tar xvf Python-3.8.0.tar.xz
cd Python-3.8.0
./configure --prefix=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python3
make
make install
``` 

**Possible issues with ssl:**
In order to be able to use pip at a later stage, python needs to be compiled with ssl support. Please check that this is the case:

    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python3/bin/python3
    import ssl

In case this gives an exception, please install ssl library and recompile python (in Ubuntu this can be done by sudo apt install libssl-dev).
Information on how to get the ssl library without admin rights can be font [here](https://chrisbebek.com/blog/?p=97).

**Possible issue with ctypes and libffi:**
Check that ctypes is working (will be required for several reasons afterwards):

```
/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python3/bin/python3
import ctypes
```

If you get an error, it is because the ffi library is not installed. 
You can download and install the library as follows:
```
cd /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python_src
wget ftp://sourceware.org/pub/libffi/libffi-3.3.tar.gz
tar -xvf libffi-3.3.tar.gz
cd libffi-3.3/
mkdir /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi
./configure --prefix=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi
make
make install
```

The library location needs to be added to our library path:
```
export LD_LIBRARY_PATH=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi/lib64:$LD_LIBRARY_PATH
```

The python compilation needs some extra information:
```
export PKG_CONFIG_PATH=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi/lib/pkgconfig
./configure --prefix=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python3 LDFLAGS="-L/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi/lib/../lib64" CFLAGS="-I/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi/include"
```
The continue as normal:
```
make
make install
```
 

**Possible issues with sqlite3:**
In order to be able to use jupyter notebooks at a later stage, python needs to be compiled with sqlite3 support. Please check that this is the case:

    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python3/bin/python3
    import sqlite3

In case this gives an exception, please install sqlite library and recompile python (in Ubuntu this can be done by sudo apt install libsqlite3-dev).

**Possible issues with tk:**
In order to be able to use ipython --pylab at a later stage, python needs to be compiled with tk support. Please check that this is the case:

    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_p3/python3/bin/python3
    import _tkinter

In case this gives an exception, please install tk library and recompile python (in Ubuntu this can be done by sudo apt install tklib; sudo apt install tk-dev ).


**Step 3:** We create a virtual environment

    cd /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3
    mkdir venvs
    cd venvs
    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python3/bin/python3 -m venv py3
             

**Step 4:** We activate the virtual environment
```
source /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/venvs/py3/bin/activate
```

If we type:
    
    which python
we get:

    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/venvs/py3/bin/python

**Step 4b**: In case libffi needed to be compiled, you should add libffi path also in activate script

To do this, edit the activate script:
```
nano /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/venvs/py3/bin/activate
```

Add after the last line:
```
export LD_LIBRARY_PATH=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/libffi/lib64:$LD_LIBRARY_PATH
```

**Step 6**: We use pip to install the python modules that we need
 
     pip install numpy scipy cython ipython matplotlib

**Steps 5 and 6 are required only to run parallel simulations using MPI.**

**Step 5 - Check that MPI is available:**

You can use the following commands to check that an MPI installation is available
```
which mpicc
which mpiexec
```
In case it is not, please activate an MPI installation (Step 5.a) or install a new MPI installation (Step 5.b).

**Step 5.a - Activate MPI:**

On certain machines an MPI installation can be activated using ```module load``` (it is the case for CERN lxplus and CERN HPC cluster) or ```mpi_selector``` (it is the case for the INFN-CNAF cluster)

**Step 5.b - Install MPI:**

If we do not have an MPI installation we need to get one:

     cd /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/python_src
     wget https://www.open-mpi.org/software/ompi/v1.10/downloads/openmpi-1.10.2.tar.bz2
     tar jxf openmpi-1.10.2.tar.bz2
     cd openmpi-1.10.2
    ./configure --prefix=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/openmpi
     make all install

We set the environment variable for the MPI compiler (pip will use the compiler pointed by your MPICC variable to compile mpi4py):

    export MPICC=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/openmpi/bin/mpicc

At this point be careful not to have other MPI paths in your environment (for example set in your .bashrc)

**Step 6:** Install mpi4py

    pip install mpi4py

_Important:_ Python jobs using mpi4py must be run with the mpiexec corresponding to the MPI compiler that has been used. In our case:

    /afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/openmpi/bin/mpiexec

Of course we can add the folder to our PATH or create a shortcut.


**Step 7:** Install h5py (if you need it)

If you don't need parallel hdf5 I/O you can just:
   
    pip install h5py

Instead, in case you need parallel hdf5 I/O and you want to compile your own hdf5 library (N.B. this is NOT needed for PyPARIS simulations):

    wget https://support.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.10.5.tar.bz2
    tar jxf hdf5-1.10.5.tar.bz2
    cd hdf5-1.10.5/
    ./configure --prefix=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/hdf5lib --enable-parallel --enable-shared
    make
    make install
    CC=/usr/bin/mpicc HDF5_MPI="ON" HDF5_DIR=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/hdf5lib pip install --no-binary=h5py h5py

In case you don't have libhdf5 installed, but you don't need parallel IO (PyPARIS case), you can:

    wget https://support.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.10.5.tar.bz2
    tar jxf hdf5-1.10.5.tar.bz2
    cd hdf5-1.10.5/
    ./configure --prefix=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/hdf5lib --enable-shared
    make
    make install
    HDF5_DIR=/afs/cern.ch/work/g/giadarol/sim_workspace_mpi_py3/hdf5lib pip install --no-binary=h5py h5py


A couple of references that helped with this task:

[1] [[https://www.open-mpi.org/faq/?category=building#easy-build]]

[2] [[http://stackoverflow.com/questions/5506110/is-it-possible-to-install-another-version-of-python-to-virtualenv]]

[3] [[https://chrisbebek.com/blog/?p=97]]