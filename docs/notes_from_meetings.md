# Notes from ABP Computing Meetings

The **agenda and Zoom links** of ABP Computing Meetings can be find in the corresponding **[indico category](https://indico.cern.ch/category/8448/)**

Information and some points to be followed up from each meeting can be found in the following.

## [22 October 2021](https://indico.cern.ch/event/1082573/)
**Present:** F. Asvesta, R. Bruce, X. Buffat, F. Carlier, L. Deniau, J. Farmer, D. Gamba, L. Giacomel, G. Iadarola, P. Kicsiny, A. Latina, K. Paraschou, A. Poyet, F. Van Der Veken.

### *Notes from the meeting*

...


## [17 September 2021](https://indico.cern.ch/event/1077444/)
**Present:** F. Asvesta, R. Bruce, F. Carlier, R. De Maria, R. De Maria, L. Deniau, D. Gamba, L. Giacomel, P. Hermes, G. Iadarola, P. Kicsiny, J. Molson, N. Mounet, A. Poyet, M. Schwinzerl, G. Sterbini, F. Van Der Veken

### *Notes from the meeting*

- [NXCALS survey](https://docs.google.com/forms/d/1epQbDRPrYLgLKDVXiS6qZkS2nsdphSDgO2ShaDaLyQ0) has been launched: please take the time to share your experience and future needs.
- VEGA HPC cluster test: report being edited by IT. ABP participants contacted to provide feedback
- Very interesting talk on non-linear normal forms at last LNO meeting (L. Deniau). Subject for future ABP computing forum.
 - Ongoing work on Xsuite:
     - Synchrotron radiation advancing well (A. Latina, G. Iadarola)
     - Interface with Geant4 running, setting up of HL-LHC loss map ongoing (A. Abramov)
     - Strong-strong 6D bb being developed (P. Kicsiny, X Buffat)
     - Large scale DA simulation (10k jobs) being compared against Sixtrack (S. Kostoglou, G. Sterbini)
     - First long space-charge studies to launched (H. Bartosik, G. Iadarola)
     - Generation of matched gaussian beam distributions with non-linear bucket (F. Asvesta), to be extended to more distributions of interest (pencil, halos…)
     - Next important milestones
        - Implementation of reference management for knobs - deferred-expression like (R. De Maria)
        - Lattice description, can we think of a further integration with MAD-X/cpymad which considers flexibility required for collective effects simulations (R. De Maria, G. Iadarola, T. Persson)
        - Porting of particle scattering from sixtrack for collimation, K2 and Fluka coupling (F. Van Der Veken, P. Hermes, ?)
        - Implementation of beam loss refinement, aperture interpolation (G. Iadarola, A. Abramov)
        - Porting of symplectic interpolator from sixtracklib (K. Paraschou, G. Iadarola)
        - Interface with MAD-NG would be a plus  needs MAD-NG/python interface (L. Deniau)




### *Points to be followed up*

- On the benchmark of synchrotron radiation in Xsuite people who might be interested are Axel, Andrey, Felix Carlier.
- Riccardo, Gianni, Felix and Tobias could start a discussion on rationalizing machine descriptions.
- Pascal, Bjorn and James are facing massive slowdown of AFS
- Axel discussed with Tobias and Leon to create tables with the EMIT module in MAD-X (presently one needs to parse the stdout).
- Lorenzo (as Xavier in the past) experiences large failure rate (>5%) for long HTCondor jobs.




## [3 September 2021](https://indico.cern.ch/event/1071870/)

**Present:** F. Asvesta, R. De Maria, L. Deniau, P. Elson, J. Farmer, P. Hermes, G. Iadarola, P. Kicsiny, S. Kostoglou, A. Latina, A. Latina, L. Mether, N. Mounet, K. Paraschou, A. Poyet, M. Schwinzerl, G. Sterbini, F. Van Der Veken, A. Wegscheider

### *Notes from the meeting*
 - From [ATS-CTTB](https://indico.cern.ch/event/1062485/) meeting (20 Aug):
    - Presentation of Community Forum: Machine Learning (V. Kain): "ML coffees' will evolve into the new Machine Learning Community Forum (conveners: A. Apollonio, V. Kain, F. Velotti). Positive experience from the CloudBank pilot project from IT to access computing resources (e.g. GPUs and even quantum computers) from external cloud providers (Google, Amazon)
    - Remote Operations Gateway (T. Oulevey): New service developed by BE-CSS to access resources in the TN from outside CERN. It allows connecting to linux machines in the TN through a web browser (could be quite handy for machine follow-up).
    - Confirmed end of support for Windows in Controls (M. Gourber-Pace)
    - Replacement campaign is ongoing for faulty Siemens I/O cards
 - CASTOR service is being discontinued: Users should have been already contacted to move their data
 - [Compute accelerator forum](https://indico.cern.ch/event/975014/) on 8 September. Presentation on Kokkos (C++ performance portability programming model)
 - PRACE (Partnership for Advanced Computing in Europe) offers several online courses (often for free). Full list [here](https://events.prace-ri.eu/category/2/).
- [School on Efficient Scientific Computing](https://web.infn.it/esc/index.php?lang=en) in Bertinoro (Italy), 4 - 9 Ottobre 2021. ABP could support participation of 1-2 interested students.
- [Pymask v1.1.0](https://github.com/lhcopt/lhcmask/releases/tag/v1.1.0) released recently
    - Should cover all use-cases of old mask files and offers more features
    - We plan to soon shift to Pymask for long-term support. Please start using it and don't hesitate to give feedback.
- Developemnt of [Xsuite](https://xsuite.readthedocs.io) for tracking simulations is advancing well. First production studies launched. Fell free to give it a try.
- Discussion on NXCALS/LSA (re)naming conventions, status [here](https://wikis.cern.ch/display/NXCALS/CMW+Entity+Lifecycle+proposal+and+object+renames).
- Status of GUI development platforms:
    - Java is and will be supported
    - PyQT community growing fast especially in the injectors

### *Points to be followed up*
- Check status of "pip install nxcals".
- [NXCALS survey](https://docs.google.com/forms/d/1epQbDRPrYLgLKDVXiS6qZkS2nsdphSDgO2ShaDaLyQ0) has been launched: please take the time to share your experience and future needs.





## [2 July 2021](https://indico.cern.ch/event/1054674/)

**Present:** R. Bruce, X. Buffat, R. De Maria, J. Farmer, D. Gamba, L. Giacomel, G. Iadarola, S. Kostoglou, L. Mether, J. Molson, K. Paraschou, M. Schwinzerl, F. Soubelet, G. Sterbini, T. Tobias, A. Wegscheider.

### *Notes from the meeting*

 - [UDEMY offer for CERN](https://lms.cern.ch/ekp/servlet/ekp?PX=N&TEACHREVIEW=N&CID=EKP000043690&TX=FORMAT1&LANGUAGE_TAG=en&DECORATEPAGE=N) includes several course that could be of interest
 - Xsuite is coming together:
     - Integrated suite for single-particle and collective effects simulations
     - Supports CPU and GPU
     - Just introduced integration with PyHEADTAIL.
     - By now tested for LHC with bb and machine imperfections and on SPS with frozen spacecharge
     - Info at https://xsuite.readthedocs.io
     - Feedback is welcome

### *Points to be followed up*

 - There is an inconsistency in the element naming between twiss and survey in cpymad (```:n``` missing in survey). This is fixed in the mad-x master. Will become available in lxplus from the next release.



## [25 June 2021](https://indico.cern.ch/event/1052393/)

**Present:** F. Asvesta, R. Bruce, R. De Maria, L. Deniau, J. Dilly, J. Farmer, D. Gamba, A. Gerbershagen, L. Giacomel, H. Graham, M. Hofer, G. Iadarola, P. Kicsiny, J. Molson, N. Mounet, K. Paraschou, F. Soubelet, G. Sterbini, T. Tobias, F. Van Der Veken.

### *Notes from the meeting*

Continued review of tools to launch and manage jobs:

 - Presentation by Felix on PyLHCsubmitter
 - Presentation by Michael on DAGman

## [18 June 2021](https://indico.cern.ch/event/1048148/)

**Present:** R. Bruce, R. De Maria, L. Deniau, J. Dilly, J. Farmer, D. Gamba, L. Giacomel, A. Gerbershagen, H. Graham, P. Hermes, C. Hernalsteens, E. Hoydalsvik, M. Hofer, G. Iadarola, A. Latina, J. Molson, T. Persson, A. Poyet, G. Russo, F. Soubelet, G. Sterbini, F. Van Der Veken, A. Wegscheider.

Started discussion on tools to launch and manage jobs:

 - Presentation by G. Sterbini

General feedback: users prefer small tools for individual functionalities (templating, job submission) to be combined flexibly in python, instead of complex integrated tools that might lack flexibility and require a big investment to integrate our codes. Agility and adaptability to different simulation setups is key



## [11 June 2021](https://indico.cern.ch/event/1048147/)

**Present:**  J. Dilly, J. Farmer, A. Gerbershagen, P. Hermes, M. Hofer, G. Iadarola, A. Latina, L. Mether, N. Mounet, T. Persson, F. Soubelet.

### *Notes from the meeting*

- A [Web Development Technical Exchange meeting](https://indico.cern.ch/event/1046226/) organized by BE-CSS will takeplace on Thursday, June 24.
- The next computing meeting (18 June) will be devoted to tools for HTCondor submission and management.
- “ABP Computing day” will take place towards the end of the year.
    - The main goals will be:
        - Discuss the progress on software development activities in ABP
        - Present the strategy and objectives for 2022+
    - Tentative date: Thu 18 Nov 2021 (there might be a conflict with Evian 2021)
    - Agenda to be drafted early enough to allow for proper preparation
    - Proposals on possible topics and contributions are very welcome

### *Points to be followed up*

- Tobias has finished the implementation of the wire in MAD-X. Guido and team will test it.
    - It would be useful to have a script in the MAD-X repository to generate cpymad from a development version. It could be limited to linux for the time being.
    - Tests could be made against the R matrix computation from tracking (using finite differences) implemented by Kostas.
- Guido found problems runnnig pytimber on SWAN to access NXCALS:
    - [Ticket opened](https://issues.cern.ch/browse/PYT-60) with CSS team


## [4 June 2021](https://indico.cern.ch/event/1045636/)

**Present:**  R. Bruce, F. Carlier, R. De Maria, P. Elson, J. Farmer, D. Gamba, A. Gerbenshagen, P. Hermes, G. Iadarola, A. Latina, L. Mether, J. Moldson, N. Mounet, K. Paraschou, F. Soubelet, G. Sterbini, M. Schwinzerl, F. Van Der Veken.

### *Points to follow up*

- Points related to BE-CSS services:
    - Users had issues using pytimber with NXCALS. Something went wrong with their access request and they had troubles related to authentication. The main issue was that the exception raised did not refer at all to authentication and therfore it took very long time to diagnose the problem.
    - PyJAPCScout is now being used widely in the injectors for commissioning and studies. The tool could be presented to a wider community in an AccPy meeting. It would be good to identify features of general interest and incorporate them in PyJAPC.
    - There were issues installing NXCALS on the SWAN Stack 100. In principle NXCALS should be already installed.
 - On 18 June there will be a meeting dedicated to HTCondor submission tools.
 - It would be good to make a new release of sixtrack and update the sixtrack version on AFS.



## [7 May 2021](https://indico.cern.ch/event/1037110/)

**Present:** X. Buffat, R. Bruce, F. Carlier, L. Deniau, J. Dilly, J. Farmer, P. Hermes, M. Hofer, D. Gamba, L. Giacomel, G. Iadarola, A. Latina, L. Mether, J. Molson, N. Mounet, K. Paraschou, T. Persson, M. Schwinzerl, F. Soubelet, G. Sterbini.

### *Information*

 - BE-CSS contacted us to see if there is any interest from our side to use SWAN in the technical network:
    -  If such a service becomes available there would be definitely several users in ABP (especially if PyJAPC, PjLSA etc. would also be accessible through SWAN-TN).
    - A question that was raised is wether making SWAN available in the TN would mean that the EOS filesystem would become also available in the TN (as SWAN presently runs on EOS). This would be very useful to avoid the overhead of copying data for offline analysis.
 - The reorganization of the HTCondor e-groups has been finalized. Users from old e-groups (SLAP, ICE) have been redistributed. Old e-groups have been discontinued.
 - Tobias and Laurent annonced the latest MAD-X release.
 - Nicolas and Markus announced their [new python package for handling impedance models](https://indico.cern.ch/event/1007418/contributions/4228063/).


### *Points to be followed up*

 - AWAKE groups for batch and HPC should be rationalized.
 - General discussion on HTCondor use and performance (to be followed up with IT):
    - Different teams have developed tools to launch and manage HTCondor jobs (the most advanced are most likely from the OMC team and Guido/Axel).
    - There is a general interest in using a supported python API for HTCondor. Could IT provide such a service?
    - Users observe high failure rate for long jobs due to the fact that sometimes the SCHEDD stops working for a short time and the job hangs. Can any improvement be considered on the IT side?
    - Users find the 2 GB of RAM associated with a single-core job small for many jobs. What is the overhead in terms of priority of requesting two cores just to have more RAM?
 - Davide is working on the implementation of PyJAPC scout
    - It would be useful to have a basic intro page






## [30 April 2021](https://indico.cern.ch/event/1034138/)

**Present:** R.Bruce, X. Buffat, R. De Maria, F. Carlier, L. Denieau, J. Dilly, J. Farmer, S. Furuseth, A. Gerbershagen, P. Hermes, M. Hofer, G. Iadarola, A. Latina, J. Molson, N. Mounet, K. Paraschou, T. Persson, M. Rognlien, M. Schwinzerl, F. Soubelet, F. Van Der Veken.

### *Information*

 - A very interesting workshop on “CloudBank” pilot project took place on Tuesday. Allows usage of computing resources from commercial providers (e.g. Google, Amazon) See [indico page](https://indico.cern.ch/event/1021544/).
 - HTCondor groups reorganization:
    - Users from old e-groups (SLAP, ICE) were redistributed (thanks to Massimo for the help!). The old e-groups will be discontinued soon.
    - Users can use the [Haggis tool](https://haggis.cern.ch/) to check their accounting group (accessible only within the CERN network).
 - MAD-NG vs PTC discrepancy for CLIC is understood. MAD-NG works on Apple M1. Work on non-linear normal forms is advancing.

### *Points to be followed up*

 - It would be convenient to have the long-name export from MAD to sixtrack enabled by default. This should come with the next MAD release (next week).
 - James would be interested in trying CVMFS for alleviating AFS/EOS issues with IO intensive startup of many jobs. A "beam-physics" CVMFS space was recently created (reqeuest by Cedric, TE-MPE) and could be used for this purpose. There should be the possibility of restricting access, e.g. to comply with software license conditions.
 - Many parallel FCC-ee tracking efforts are starting. It is not always trivial to understand tools assumptions and conventions (e.g. with respect to tapering and sawtooth orbit). Some coordinated benchmarking effort would be beneficial.
    - Andrea mentioned tha some benchmarking of MAD-X radiation features against MAD8 and Placet was done in the past.

## [23 April 2021](https://indico.cern.ch/event/1030187/)

**Present:** A. Abramov, X. Buffat, J. Dilly, J. Farmer, L. Giacomel, D. Gamba, P. Hermes, G. Iadarola, A. Latina, J. Molson, N. Mounet, M. Rognlien, T. Persson, F. Soubelet, G. Sterbini, F. Van Der Veken

### *Information*
 - CERN HPC team asked for test simulations that could be used to validate scalability on large external HPC clusters (details on [mattermost](https://mattermost.web.cern.ch/abpcomputing/pl/9e3p675jf7df8rexwcpk6qhqey)).
 - Registrations to [PyHEP2021](https://indico.cern.ch/event/1019958/) (July 2021) are open.
 - HTCondor usage: so far no visible side effect of accounting groups remapping.
 - James mentioned that bugfixes for Geant4 have been provided (related to issues mentioned in a previous meeting) and are being tested. Pull request for sixtrack coming soon (mostly collimation features).
 - Andrea developed backtracking in RFTrack for injector-gun design based on required distribution defined downstream.
 - Nicolas asked for passwordless access to NXCALS. It can be done only with kerberos.
 - Markus suggested to look into the joblib library for simple parallel tasks.

### *Points to be followed up*
 - MAD-X team looking into issue with IBS module.
 - Pascal encountered issues with BOINC spool space. Being followed-up.
 - Gianni/Frederik/Tobias to have a chat on status and evolution of DIST library.



## [16 April 2021](https://indico.cern.ch/event/1027542/)

**Present:** R. Bruce, X. Buffat, D. Gamba, G. Iadarola, R. De Maria, J. Dilly, S. Joly, P. Elson, J. Farmer, A. Gerbenshagen, L. Giacomel, A. Latina, T. Persson, F. Soubelet, G. Sterbini, F. Van Der Veken.

### *Information*

- ABP HTCondor quota remapped on Tuesday 13 Apr:
    - we now have a single computing group “group_u_BE.ABP.NORMAL”, which is organized in six e-groups associated to the sections
        - batch-u-abp-cei (contains the old e-group: htcondor-u-ICE)
        - batch-u-abp-hsl
        - batch-u-abp-inc
        - batch-u-abp-laf
        - batch-u-abp-lno (contains old e-group: htcondor-u-SLAP)
        - batch-u-abp-ndc (contains old e-group: LHC-COLL-LSF-users)
   - Please use the new section e-groups to add new users.
   - The old e-groups will be discontinued after moving the users to the respective section e-group.
 - Discussion have started to prolong the exploitation of the [cluster at INFN-CNAF](computing_resources/hpc_cnaf.md) (800 cores) beyond the end of the contract (Dec 2022).
    - We could prolong its usage for three more years (paying the energy consumption)
    - If some extra funding is available, a few more nodes could be added to compensate for expected “ageing”.
    - It is assumed that it will be used mostly for single-node jobs (up to 48 cores) due to end of support of the installed low-latency network (OK based on past experience).
 - A survey is being run across the BE department to identify services provided by the IT department on which we rely for simulations and data analysis. The goal is to put in place a coordinated interface to IT and find synergies with other ATS departments.
    - Some draft slides are discussed. Points that could be added:
        - HDFS filesystem for data storage for spark-based analysis.
        - Users would like a more complete and supported software stack (libraries, compilers, python, etc.)
        - Openshift and webservices for documentation.
        - Openstack, GitLab
        - Licensed software: Mathematica, Matlab, CST, etc.
        - Lxplus, Windows Terminal Services
 - Information from Phil (CSS):
     - A software stack based on LCG 100 is being prepared for usage in LXPLUS via CVMFS.
     - A pip-installable NXCALS-pyspark bundle is being also considered.
 - NXCALS can be accessed from outside CERN using an ssh tunnel. ```lxtunnel.cern.ch``` to be preferred to ```lxplus.cern.ch``` for this purpose (see [recipe](guides/sshtunnel.md) just updated by Joshua).
 - Discussion on how to best reformat JAPC data for storage on parquet files: one possibility is to use the same serialization used at RDA level.


## [9 April 2021](https://indico.cern.ch/event/1025755/)

**Present:** R. Bruce, X. Buffat, R. De Maria, L. Deniau, J. Farmer, A. Gerbenshagen, L. Giacomel,  P. Hermes, G. Iadarola, A. Latina, N. Mounet, T. Persson, F. Soubelet, G. Sterbini, F. Van Der Veken.

### *Information*

 - Phil from CSS will join the next meeting.
 - Applications are open for the upcoming [CERN thematic School on Computing](https://indico.cern.ch/event/1017080/) on "Scientific Software for Heterogeneous Architectures”.
 - A [guide on mounting EOS on mac](http://abpcomputing.web.cern.ch/guides/eos_on_mac/) has been prepared by Ilias, Guido and Joshua. More info also on [this mattermost discussion](https://mattermost.web.cern.ch/abpcomputing/pl/5p54ieirofdxf8caejuy64emuy).
 - An [Accelerating Python user's meeting](https://indico.cern.ch/event/974794/) will take place t2021 Q1 on 29 April. Topics:  PyTimber, PyJapc, accwidgets, asyncio usage
 - A pilot program was launched by IT and IPT to access commercial cloud services (Google, Amazon). A [workshop](https://indico.cern.ch/event/1021544/) will be held on Apr 28 to have a first overview.
 - Information on how to install EOS on Ubuntu can be found in [this docker file](https://gitlab.cern.ch/sterbini/be-abp-docker/-/blob/master/Dockerfile) prepared by Guido.
 - Frederik deployed a fixed version of SixDesk/DB in the AFS repository (compiles correctly).
 - Issues with slicing of solenoid in MAD-X was fixed by Helmut.
 - Nicolas and Markus found very convenient to use [joblib](https://joblib.readthedocs.io/en/latest/) for simple parallelization in the new Impedance Toolbox.


### *Points to be followed up*
 - New e-groups for access to HTCondor have been created. One per section, with associated admin e-group. SL and CP members have been added to admin e-group for their sections
    - We will proceed to the remapping of the ABP quota quota next week. The operation should be transparent as the old e-groups were inserted inside the new ones.
    - We should gradually empty the old groups and move users to the new ones
 - Guido prepared an "ABP docker container" based on Ubuntu with the typical tools (python installation, mad-x) and the capability of mounting EOS.
    - An installation of HTCondor will also be added.
 - An issue was identified in the usage of beam-beam in sixrtack with ions (see [GitHub issue](https://github.com/SixTrack/SixTrack/issues/1082)). A workaround has been inserted in pymask to circumvent the problem.
 - Frederik is now working on fixing the error ruotines for the mask. Should be ready in a few weeks.
 - A ticket has been opened by external users on the IBS calculation for MAD-X in some special cases. Tobias will look into it together with Fanouria.
  - Andrea is studying multibunch effects for the FCC-ee injector linac. He improved the modeling of the wakefields. Perhaps we could look into possible synergies with PyHEADTAIL.






## [26 March 2021](https://indico.cern.ch/event/1021214/)

**Present:** R. Bruce, X. Buffat, R. De Maria, L. Deniau, F. Calier, J. Dilly, J. Farmer, S. Furuseh, D. Gamba, L. Giacomel,  P. Hermes, M. Hofer, G. Iadarola, A. Latina, J. Molson, N. Mounet, T. Persson, K. Paraschou, T. Pieloni, F. Soubelet, G. Sterbini, F. Van Der Veken.


### *Information*
- JetBrains (the company developing PyCharm) is looking for early adopters at CERN for their new IDE for data analysis and prototyping machine learning models.
 - An interesting reading: [“Good enough practices in scientific computing"](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510)
 - The [Zenodo service](https://zenodo.org) allows getting DOI code for data and code, for referencing in publications.
 - Tatiana introduced the EPFL project on FCC-ee code development.
 - Nicolas had very satisfactory results speeding up pythoon code with numba parallel.


### *Points to be followed up*
 - There are discussions ongoing on the future of PyTIMBER (see: https://wikis.cern.ch/display/NXCALS/Future+of+PyTimber). Riccardo joined the meeting.The idea is to converge to a single Python interface for NXCALS, which is easy to install, exposes the pyspark features, and has high-level methods like pytimber. CSS plans to discontinue the Java Backport API at the end of Run 3.
 - Pascal encountered a blocking issue installing SixDesk/SixDB. Frederik will provide some help.
 - It is proposed to enable the long names by default in the sixtrack input generation of MAD-X (requires Sixtrack V).
 - Some updates have been introduced in the SixTrack collimation features (to be pushed). A problem has been identified in Geant 4 (a bug report has been opened).
 - Non-staff members of the collimation team have issues accessing the source of Fluka.
 - Nicolas asked whether anybody has experience with the diagonalization of very large matrices. Riccardo faced the problem in the past and will provide the solution that he adopted.


## [19 March 2021](https://indico.cern.ch/event/1019549/)

**Present:** F. Antoniou, F. Asvesta, H. Bartosik, R. Bruce, F. Calier, R. De Maria, L. Deniau, P. Elson, J. Farmer, S. Furuseth, J. Dilly, P. Hermes, D. Gamba, L. Giacomel, M. Hofer, G. Iadarola, A. Latina, N. Mounet, K. Paraschou, T. Persson, T. Pieloni, F. Soubelet, G. Sterbini, F. Van Der Veken.

### *Information*
 - The TE-MPE team would like to store software for beam physics in CVMFS. We will propose to create a general "beam-physics" project in CVMFS where we will able to store also ABP software if needed.
 - Even if the AFS phaseout has been put on hold, IT is still checking with users whether their project spaces could be moved to EOS. In general this works for data storage, but can create problems when using the filesystem as a working space for simulations (e.g in HTCondor). For this kind of usage we have the option to keep using AFS.
 - Next events: [GPU Technology Conference 2021 (GTC21)](GPU Technology Conference 2021 (GTC21), free to attend), free to attend.


### *Points related to CSS services*
 - [This page](http://abpcomputing.web.cern.ch/guides/accpy/) summarizes issues encountered with python packages stored in PyPI, which depend on packages available only in the acc-py repository. Although a workaround was identified it would be good to find a more flexible solution.
 - The ongoing development to adapt PyJAPC to the needs of the injectors commissioning (to discontinue the usage of matlabMonitor) is using [this repository](https://gitlab.cern.ch/abpcomputing/sandbox/pyjapcscout). More info can be found in the [slides shared by Guido](https://codimd.web.cern.ch/p/YOehZUxXv#). The main needs are:
    - Ensuring “synchronization” of a list of devices properties
    - Having a single centralized callback
    - Saving automatically the data in a “reasonable” format.
 - Relying on pandas for the data manipulation is a reasonable choice. The candidate format for the data saving is parquet at present, but we could probably get in contact with the NXCALS team to see if they have any further suggestion. Feather and HDF5 could also be investigated.
 - Answers to some of the questions in Guido's slides were provided by Phil after the meeting
    - *Q: Is it possible to install Acc-Py on non TN machines? Is there a container/docker image?* A: Yes, there is an installer for the base distribution available. Please see https://wikis.cern.ch/display/ACCPY/Acc-Py+base#Acc-Pybase-UsingAcc-Pybase. If there are any issues, please contact acc-python-support@cern.ch for the installer. There is a prototype docker image, but we have not officially released it yet; we would happily engage with anybody who wanted to use the docker image to better understand the use cases and requirements.
    - *Q: Is there a better way to avoid blocking the exit of a Python application which uses the JVM?* A: The next version of cmmnbuild-dep-manager includes a workaround for Java libraries that aren’t correctly clearing up their non-daemon threads. This will be released over the coming days as cmmnbuild-dep-manager 2.8.0.
    - *Q: What is the best way to build documentation for packages with Acc-Py* A: Please see https://wikis.cern.ch/display/ACCPY/Documentation for some tips. We would be very happy to improve our documentation service’s documentation 😊… please get in touch if something isn’t clear or could be better phrased! Note that this service is only available inside the GPN – we don’t currently plan to make the documentation available outside of the CERN network. For externally hosted documentation readthedocs is a good solution.


## [12 March 2021](https://indico.cern.ch/event/1017254/)

**Present:** X. Buffat, R. Bruce, F. Carlier, R. De Maria, J. Dilly, L. Deniau, J. Farmer, S. Furuseth, P. Hermes, M. Hofer, G. Iadarola, L. Giacomel, S. Kostoglou, A. Latina, J. Molson, N. Mounet, T. Persson, G. Sterbini.

### *Information*
 - Phil from CSS will join the next meeting (19 March 2021)
 - Talks on GPU applications at last Compute Accelerator Forum ([link](Talks on GPU applications at last Compute Accelerator Forum (link))).
 - Gianni is progressing with the development of the Xfield library.
 - Sofia is continuing the development of pymask to cover simulations with ions.
 - Pascal is looking into refurbishing the python tools used for collimation, to move to a pip-installable package. Something that might be useful:
    - [Guidelines for python packages](http://abpcomputing.web.cern.ch/guides/python_packages/) are available on the ABP Computing website (including an example package with instructions).
    - Git workflows can be used for the automatic deployment in PyPIC (see for example [PyLHC](https://github.com/pylhc/omc3/blob/master/.github/workflows/publish.yml)).
 - Guido found an [issue](https://github.com/lhcopt/lhcmask/issues/37) in the generation of the MAD-X beam-beam lenses in pymask (which does not affect the generation of the sixtrack models, unless matchings are done with beam-beam on). This has been fixed in the latest release.
 - Laurent is working on non-linear normal forms.
 - Andrea (and Raul) are porting CSR features form Placet 1 to Placet 2, improving the implementation in different ways.
 - John and the AWAKE team solved an issue with their quasi-static PIC code.
 - Riccardo added a little feature in cpymad to access the strengths generated by the correct module.


### *Points to be followed up*
 - IT is moving Nag and Lahey compilers and libraries from afs to cvmfs. The compilers are indeed used to test sixtrack compilation.
 - Joshua and Felix prepared an [intro page on AccPy](http://abpcomputing.web.cern.ch/guides/accpy/). Here they summarize also the issues that they faced with python packages hosted in the standard PyPI index, which depend AccPy hosted packages. Their workaround to make the package pip installable is described in the page o Definitely a general issue to be discussed with CSS.
 - EPFL is working on code development for FCC-ee. Input on possible software requirements for future studies is welcome.
 - MAD-X development (Tobias):
    - Issue with equilibrium emittance calculation in the presence of tapering being investigated (for FCC-ee).
    - Improving the slicing of RBEND (placing of slices for shared dipoles).
 - Sondre finds extreme numerical convergence conditions (number of slices) in COMBI to resolve the tune shift.
 - Roderick and team are working on identifying software tools for collimation studies for FCC-ee. In a few weeks we could have a first discussion on collimation requirements for the Xtrack library that is being developed.
 - Discussion are starting in CSS on how to rationalize python tools to access NXCALS.


## [5 March 2021](https://indico.cern.ch/event/1013327/)
**Present:** X. Buffat, R. Bruce, F. Carlier, L. Deniau, R. De Maria, J. W. Dilly, J. Farmer, M. Hofer, D. Gamba, P. Hermes, G. Iadarola, A. Latina, S. Joly, N. Mounet, M, Rognlien, G. Sterbini, T. Persson, F. Soubelet, F. Van Der Veken.

### *Information*
- New [ABP Computing Sandbox space](https://gitlab.cern.ch/abpcomputing/sandbox) was created on GitLab (suggestion by Davide and Guido). Feel free to use it as incubator for new shared projects.
- Following discussion from last meeting:
    - Guido prepared a simple guide on the use of docker containers (available [here](http://abpcomputing.web.cern.ch/guides/docker/))
    - Nicolas prepared a small guide on how to install PyHEADTAIL on Mac using Anaconda (available [here](https://github.com/PyCOMPLETE/PyHEADTAIL/wiki/Installation-Notes#installation-on-macos-with-anaconda))
- In SixTrack two bug-fixes related to collimation were introduced (see [PR1](https://github.com/SixTrack/SixTrack/pull/1077) and [PR2](https://github.com/SixTrack/SixTrack/pull/1078))
- Report from the last IT User Meeting (by Laurent). Agenda and material of the meeting can be found [here](https://indico.cern.ch/event/980347/). Particularly relevant for our scientific computing activitiies:
    - AFS replacement is now stopped (since no available drop-in solution was found). The strategy will be reviewed at the end of Run-3 (Interesting review document published - https://cds.cern.ch/record/2750122).
    - A working group is being setup to look into possible replacement of CentOS7 due to a change in support policy from RedHat. 
- There is an upcoming OpenLab Technical workshop ([indico page](https://indico.cern.ch/event/1009424)).


### *Points to be followed up*
 - For MAD-X:
     - The new MAD-X release is slowly converging.
     - The build through GitHub actions started failing due to an upgrade of the compiler on the GitHub size (probably related to vectorization and data alignment). It might be related to the problems recently encountered by Riccardo (see [issue](https://github.com/MethodicalAcceleratorDesign/MAD-X/issues/982)).
 - For SixTrack:
    - Sixtrack build with GCC 10 was failing due to multiple includes in DISTlib. A workaround has been introduced in sixtrack (see [PR](https://github.com/SixTrack/SixTrack/pull/1076)),  but proper fix needs to be introduced in DISTlib.
    - Full crab cavity tilt required by Sofia is not really easy to implement, but could be handled through reference frame rotations in the user's side.
- Features to complement PyJAPC are being developed in the [PyJapcScout repository](https://gitlab.cern.ch/abpcomputing/sandbox/pyjapcscout) on the ABP Computing sandbox.
- Josh and Felix are facing issue in the development of the OMC3 toolbox, having to combine packages from the standard PyPI and the acc-py package indices. They arranged a workaround and summarized the situation [here](guides/accpy.md) -> to be discussed with Phil, to see whether better solutions can be identified.


## 26 February 2021

### *Seminar*
Our usual round table was replaced by a seminar by R. Brito Da Rocha from IT on "Notebooks and Computing Workflows with IT services".
The slides and and the recording of his presentation are available on [indico](https://indico.cern.ch/event/976158/).

## 19 February 2021
**Present:** R. Bruce, X. Buffat, L. Deniau, P. Elson, J. Farmer, P. Hermes, G. Iadarola, S. Kostoglou, A. Latina, N. Mounet, T. Persson, G. Sterbini.


### *Information*
 - P. Elson, indicated as link person between BE-CSS and BE-ABP, joined the meeting. He has vast background on python solutions for scientific computing and has a leading role in the AccPy community. He could join our meetings ~once per month, to discuss CSS services.
 - Two guides in abpcomputing website have been updated to cover Ubuntu 20.04:
    - [Local HTCondor installation](guides/htcondor.md) (thanks Joschua & co.)
    - [OpenAFS installation](guides/openafs.md) (thanks Guido, Riccardo etc.)
 - We have two new [Mattermost channels](https://mattermost.web.cern.ch/abpcomputing/channels/town-square): Six* (for sixtrack, sixdesk, and other things like that) and pymask.
  - The change of PyPI index caused by the installation of the acc-py-pip-config package can be undone with pip uninstall. Thanks Phil!
  - Sofia is working to extend pymask to work with ions.
  - There will be an inrmediat MAD-X course on 22-23 March


### *Points to be followed up*

 - Guido gave a [presentation at the ABP-INC meeting](https://indico.cern.ch/event/1006995/contributions/4226442) on how to reverse sequences using cpymad (generation of beam 4). cpymad input from python seems to be slower than calling a madx script file. To be investigated.
 - The issue with SixTrack V identified by the collimation team was traced back to wrong units used for the proton mass in one place (to be ported in the master branch). There was also an issue compiling Sixtrack in the presence of the dist module. For now this can be bypassed disabling the module (not needed for these studies). Tobias will follow it up. 
 - [Issue with crabcavity in MAD-X](https://github.com/MethodicalAcceleratorDesign/MAD-X/issues/981): it has been fixed in the MAD part. The problem with PTC still needs to be understood (not urgent). The fix for the MAD side will be deployed with the next release.
 - Group subscription in PyJAPC: Davide will start working on it soon, using examples for the PS provided by Alex. Phil provided useful suggestions to ease the implementation.
 - Nicolas asked for suggestions to get PyHEADTAIL running on Mac (issues with compiling the Cython part). One possibility is to usee Anaconda: after the meeting Nicolas provided a [simple recipe on the PyHEADTAIL wiki](https://github.com/PyCOMPLETE/PyHEADTAIL/wiki/Installation-Notes#installation-on-macos-with-anaconda). The alternative is to use docker -> some information on how to get started has been prepared by Guido ([available on CodiMD](https://codimd.web.cern.ch/1ZjsMtBuQkWrjJlAVbqk-Q), to be ported to the abpcomputing website).


## 12 February  2021

**Present:** R. Bruce, R. De Maria, J. Dilly, D. Gamba, A. Gerbershagen, P. Hermes, G. Iadarola, S. Joly, J. Farmer, A. Latina, L. Medina, N. Mounet, K. Paraschou, T. Persson, G. Sterbini, F. Van Der Veken.

### *Information*

- Phil Elson will be the CSS contact person for ABP
- News on GPU infrastructure from IT (e.g. GPUs for CI). More info ([here](https://indico.cern.ch/event/975007/contributions/4208132))
- Discussion on necessary prerequisites to migrate ABP tools for the injectors to PyJAPC, to be followed up in collaboration with BE-CSS
    - Need for group subscriptions (as available in MATLAB interface). Davide working on the development of this functionality
    - Need to identify a common way of saving PyJAPC data on file (Guido investigated the possibility of using parquet files)
- Some extra information on how to access NXCALS using pytimber is available at: http://abpcomputing.web.cern.ch/guides/pytimber_nxcals/
- Issues encountered with with Pytimber in SWAN: there are plans ot remove pytimber from SWAN and leave the installation to the user.
- News from BE-EA: some members of their team are already using cpymad. Their interface to mad-x (ApplePy) is being interfaced with the control system (CESAR).

### *Points to be followed up*

- Issue with CrabCavity map in MAD-X should be easy to solve. Fixing the PTC side is more involved but not urgent.
- Issue in the error routines in the lhcmask is expected to be addressed in 2-3 weeks.
- The collimation team had problems in compiling sixtrack, which could be solved only by removing the DIST block. Tobias is aware of this and will follow it up. No particular urgency, as this is not blocking.
- The collimation team is investigating different behaviors of the scattering routines between Sixtrack 4 and Sixtrack 5.
- Andrea is trying to align spacecharge and beambeam development in MAD-X from F. Schmidt and collaborators to the latest version of the code.
- Herry Randal is investigating speed issues of MAD-X compared to older versions. The issue seems to be related to OpenMP.

## 5 February  2021

**Present:** F. Asvesta, D. Banerjee, R. Bruce, X. Buffat, L. Deniau, R. De Maria, J. Farmer, S. Furuseth, A. Gerbershagen, L. Giacomel, P. Hermes, G. Iadarola, S. Kostoglou, J.B. Lallement, A. Latina, N. Mounet, T. Persson, G. Sterbini, F. Van Der Veken.

### *Information*
 - Opened Mattermost channel
 - Proposal (driven by BE-CSS) to create a structured interface between the ATS and IT managements, being discussed within ATS.
 - Software developers from the BE-EA team joined the meeting. They will stay in contact for discussions related to mad-x and layout database. Riccardo and team might use their expertise with BEACH to understand discrepancies with respect to MAD-X.
 - Tensor Processing Unit (TPU) made available experimentally by IT for machine learning applications (contact IT person: Ricardo Brito Da Roca)
 - CALS was discontinued on Feb 1, replaced by NXCALS.
 - Guido is working on a simple package to create trees of jobs.
 - Andrea implemented long-range wakes in RFTrack for studying multibunch effects in FLASH. Synergy with PyHEADTAIL for parallelizing interpolations.
 - Xavier implemented new feature in COMBI to have linearizeed beam-beam (for tests).


### *Points to be followed up*

 - MAD-X issues to be followed up:
     - Calculation of crabcavity R and T matrix not correct in MADX and PTC. (Required to include crab cavities in the HL-LHC sequence!). Related GitHub issue [here](https://github.com/MethodicalAcceleratorDesign/MAD-X/issues/981)
    - Current master segfaults on a long hl-lhc script when compiled with 'make'. Related GitHub issue [here](https://github.com/MethodicalAcceleratorDesign/MAD-X/issues/982)
    - Tobias is reviewing the behavior of the solenoid.

## 29 January 2021

**Present:** G. Iadarola, X. Buffat, L. Deniau, R. De Maria, J. Farmer, S. Furuseth, D. Gamba, S. Kostoglou, A. Latina, N. Nounet, K. Paraschou, G. Sterbini, F. Van Der Veken, T. Persson, F. Soubelet.

### *Informatio*n**

 - Ilias and Guido prepared a page for the configuration of NXCALS (pyspark) on lxplus. It can be found [here](guides/nxcals_lxplus.md).
 - The Timber web application does not work from outside the CERN GPN network.
    - To solve this, Riccardo and Davide have recipes to redirect the web traffic to the CERN network. Their bash scripts have been made available [here](http://abpcomputing.web.cern.ch/guides/sshtunnel/).
 - Example SixDesk study prepared by Sofia and Guido. First thoughts on how to extract components of general interest.
 - Davide and Andrea are working on benchmarking of cooling modeling tools. A thorough exploration of the parameter space is revealing quite educative, leading to several improvements in RFTrack.
 - Tracking library development: refactoring of GPU memory management is ongoing (Riccardo).
 - Davide is refactoring the MATLAB interface to the controls infrastructure (PyJAPC is now used under the hood).
 - John and the AWAKE team are comparing different PIC solvers in very challenging scenarios with many plasma buckets.
 - New release of MAD-X coming soon to fix a bug related to particle losses in PTC-Track (Tobias).
 - The CERN gitlab service now allows Continuos Integration tests on different GPUs (more info on Mattermost GPU).
 - Work on restructuring and extension of DELPHI Vlasov solver is ongoing (Nicolas).
 - GitHub actions allow build tests on several different platform (being used by MAD-X team).
 - We will have a IT seminar on "Notebooks and Computing Workflows with IT services" on 26 Feb ([indico page](https://indico.cern.ch/event/976158/)). 

### *Points to be followed up*

 - Reorganization of HTCondor e-groups (one e-group per section).
 - Codes [housekeeping page](housekeeping.md) to be completed with missing info.
 - Some of the tools from the OMC suite could be of general interest (e.g. harpy, machine imperfection management and correction). 
     - A first step could be to prepare a list of components that could be shared as individual packages, and start from the ones that are easier and more useful. 
     - An updated version of harpy should come within a few months.
 - In MAD-X/PTC, found a bug related to particles having mass that is not a multiple of the electron or the proton mass. Piotr might be able to look into that. 
 - There is a problem with imperfection simulation in the mask. If anybody needs simulations with imperfections before this is solved should contact Frederik.
 - COMBI team worried about "unintended consequences" of migrating repository to common space. Forking instead of transferring the project should be safe.

## 22 January 2021
(Kick-off meeting)

**Present:**  R. Bruce, R. De Maria, L. Deniau, G. Iadarola, J. Farmer, S. Furuseth, D. Gamba, L. Giacomel, A. Latina, J. Lettry, T. Persson, F. Van Der Veken.

### *Points to be followed up*

 - Please review the [list of objectives and activities](codespecific_activities.md) and provide feedback by Fri 29 Jan (comments already received from Roderik and Jacques --> added to the webpage)
 - Feel free to use the [abp-computing website](http://abpcomputing.web.cern.ch) to share any technical information/guideline of general interest (including those related to controls/operation tools).
 - Anybody interested in attending the meetings can self-subscribe the invitation list using [this link](meetings.md).
