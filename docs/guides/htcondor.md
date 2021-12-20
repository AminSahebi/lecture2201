# Submitting Jobs to HTCondor from a local Machine

The recommended way of using HTCondor is to submit jobs by logging to lxplus.cern.ch.

It is also possible to configure your own computer to manage HTCondor jobs, as described in this guide.

These notes refer to Ubuntu 16.04 LTS, 18.04 LTS and 20.04 LTS and includes possible caveats. If you have a different Linux distribution, steps might be the same, but syntax may change. Sudo rights are needed.

As pre-requisite, you will need to install a `kerberos` client on your desktop; afterwards, you can proceed with the installation of `HTCondor`



## Install `kerberos`

install user and developer packages and add lxplus credential components (when asked, default realm is `CERN.CH`): 
  
```shell
sudo apt install krb5-user libkrb5-dev libauthen-krb5-perl

scp $USERNAME@lxplus.cern.ch:/usr/bin/batch_krb5_credential .
chmod +x batch_krb5_credential 
sudo mv batch_krb5_credential /usr/bin/

scp $USERNAME@lxplus.cern.ch:/etc/ngauth_batch_crypt_pub.pem .
sudo mv ngauth_batch_crypt_pub.pem /etc/

scp $USERNAME@lxplus.cern.ch:/etc/krb5.conf.no_rdns .
sudo mv krb5.conf.no_rdns /etc/krb5.conf.no_rdns

scp $USERNAME@lxplus.cern.ch:/etc/sysconfig/ngbauth-submit .
sudo mkdir /etc/sysconfig/
sudo mv ngbauth-submit /etc/sysconfig/
```
  
## Confirm installation

Before this step make sure you have valid credentials already (i.e. run `kinit`).
Then check that the `kerberos` components are properly installed and set-up (the script will tell you the missing `perl` packages): 
  
```shell
/usr/bin/batch_krb5_credential
```

There should be an output like: 

```shell
-----BEGIN NGAUTH COMPOSITE-----
# LOTS OF LINES OF YOUR KEY

-----END NGAUTH COMPOSITE-----
```

and nothing else (i.e. no missing files or errors).

## Debugging the `kerberos` installation

if the last step does not deliver the desired output, `/usr/bin/batch_krb5_credential` might have to be modified.
Some things can be tried:

1. change the line

    ```bash
    my $principalName = "ngauth/SOMESERVER";
    ```

    into

    ```bash
    my $principalName = "ngauth/ngauth.cern.ch"; 
    ```

2. install missing `` perl `` components: 
  
    ```shell
    perl -MCPAN -e 'install Authen::Krb5'
    ```

3. on Ubuntu 20.04 neither of these steps helped, as the `Authen:Krb5` package was not available.
    Try getting a new version of `batch_krb5_credential` directly from `lxplus8`:

    ```bash
    scp $USERNAME@lxplus8.cern.ch:/usr/bin/batch_krb5_credential .
    chmod +x batch_krb5_credential 
    sudo mv batch_krb5_credential /usr/bin/
    ```

4. or try manual fix  of `Authen:Krb5` issue by replacing the lines:

    ```bash
    my $newCreds = Authen::Krb5::cc_resolve("FILE:".$tgt_fn);
    $newCreds->initialize($credCache->get_principal());
    Authen::Krb5::cc_copy_creds($credCache, $newCreds);
    ```

    with

    ```bash
    copy($tgt, $tgt_fn);
    ```



## Install `HTCondor`

On Ubuntu 18.04+ it is usually enough to install condor from the packaged version

=== "Ubuntu 20.04"
  
    ```shell
    sudo apt update
    sudo apt install htcondor
    ```

=== "Ubuntu 18.04"
  
    ```shell
    sudo apt-get update
    sudo apt-get install condor
    ```

If you need a more recent version, or in case of Ubuntu 16.04, use the resources on the [web-page of `HTCondor`](https://research.cs.wisc.edu/htcondor/instructions/){target="_blank"}.

## Debugging the `HTCondor` installation

It may happen that at `sudo apt-get update`, you get the error message:

```bash
N: Skipping acquire of configured file 'contrib/binary-i386/Packages' as repository 'http://research.cs.wisc.edu/htcondor/ubuntu/stable trusty InRelease' doesn't support architecture 'i386'
```

In case your system is actually 64bit, a common solution is to limit the research of the package distro to just 64 bit by introducing the `` [arch=amd64] `` in the list of sources (in `` /etc/apt/sources.list ``), e.g.

```shell
deb [arch=amd64] http://research.cs.wisc.edu/htcondor/ubuntu/stable/ trusty contrib
```

## Configure `HTCondor`

1. create the config file `/etc/condor/config.d/10-local.config`.

    Please set as scheduler (`SCHEDD_HOST`) the default one you get on `lxplus`, e.g. in your `condor_q` output.
    You can also find it out by running (on `lxplus`):

    ```shell
    condor_config_val SCHEDD_HOST
    ```

    An example content is provided here:
  
    ```bash
    CONDOR_HOST = tweetybird03.cern.ch, tweetybird04.cern.ch
    COLLECTOR_HOST = tweetybird03.cern.ch, tweetybird04.cern.ch
    SCHEDD_HOST = bigbirdXX.cern.ch
    SCHEDD_NAME = $(SCHEDD_HOST)
    SEC_CLIENT_AUTHENTICATION_METHODS = KERBEROS
    SEC_CREDENTIAL_PRODUCER = /usr/bin/batch_krb5_credential
    CREDD_HOST = $(SCHEDD_HOST)
    FILESYSTEM_DOMAIN = cern.ch
    UID_DOMAIN = cern.ch
    ```
  
2. restart `HTCondor`:
  
    ```shell
    /etc/init.d/condor restart
    ```
  
## Debugging the `HTCondor` configuration

1. Useful: The full configuration can be checked by
   
    ```shell
    condor_config_val -dump
    ```

2. If you have connection problems when running `condor_q` or `condor_status`, you might want to check your `NETWORK_INTERFACE`.

    ```shell
    condor_config_val NETWORK_INTERFACE
    ```

    In some cases it might be set to `127.0.0.1` or similar. Yet it should be set to `*`.
    If this is not the case, simply add the appropriate line at the end of your configuration file (from above):

    ```bash
    NETWORK_INTERFACE = *
    ```

    Don't forget to restart `HTCondor`.

3. Pay attention to the couple `COLLECTOR_HOST` and `SCHEDD_HOST`, as, depending on the collector, you may be able to reach only a sub-set of the scheduler.
   To get the whole lists, please login to `lxplus.cern.ch` and type:

    === "schedulers"

        ```shell
        condor_status -sched 
        ```

    === "collectors"

        ```shell
        condor_status -collector
        ```
