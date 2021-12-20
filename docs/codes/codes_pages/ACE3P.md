# ACE3P

## Short description

ACE3P is a complete package for electrodynamics simulations in accelerator components, including eigenmode (Omega3P), S-parameters (S3P), Time domain wakefields etc. (T3P), Particle in cell injectors etc. (Pic3P), Tracking charged particles in eigenmode fields for multipacting and dark current (Track3P), and multi-physics for detuning due to thermal expansion from wall losses and mechanical forces (Temp3P).
The solvers run on the external computer clusters at <a href="http://www.nersc.gov/" target="_blank">NERSC



</a>.

For post-processing, the package uses <a href="http://www.paraview.org/" target="_blank">ParaView



</a>, which can be installed through the package manager on most Linux systems, in addition to the "acdtool" post-processor.

For mesh generation, the package uses Trellis or Cubit - please contact the contact persons for more information.
Trellis can be installed on most Linux systems as a .rpm (Fedora, Scientific Linux and other RedHat based systems) or .deb (Debian, Ubuntu, etc.), and can also be installed on most Windows and Mac systems.

## Web resources

* <a href="https://confluence.slac.stanford.edu/display/AdvComp/ACE3P+-+Advanced+Computational+Electromagnetic+Simulation+Suite" target="_blank">ACE3P Homepage at SLAC



</a>

## Technical information

 

* __Programming Languages used for implementation:__ 
  
    - C++ (mainly)
  
  
  
* __Parallelization strategy:__ 
  
    - MPI
  
  
  
* __Operating systems:__ 
  
    - Solvers: Linux
    - ACDTOOL pre- and post-processing: Linux
    - Paraview: Any modern desktop OS
    - Trellis/CUBIT: Any modern desktop OS
  
  
  
* __Other prerequisites:__ 
  
    - You need a NERSC account in order to run the solvers.
  
  
  

## Other information

 <ul><li> <strong>Developed by:</strong> The <a href="mailto:ace3p@slacNOSPAMPLEASE.stanford.edu">SLAC ACD</a> (advanced computations) group
</li> <li> <strong>License:</strong> Unclear, source code private to SLAC
</li> <li> <strong>Contact persons:</strong> <span class="twikiNewLink"><a href="/twiki/bin/edit/ABPComputing/KyrreSjobak?topicparent=ABPComputing.ACE3P;nowysiwyg=1" rel="nofollow" title="this topic does not yet exist; you can create it.">https://phonebook.cern.ch/phonebook/#search/?query=Kyrre+Ness+Sjobaek+BE-ABP-HSS</a></span> (ABP) and <a href="https://phonebook.cern.ch/phonebook/#personDetails/?id=625911" target="_blank">Nikolay Schwerg</a> (in general at CERN)
</li> <li> <strong>Being actively developed and supported:</strong> Yes
</li></ul>

Main.KyrreSjobak - 2016-11-25