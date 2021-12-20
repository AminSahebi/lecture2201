# Code-specific objectives and activities

### *MAD-X*

*Involved persons: Tobias, Laurent*

 - Improve support for misaligned and overlapping elements
 - Support cpymad for python workflows
 - Improve save/reload capabilities (full mad-x state)

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

??? warning "Pending bug-fixes (required for ABP activities)"
    - Calculation of crabcavity R and T matrix not correct in MADX and PTC. 
        - Required to include crab cavities in the HL-LHC sequence!
        - Some functionality duplication between crabcavity and RFmultipole. We might want to  to port all the functionality in RFMultipole and call it from CrabCavity for backward compatibility.
        - Related GitHub issue [here](https://github.com/MethodicalAcceleratorDesign/MAD-X/issues/981)
    - Current master segfaults on a long hl-lhc script when compiled with 'make'
        - Related GitHub issue [here](https://github.com/MethodicalAcceleratorDesign/MAD-X/issues/982)

### *MAD-NG*

*Involved persons: Laurent*

 - Focus will be on building know how and develop tools for non-linear normal forms analysis and advanced tracking maps (see [recommendations of MAD-NG review](https://indico.cern.ch/event/991905/attachments/2178071/)).
    - The long-term goal is to match the capabilities and performance of PTC and possibly do better.
 -  Provide python interface for integration with other ABP and operation tools (LSA, pyheadtail, sixtracklib, pymask)  

??? note "Milestones and timeline"
    - See [presentation at MAD-NG forum](https://indico.cern.ch/event/991905/contributions/4172235)

## Tracking tools

### *Xtrack*

[NAME IS TEMPORARY]

*Involved people: Riccardo, Martin, Kostas, Frederik, Tobias, Gianni, Roderik*

 - Based on the sixtracklib experience, build a modular library (Xtrack) that performs tracking on CPUs and GPUs
 - Requirements:
    1. Possibility of working in combination with other tools (PyHEADTAIL, PyPIC) for collective effects studies (instabilities, space-charge, e-cloud)
    2. Should be able to replace Sixtrack for conventional single-particle studies
    3. Run efficiently with HTCondor and BOINC (requires numerical reproducibility)
    4. Adopt design choices that facilitate future maintenance and development, as well as adaptation to new technologies (e.g. GPU standards) -> keep the code slim
    5. Allow the integration of advanced collimation capabilities (advanced aperture models, scattering, with FLUKA, tracking of fragments)
    6. Be extendable to model lepton rings.

??? note "Design choices"
    - To keep a slim and flexible code, we choose to manage the memory and the simulation through python.
    - We will use pyopencl to build a first version, then possibly extend to cupy and numba-cuda.
    - Some modifications in [PyPIC](#PyPIC) and [PyHEADTAIL](#PyHEADTAIL) might be necessary.
    - Description of the particles ensemble might be moved to a separate library ([Xpart](#Xpart)) and shared with PyHEADTAIL.

??? note "Short-term tasks"
    - Build a first skeleton version.
    - Collect a set of examples representative of all the use-cases, to make sure that the design covers all needs:
        - Examples for DA and lifetime studies already available
        - We need a set of examples  illustrating che collimation us-cases (using the SixTrack)
        - We need an example for the space charge studies (sixtracklib, pyheadtail, pypic)

??? note "Milestones and timeline"
    - Skeleton code with main features Feb 2021
    - Collection of use-cases (e.g. space-charge, collimation) to be done in Q1-Q2 2021
    - By end of 2021 ABP-INC should be able to migrate their studies:
         - requires all features available in sixtracklib 1.0, interface with PyPIC, dynamic elements (noise)

    - Other features (aiming at matching SixTrack capabilities that we need to retain): 2022
         - For collimation features, the timescale will be defined only after reviewing all the use cases (might need to go beyond 2022, depending on allocated resources).


### *Xpart*

[NAME IS TEMPORARY]

*Involved persons: Guido, Foteini, Kostas, Lotta*

  - Concentrate in a single library tools for the generation of particle ensembles. Capabilities are presently scattered over:
     - SixDesk
     - pysixdesk
     - sixtrack (recent work by Riccardo, Tobias and co.)
     - pysixtrack (Kostas' code)
     - PyHEADTAIL (advanced longitudinal matching)
  - This library should define a general and flexible particle description that can be imported and used in PyHEADTAIL, in the new tracking library and for other usages.
  - Probably we can use PyHEADTAIL's Particles class as a starting point.
  - Remember that masked access needs to be available for bunch slicing.
  - Extraction of statistical properties (average position, r.m.s. sizes, optical functions, emittances) should be implemented (ported from PyHEADTAIL).

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021


### *SixDesk* 

*Involved persons: Guido, Frederik*

 - Restructure the tool to ease maintenance and further development (re-use as much as possible the [pysixdesk](https://github.com/SixTrack/pysixdesk) code).
 - Integrate new developments (pymask, Xtrack)
 - Improve usage flexibility.
 - Explore the usage of containers ([singularity](https://sylabs.io/singularity/) or [docker](https://www.docker.com)) on BOINC for more flexible simulations (e.g. including python)
  - Move generation of particles distribution to a separate library usable for other applications (synergy with PyHEADTAIL).

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021-2022

??? note "Updates"
    - An example with some python helpers (prepared by Sofia) can be found [here](https://github.com/sterbini/sixdesk_example)
    - A possible functionality breakdown can be found [here](https://codimd.web.cern.ch/s/L8ANqV-Rd), together with some notes.


### *mask / pymask*

*Involved persons: Guido, Sofia Kostoglou, NLD fellow (with Massimo)*

 - Extend to ions
 - Strengthen automatic and interactive checks on error-routines, optics, knobs, etc.
 - Validate beam 4 implementation.
 - Plan transition to pymask for all applications.

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021-2022
           - Ion extension by Spring
           - Validation of beam 4 and first set of checks by end-2021 

??? warning "Pending bug-fixes (required for ABP activities)"
    - Presently not working with machine imperfections! (Frederik is on it)

## Tools for collective effects

### *COMBI* 

*Involved persons: Xavier, Sondre*

- Port to python the top-level layer of COMBI that manages the interaction schedule, in order to profit from other libraries having a python interface (PyHEADTAIL, Xtrack)
    - Build a ”proof-of-principle” code to test and validate the main functionalities (e.g. asynchronous MPI calls)
    - Then move to a well structured python library (reusing as much as possible modules from PyHEADTAIL)
    - Expose to python features of COMBI that are not already available in other python packages (e.g. BTF, noise modeling).

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021-2022
           - ”proof-of-principle” code with main functionalities in 2021


### *PyHEADTAIL* 

*Involved persons: Lotta*

 - Build a solid set of examples and tests covering the entire library
 - Improve documentation, introduce a simple “Getting started guide”
 - Finalize merge into master of the coupled-bunch branch
 - Generation and description of particles ensembles should be moved to a separated library [Xpart](#Xpart) (shared with the [Xtrack](#Xtrack) tracking library)
 - Integrate with Xtrack library for advanced non-linear tracking.
 - Introduce multithread CPU parallelization (numba, or cython), required for performance in COMBI-like simulations
 - Review, document and update GPU features (need to stay compatible with [Xtrack](#Xtrack)).
 - Integrate coasting beam capabilities (development from Nicolo').

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021-2022
           - merge of coupled-bunch branch, example set, and documentation review to be done in 2021.
           - ESRF would like to use the coupled bunch mode in python 3 (needs merged version). Tentatively this should be possible in June.

### *PyPIC (becomes Xfields)*

*Involved persons: Gianni*

 - Restructure the library to better integrate CPU-based FD solvers and GPU-based FFT solvers.
 - Foresee combined usage with [Xtrack](Xtrack) for space-charge simulations.
 - Move to standard python-package structure (pip installable).

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

??? note "Design ideas and constraints"
    Details here: https://github.com/giadarol/PyPIC/issues/1

??? note "Updates"
    - Development being done in this GitHub branch: https://github.com/giadarol/PyPIC/tree/reorganize
        - Started sketching the structure
    - Space-charge equations collected at: https://github.com/giadarol/PyPIC/tree/reorganize/doc

### *PyECLOUD, PyPARIS*

*Involved persons: Gianni, Lotta*

 - Move to standard python-package structure (pip installable).

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021


### *DELPHI*

*Involved persons: Nicolas, Gianni, Sebastien, Sofia Johannesson*

 - Restructure and simplify the code (more flexible interface, more pythonic, easier to bypass convergence tests, etc.), 
 - Move to standard python-package structure (pip installable)
 - Integrate different matrix calculation from temporary eDELPHI package (to handle e-cloud, detuning impedances, short wakes)
 - Improve integration with PySSD

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

??? note "Design constraints and first ideas (2020-01-15)"
    Requirements:
    
     - We need the possibility of enlarging the matrix for convergence checks
     - We should be able to reuse quantities when possible (e.g. the full matrix for "intensity" scans or different synchrotron tunes, or parts for the calculation). Some ingredients break the reusability, the code should check automatically.

    Design ideas:

     - Make a base "coupling matrix" class with the methods that are shared (e.g. ```compute_complex_tune_shifts(rescale_factors)```). Such a base class will depend on the beam distribution and on the chosen base functions but not on the description of the collective effects forces.
     - Then we make children classes with specialized implementations for the different descriptions of the coherent forces: impedance sum from DELPHI, sine responses from eDELPHI, but also Dirac-delta response, specialized versions for fast-decaying wakes and resonators.
     - We should be able to combine matrices.
     - We could try to express all cases (or most cases) in general form like:
     $$
     {\Large
     M_{l,m,l',m'} = K_\text{coh}\sum_n A_n R_{l,m,n} \tilde{R}_{l',m',n}}
     $$
     The different child classes will have different ways of computing $\Large A_n$ (which is the impedance in the case of Delphi), $\Large R_{l,m,n}$, $\Large \tilde{R}_{l',m',n}$. We would keep these quantities in memory to test different matrix truncations...
     - Using python memorizers might help, but we would lose the possibility of working with numpy arrays, which could impact performance.

??? note "Updates"

     - Working in in https://gitlab.cern.ch/IRIS/DELPHI/-/tree/merged_eDELPHI
     - The Harmonic Response Matrix from eDELPHI has been ported and tested.
         - Need to move generic functionalities to base class (done to some extent).
         - Need to separate the part coming from detuning with longitudinal amplitude into a separate class (done)
     - Implement matrix extension for convergence checks.
     - ```n_l```, ```n_m```, ```n_l_pos``` could be properties
     - At that point we should review the conventions (e.g. Qs or Q_s?, do we use f or omega, tunes... -> we should be consistent across the code).
     - Then move to impedance, damper etc.

    Questions:
     - Maybe move de parameters in a dictionary and not have them as lose members of the object. Easier to make copies of objects.
     - We need a slim physics manual for notations and conventions.

??? note "Plan (16/06/2021)"

     - Detuning extension (Gianni) – end of August (can be done in parallel or later than the second point)
     - Make some separate tests on impedance sum - check best strategy time wise (Nicolas) – end of August
     - If FactorizedMatrix is the way to go, generalize its implementation with functions of “m” for R and R_tilde (Nicolas/Gianni)
     - Impedance Matrix implementation (Nicolas)
         - Do it first in numpy/scipy
         - Write it in the latex doc
         - (Profile C++ vs Numba)
     - Unit tests (Nicolas)
     - Examples (Nicolas/Gianni/Sofia/Sebastien)
     - Documentation (Nicolas/Gianni)
         - Docstrings
         - Readthedocs (doc on installation & use)
     - (Attempt to parallelize on radial modes) (Nicolas)
     - Convergence strategy (Nicolas/Gianni)


### *PySSD*

*Involved persons: Xavier*

 - Move to standard python-package structure (pip installable)
 - Improve integration with DELPHI

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

### *PyRADISE*

*Involved persons: Xavier, Sondre*

  - Prepare startup examples.

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021



### *Impedance ToolBox*

*Involved persons: Nicolas, Markus*

- Develop a python package for the management of Accelerator Impedance Models.
- Use standard python-package structure (pip installable)
- The code should be interfaced to IW2D and TLWall
- Make sure that we cover specificities of all accelerators of interest (including injectors and possibly FCC)

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

### *IW2D and TLWall* 

*Involved persons: Nicolas, Markus, Carlo*

 - Move to standard python-package structure (pip installable)

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021


### *RFTrack*

*Involved persons: Andrea*

 - Support and development for identified use cases (positron sources, very low-energy machines, bunch compressors, electron cooling, RFQs, flash medical accelerator, Compton scattering)
 - Implementation of CSR 
 - Expose individual components (interpolators, integrators) for combined usage with other tools (possibly via python)

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

## Beam cooling tools

### *Interface*

*Involved persons: Davide, Andrea*

 - Develop a common interface to use and compare different beam cooling codes (e.g. betacool and RFTrack)
 - Further develop integration with other modeling tools (e.g. PyHEADTAIL, new tracking library)

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021-2022
 
## Linear collider tools

### *Placet / Placet2*

*Involved persons: Andrea*

 - Integrate in Placet 2 the missing features from Placet
    - Missing CLIC-specific physics to be implemented (e.g. Power Extraction and Transfer Structures)
    - Sliced beam model to be implemented
 - Improve integration with other tools (PyHEADTAIL, XTrack), e.g. expose CSR modeling

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021-2022. In particular:
        - Missing CLIC-specific physics should come in 2021
        - Sliced model should come in 2022

### *Guinea-Pig*

*Involved persons: Andrea, Daniel*

 - Focus on C++ implementation if possible
 - Extensions for FCC-ee being discussed

## Luminosity modeling tools

### *LumiMod*

*Involved persons: Guido, Gianni, Ilias*

- Review and document the code 
- Move to standard python-package structure (pip installable)

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2021

## Beam source modeling

### *ONIX*
*Involved persons: Anna, Jacques*
 
 - Adaptation to CERN’s H- source

??? note "Milestones and timeline"
    - Timescale for objectives mentioned above: 2022

## FCC-ee developments

*Involved persons (from ABP): Riccardo, Xavier, Gianni, Tobias, Frank Schmidt, Daniel, Frank Zimmermann*

 - Synergy with code development project led by EPFL
 - ABP involved on three main fronts:
    - Development of optics tools
    - Modeling of interaction regions (e.g. Beamstrahlung)
    - Collimation studies
