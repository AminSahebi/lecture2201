# Using NXCALS via pyspark on lxplus

*Prepared by Ilias*

## Introduction

[Ilias](mailto:ilias.ilias.efthymiopoulos@cern.ch) installed the [NXCALS](http://nxcals-docs.web.cern.ch/current/) bundle to our luminosity follow-up service account ```lumimod```. 

You need to have granted the access to NXCALS service and be in the egroup **it-hadoop-nxcals-pro-analytics**. Please follow the instruction [here](http://nxcals-docs.web.cern.ch/current/user-guide/data-access/nxcals-access-request/). 

As the software/bundles are installed in a public area, they can be used from any [lxplus](https://information-technology.web.cern.ch/services/lxplus-service) account. Ilias provided some shell scripts to facilitate the use:

Go in the your working folder (some link/subfolders will be created).

Use the script: 
```
source /afs/cern.ch/user/l/lumimod/public/nxcals/nxcals_lumimod_conda.sh
```
to initialize the conda installation, and then use the command:
```
conda activate nxcals-lcg95-env
```
to activate the environment. The two commands above need to be repeated for any new shell.

The following command, instead, needs to be used only once to set in your folder the soft links to the nxcals bundle files:
```
source /afs/cern.ch/user/l/lumimod/public/nxcals/nxcals_setupdir.sh
```

It is done.


## Accessing NXCALS data

In a configured directory with the commands above, one can use the pre-defined commands of the NXCALS bundle to:

- run an interactive session with pySpark
```
./spark-home/bin/pyspark
```
that can be further configured with additional options available from the help menu
```
./spark-home/bin/pyspark --help
```
A simple command to test could be:
```
from cern.nxcals.api.extraction.data.builders import *

data = DataQuery.builder(spark).byVariables() \
    .system('CMW') \
    .startTime('2018-07-20 13:38:00.000').endTime('2018-07-20 13:39:00.000') \
    .variable('LHC.BOFSU:TUNE_B1_V') \
    .build()

data.show(5)
```

- run interactively a python script as standalone application (without using `yarn`):
``` 
./spark-home/bin/spark-submit test.py
```
that an be also put to a crontab job or run in HTC-condor.

An example of `test.py` is the following:
```
#
# -- simple test file
#
from pyspark import SparkConf
from pyspark import SparkContext
from pyspark.sql import SparkSession
from cern.nxcals.api.extraction.data.builders import *

conf = SparkConf()

# Possible master values (the location to run the application):
# local: Run Spark locally with one worker thread (that is, no parallelism).
# local[K]: Run Spark locally with K worker threads. (Ideally, set this to the number of cores on your host.)
# local[*]: Run Spark locally with as many worker threads as logical cores on your host.
# yarn: Run using a YARN cluster manager.

# conf.setMaster('yarn')
conf.setMaster('local[*]')
conf.setAppName('spark-basic')

sc = SparkContext(conf=conf)
spark = SparkSession(sc)


intensity = DevicePropertyDataQuery.builder(spark).system("CMW") \
    .startTime("2018-06-17 00:00:00.000").endTime("2018-06-20 00:00:00.000") \
    .entity().parameter("PR.BCT/HotspotIntensity").build()

# count the data points
print('>>> data : ', intensity.count())
intensity.show()
```

- run interactively a python script as standalone application (using `yarn`) by using
```
./spark-home/bin/spark-submit --master yarn --executor-memory 4G --total-executor-cores 8 test_yarn.py

```

An example of `test_yarn.py` is the following.
```
from pyspark import SparkConf
from pyspark import SparkContext
from pyspark.sql import SparkSession

from cern.nxcals.api.extraction.data.builders import *

from pyspark.sql.functions import col
from pyspark.sql.types import StructType
from pyspark.sql.types import StructField
from pyspark.sql.types import DoubleType
from pyspark.sql.types import ArrayType

from pyspark.sql.window import Window
from pyspark.sql.functions import rank, col
import pyspark.sql.functions as func

import time

from matplotlib import pyplot as plt
import numpy as np

import pandas as pd
import os

# --- Configure spark

conf = SparkConf()

# Possible master values (the location to run the application):
# local: Run Spark locally with one worker thread (that is, no parallelism).
# local[K]: Run Spark locally with K worker threads. (Ideally, set this to the number of cores on your host.)
# local[*]: Run Spark locally with as many worker threads as logical cores on your host.
# yarn: Run using a YARN cluster manager.

conf.setMaster('yarn')
# conf.setMaster('local[*]')
conf.setAppName('spark-basic')

sc = SparkContext(conf=conf)
spark = SparkSession(sc)

# --- initial settings

tstart = pd.Timestamp('2018-10-23 11:22:40.094000101+0000', tz='UTC')
tend = pd.Timestamp('2018-10-23 13:36:20.035000086+0000', tz='UTC')
variable = 'LHC.BCTFR.A6R4.B1:BUNCH_FILL_PATTERN'
variable_spark = 'LHC@BCTFR@A6R4@B1:BUNCH_FILL_PATTERN'

t1 = tstart.tz_convert('UTC').tz_localize(None)
t2 = tend.tz_convert('UTC').tz_localize(None)

# --- get the data

ds = DataQuery.builder(spark).byVariables().system("CMW").startTime(t1).endTime(t2).variable(variable).buildDataset()

auxdf = ds.select('nxcals_timestamp','nxcals_value.elements').withColumnRenamed('nxcals_timestamp','timestamp') \
.withColumnRenamed('elements',variable_spark)

print('\n\nThis is the result:\n')
print(auxdf.count())
```


---

## Install your own NXCALS bundle

If you want to install your own bundle you can follow the following steps.

### Install miniconda

Start with a miniconda installation as minimal set. Follow the installation instructions from the [conda web page](https://docs.conda.io/en/latest/miniconda.html#linux-installers) and [linux installation](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html)

- download the [Miniconda3 Linux 64bit](https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh)
- execute it with 
    ```bash Miniconda-latest-Linux-x86_64.sh```
    and follow the installer prompts
- use the ==`~lumimod/public/miniconda3`== as the installation directory
- removed the conda initialization lines from .bashrc and put them in a separate file (see below)

### Install nxcals bundle

Follow the instructions from [NXCALS Documentation](http://nxcals-docs.web.cern.ch/current/). Navigate to:
> Public APIs > Data Access Methods > NXCALS Spark bundle 

Created the installation script `install_nxcals.sh` 
```
#!/bin/bash

curl -s -k -O http://photons-resources.cern.ch/downloads/nxcals_pro/spark/spark-nxcals.zip
unzip spark-nxcals.zip
rm spark-nxcals.zip
cd spark-*-bin-hadoop2.7
```

and install the software in `~/lumimod/public/nxcals` (to replace with your desired path) directory.

To remain compatible with NXCALS installation in SWAN, you can configure the python environment as LCG95. Create a minimal set for our needs in `lcg95_basic.txt`

```
pandas==0.23.3
numpy==1.14.2
matplotlib==2.2.2
pyarrow==0.8.0
```
Create the environment with:
```
conda create -n nxcals-lcg95-env --file lcg95_basic.txt
```
Then to use it with the commands:

```
conda env list                     ! list the available environments
conda activate nxcals-lcg95-env    ! activate an environment
conda deactivate                   ! when done to exit the environment 
```

That's it.