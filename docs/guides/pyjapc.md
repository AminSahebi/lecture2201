# PyJapc and Accelerator data

- [PyJapc](https://gitlab.cern.ch/scripting-tools/pyjapc) is the official tool maintained by BE-CSS to access the CERN accelerator control system in Python using (JAPC)[https://wikis.cern.ch/display/JAPC).
- [PyJapcScout](https://gitlab.cern.ch/abpcomputing/sandbox/pyjapcscout) is a wrapper over PyJapc developed by ABP. The main difference with respect to the plane PyJapc is the data conversion from JAPC to Python. This was necessary to allow for storing the acquired data to Parquet files using [datascout](https://gitlab.cern.ch/abpcomputing/sandbox/datascout) package.
- [datascout](https://gitlab.cern.ch/abpcomputing/sandbox/datascout) is a small package of helper functions to easy saving and loading data (dict, [pandas](https://pandas.pydata.org), [Awkward-array](https://awkward-array.readthedocs.io/en/latest/)) mainly into parquet files.




