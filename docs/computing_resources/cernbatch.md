# HTCondor batch system

Computing jobs that run on individual nodes with up to 32 CPU cores per node can be submitted to the CERN batch service (lxbatch). The jobs are submitted and managed using the HTCcondor platform.

### Access

All users having access to the CERN linux service and the AFS filesystem (which can be self-enabled at https://resources.web.cern.ch) can submit jobs to HTCondor, but have by default rather low priority.

ABP users working on computationally intensive tasks can be granted higher priority, by being added to one of the following e-groups (based on their section):

| Section name  | e-group name    |
| ------------- | ----------------|
| BE-ABP-CEI    | batch-u-abp-cei |
| BE-ABP-HSL    | batch-u-abp-hsl |
| BE-ABP-INC    | batch-u-abp-inc |
| BE-ABP-LAF    | batch-u-abp-laf |
| BE-ABP-LNO    | batch-u-abp-lno |
| BE-ABP-NDC    | batch-u-abp-ndc |

The section leaders and the [ABP-CP members](../abpcp.md#members) have admin rights to add users to the e-group of their section. All these e-groups are mapped to a single computing group called “group_u_BE.ABP.NORMAL”.


## Usage

Detailed documentation managed by the IT department can be found here:

https://batchdocs.web.cern.ch/index.html

A quick start guide can be found here:

https://batchdocs.web.cern.ch/local/quick.html


GUIs for monitoring the clusters can be found here:

https://batch-carbon.cern.ch/grafana/dashboard/db/user-batch-jobs

https://batch-carbon.cern.ch/grafana/dashboard/db/cluster-batch-jobs

https://monit-grafana.cern.ch/d/000000865/experiment-batch-details

https://monit-grafana.cern.ch/d/000000868/schedds


### GPUs

Graphics Processing Units are available in the system. To use GPUs please follow the instructions available here:

https://batchdocs.web.cern.ch/tutorial/exercise10.html

An example submit file is:

```
executable  = job_name/job_name.sh
arguments = $(ClusterId) $(ProcId)
output = job_name/htcondor.out
error = job_name/htcondor.err
log = job_name/htcondor.log
transfer_input_files = job_name
requirements = regexp("V100", Target.CUDADeviceName)
request_GPUs = 1
request_CPUs = 1
+MaxRunTime = 86400
queue
```

The line `requirements = regexp("V100", Target.CUDADeviceName)` will find nodes that only have a V100 GPU. Nodes with T4 GPUs also exist.

### Nodes with large memory

Some nodes are equipped with a larger number of cores and memory, namely (31 Oct 2019):
 - a few nodes with 24 physical cores and 1Tb of memory
 - 6 nodes with 48 cores (hyperthreaded) and 512Gb of memory

These can be used via HTCondor by adding the appropriate lines to the submit file, e.g.:
```
RequestCpus           = 24
+BigMemJob = True
```
Members of the accounting group group_u_BE.ABP.NORMAL should have access to run on these nodes. Access can be granted to other users in the group.

### Specific applications

Example on how HTCondor is used to manage PyECLOUD, PyHEADTAIL and PLACET simulations can be found here:

https://indico.cern.ch/event/637703/contributions/2583365/

https://indico.cern.ch/event/580885/contributions/2355043/

https://twiki.cern.ch/twiki/pub/ABPComputing/Placet/Run_placet_on_HTCondor.pdf

## For administrators

The shares of the different groups can be monitored on https://haggis.cern.ch/ (available only inside the CERN network).
Search for "be" to see our shares.

## FAQs

### Scheduler Not Replying

From time to time it happens that the scheduler does not reply. 
In general, it is a temporary problem; if this is not the case, open [IT ticket](https://cern.service-now.com/service-portal/help.do?t=inc){target="_blank"}.
At the same time, you may try changing the scheduler you are assigned by default.
This can be accomplished by one of two ways:

1. setting the two environment variables:  `_condor_SCHEDD_HOST` and `_condor_CREDD_HOST`.
    E.g.:

    === "tcsh"

        ```tcsh
        setenv _condor_SCHEDD_HOST bigbird02.cern.ch
        setenv _condor_CREDD_HOST bigbird02.cern.ch
        ```

    === "bash"

        ```bash
        export _condor_SCHEDD_HOST="bigbird02.cern.ch"
        export _condor_CREDD_HOST="bigbird02.cern.ch"
        ```

    In the output of a simple call to `condor_q` you can find the scheduler name. If you don't set these variables, the reported scheduler name is the one assigned to you by default; otherwise, you should find the one that you have set via the previous variables.

    Please keep in mind that these statements, if typed on terminal, will apply only to that session.
    For instance, in case you log out or the `lxplus` session expires, you have to re-set those two variables if you want them also in the new session.
    So, please remember the scheduler that you have requested, otherwise you won't be able to retrieve the results form `HTCondor`.
  
  2. Calling `condor` commands with `-name` parameter.
    You can use another than your defined schedular by addressing it directly in your commands, e.g.

    ```shell
    condor_q -name bigbird15.cern.ch
    ```

    This should work for any of the `condor`-commands (e.g. `condor_q`, `condor_submit`, etc.). The scheduler is then used only for this command.

### Jobs Being Taken Very Slowly


It may happen that you see your jobs queueing for too long. This might be simply due to overload of the batch system (please check the [batch GUI](#queue-gui)); more rarely, it can be also a problem with priorities. Indeed, it may happen that your jobs are assigned (by mistake) an accounting group with very low priority. 

Hence, you can check if your jobs are assigned the wrong accounting group via (an example output is shown):

```bash
$ condor_q owner $LOGNAME -long | grep '^AccountingGroup' | sort | uniq -c
9 AccountingGroup = "group_u_ATLAS.u_zp.nkarast"
1496 AccountingGroup = "group_u_BE.UNIX.u_pz.nkarast"
```

You can force the use of the high priority accounting group modifying your `` .sub `` script as:
```bash
+AccountingGroup = "group_u_BE.ABP.NORMAL"
```

## Advanced features

### Spool Option

The `` -spool `` option can be used at `` condor_submit `` level, e.g.

```bash
condor_submit -spool htcondor.sub
```

In this case, all the output files (`` transfer_output_files ``) and the `` error ``, `` log `` and `` output `` files are _not_ generated once the jobs finishes, but only when requested by the user, after the job is over. Retrieval can be done via the following command:

```bash
condor_transfer_data $LOGNAME -const 'JobStatus == 4'
```

In the above example, the files from all completed job in each cluster will be retrieved.

In this case, the jobs may not automatically disappear from `` condor_q ``. Job removal takes place after 10 days the job has finished.



### Submitting Jobs to HTCondor from a local Machine

The recommended way of using HTCondor is to submit jobs by logging to lxplus.cern.ch.

It is also possible to configure your own computer to manage HTCondor jobs, as described in [this guide](../guides/htcondor.md). 
