# MAD-X

## Short description

MAD-X is an application used world-wide with a long history going back to the 80's in the field of high energy beam physics (i.e. MAD8, MAD9, MADX). It is an all-in-one application with its own scripting language used to design, simulate and optimize particle accelerators: lattice description, machine survey, single particles 6D tracking, optics modeling, beam simulation &amp; analysis, machine optimisation, errors handling, orbit correction, aperture margin and emittance equilibrium.

## Web resources

The <a href="http://cern.ch/madx" target="_self">MAD-X website</a> provides access to information, documentation (PDF), releases (binaries), source code (tarball), e-groups, versioning system (SVN), issues tracking system (Trac), and more... The user manual can be downloaded <a href="http://cern.ch/madx/releases/last-dev/madxuguide.pdf" target="_self">here</a>.

## Technical information

 

* __Programming Languages used for implementation:__ 
  
    - Fortran 77, Fortran 90, C, C++ for a total of about 180000 lines of codes.
    - MAD-X scripting language is garbage collected (based on GC Boehm).
    - Build system entirely done with make.
    - Tested every night on server equiped with VMs for supported OS and architectures.
  
  
  
* __Parallelization strategy:__ 
  
    - Particle tracking (track command) is parallelized with OpenMP if compiled with the proper flags. This is not the default as it does not bring much speed gain (old-style Fortran 77).
    - Compilers vectorize strings, arrays, vectors and matrices computations, and perform loop unrolling plus many other common optimizations done by modern compilers on modern CPU/FPU.
  
  
  
* __Operating systems:__ 
  
    - Supported on MAC OSX (10.8 or above), Windows (7 or above), Linux (static binary).
    - 32 bit and 64 bit architectures are avalaible.
  
  
  
* __Other prerequisites:__ 
  
    - No libraries. Scatter plots use gnuplot.
  
  
  

## Other information

 

* __Delivery:__ 2-3 releases per year.
* __Developed by:__ Main developpers were H. Grote (MAD8, MADX) and C. Iselin (MAD8, MAD9) in the 90's. Many people contributed to the project since then, see the contributors section on the website.
* __License:__ Open source software under CERN Copyrights.
* __Contact persons:__ mad at cern dot ch (see the website for the persons members of the MAD team).
* __Being actively developed and supported:__ Yes.

 