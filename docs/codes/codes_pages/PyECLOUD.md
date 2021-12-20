# PyECLOUD

## Short description

PyECLOUD is a 2D macro-particle code for the simulation of electron cloud effects in particle accelerators. It can be used for two purposes: 

* in stand-alone mode for the simulation of the e-cloud buildup at a certain section of an accelerator (it this case the beam is rigid and feels no effect from from the cloud);
* in combination with the <a class="twikiLink" href="/twiki/bin/view/ABPComputing/PyHEADTAIL">PyHEADTAIL</a> code for the simulation of the e-cloud effects on the beam dynamics. 

## Web resources

**Git repository:** https://github.com/PyCOMPLETE/PyECLOUD

**Getting started guides:** [Installation](https://github.com/PyCOMPLETE/PyECLOUD/wiki/How-to-install-PyECLOUD), [Usage](https://github.com/PyCOMPLETE/PyECLOUD/wiki#examples-and-tutorials)

**Examples:** Available in Getting-started guides.

**Documentation:**: https://github.com/PyCOMPLETE/PyECLOUD/wiki


## Technical information

 

* __Programming Languages used for implementation:__ 
  
    - Mainly Python.
    - Computationally intensive routines are implemented in FORTRAN (and linked via f2py) or C (and linked via cython).
  
  
  
* __Parallelization strategy:__ 
  
    - PyECLOUD-PyHEADTAIL simulations can be paralleled using the <a class="twikiLink" href="/twiki/bin/view/ABPComputing/PyPARIS">PyPARIS</a> layer.
  
  
  
* __Operating systems:__ 
  
    - tested exclusively on Linux.
  
  
  
* __Other prerequisites:__ 
  
    - Python 3.6+
    - Libraries: numpy, scipy, cython, h5py
  
  
  

## Other information

* __Developed by:__ [Giovanni Iadarola](mailto:giovanni.iadarola@cernNOSPAMPLEASE.ch)
* __License:__ CERN Copyright
* __Contact persons:__ Giovanni Iadarola

 