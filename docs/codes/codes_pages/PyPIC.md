# PyPIC

## Short description

PyPIC is a python library featuring different 2D Particle in Cell Solvers. It includes advanced features like the accurate modelling of curved boundary using the Shortley-Weller approximation, and improved accuracy based on nested grids. PyPIC it is used to simulate electron cloud and space charge effects within <a class="twikiLink" href="/twiki/bin/view/ABPComputing/PyECLOUD">PyECLOUD</a> and <a class="twikiLink" href="/twiki/bin/view/ABPComputing/PyHEADTAIL">PyHEADTAIL</a>.

## Web resources

 <ul><li> <strong>Source code:</strong> <a href="https://github.com/PyCOMPLETE/PyPIC" target="_blank">https://github.com/PyCOMPLETE/PyPIC</a>
</li> <li> <strong>Additional information:</strong> <a href="https://github.com/PyCOMPLETE/PyPIC/wiki" target="_blank">https://github.com/PyCOMPLETE/PyPIC/wiki</a>
</li></ul>

## Technical information

 <ul><li> <strong>Programming Languages used for implementation:</strong> <ul>
<li> Mainly Python
</li> <li> Computationally intensive routines are implemented in FORTRAN (and linked via f2py) or C/C++ (and linked via cython).
</li></ul>
</li> <li> <strong>Parallelization strategy:</strong> <ul>
<li> None
</li></ul>
</li> <li> <strong>Operating systems:</strong> <ul>
<li> Tested exclusivey on Linux (experience on Ubuntu 12.04 or more recent, and SLC 5 or more recent)
</li></ul>
</li> <li> <strong>Other prerequisites:</strong> <ul>
<li> Python 2.7+ (never tested on Python 3)
</li> <li> Libraries: numpy, cython, f2py. Optionally: pyfftw, <a href="http://faculty.cse.tamu.edu/davis/suitesparse.html" target="_blank">KLU</a> interface).
</li></ul>
</li></ul>

## Other information

 

* __Developed by:__ [Giovanni Iadarola](mailto:giovanni.iadarola@cernNOSPAMPLEASE.ch), Kevin Li, Eleonora Belli, Lotta Mether
* __License:__ CERN Copyright
* __Contact persons:__ [Giovanni Iadarola](mailto:giovanni.iadarola@cernNOSPAMPLEASE.ch)
* __Being actively developed and supported:__ Yes

 
