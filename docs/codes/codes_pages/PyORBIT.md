# PyORBIT

## Short description

PyORBIT is a Python/C++ implementation of the ORBIT (Objective Ring Beam Injection and Tracking) code. PyORBIT software is an open environment for simulations of diverse physical processes related to particle accelerators. The original ORBIT has the Super Code driver shell which is replaced by Python in PyORBIT. At this moment only few capabilities of the original ORBIT are implemented.
Particle tracking can be done in two ways, either with the built-in Teapot tracker module or using a special version of the PTC library. 

## Web resources

 <ul><li> <strong>Source code:</strong> <a href="https://sourceforge.net/projects/py-orbit/" target="_blank">https://sourceforge.net/projects/py-orbit/</a>
</li> <li> <strong>Wiki pages:</strong> <a href="https://sourceforge.net/p/py-orbit/wiki/?source=navbar" target="_blank">https://sourceforge.net/p/py-orbit/wiki/?source=navbar</a>
</li></ul>

## Technical information

 

* __Programming Languages used for implementation:__ 
  
    - Top layer in Python 
    - All computationally intensive routines are implemented in C++ 
  
  
  
* __Parallelization strategy:__ 
  
    - Based on MPI, communication between cores at each space charge interaction node.
  
  
  
* __Operating systems:__ 
  
    - Tested on Linux and MAC OSX (Windows), at CERN used on lxplus
  
  
  
* __Other prerequisites:__ 
  
    - Python 2.6
    - PTC
  
  
  

## Other information

 <ul><li> <strong>Developed by:</strong> A. Shishlo, J. Holmes, S. Cousineau, SNS Oakridge, contributions from CERN
</li> <li> <strong>License:</strong> <a href="https://sourceforge.net/directory/license:mit/" target="_blank">MIT License</a>
</li> <li> <strong>Contact person at CERN:</strong> Hannes Bartosik
</li> <li> <strong>Being actively developed and supported:</strong> Yes
</li></ul> 