# MapClass

## Short description

MapClass and its successor MapClass2 are two codes written in Python and C++ conceived to optimize the non-linear aberrations in beam lines. First and second order momenta of the beam at the end of the given beam line are used as figure of merits. MapClass takes the transfer map from PTC while MapClass2 is equipped with a simple integrator to produce the transfer map up to the desired order.

## Web resources

 <ul><li> <strong>Source code:</strong> <a href="https://github.com/pylhc/MapClass2" target="_blank">https://github.com/pylhc/MapClass2</a>
</li> <li> <strong>MapClass documentation:</strong> <a href="https://cds.cern.ch/record/944769/files/ab-note-2006-017.pdf" target="_blank">https://cds.cern.ch/record/944769/files/ab-note-2006-017.pdf</a>
</li> <li> <strong>MapClass2 documentation:</strong> <a href="https://cds.cern.ch/record/1491228" target="_blank">https://cds.cern.ch/record/1491228</a>
</li> <li> <strong>GPU parallelization:</strong> <a href="http://www.sciencedirect.com/science/article/pii/S1877050916306573" target="_blank">http://www.sciencedirect.com/science/article/pii/S1877050916306573</a>
</li></ul>

## Technical information

 

* __Programming Languages used for implementation:__ 
  
    - Python
    - C++
  
  
  
* __Parallelization strategy:__ 
  
    - GPU in C++
  
  
  
* __Operating systems:__ 
  
    - Linux
  
  
  
* __Other prerequisites:__ 
  
    - Boost libraries for communication between C++ and python
    - GPU optionally
  
  
  

## Other information

 <ul><li> <strong>Developed by:</strong> <a href="http://rtomas.web.cern.ch/rtomas" target="_blank">Rogelio Tomas</a>, Eduardo Marin Lacoma, David Martinez, Alice Rosam, Hector Garcia Morales and Andrea Popescu.
</li> <li> <strong>License:</strong> Open source
</li> <li> <strong>Contact persons:</strong> <a href="http://rtomas.web.cern.ch/rtomas" target="_blank">Rogelio Tomas</a>
</li> <li> <strong>Being actively developed and supported:</strong> Yes
</li></ul> 