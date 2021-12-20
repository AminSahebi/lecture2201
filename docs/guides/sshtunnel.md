# SSH tunnel to browse CERN internal websites


In the following you find a few options to access web pages as from the CERN General Public Network while being outside CERN.

According to [CERN recommendations](https://security.web.cern.ch/recommendations/en/ssh_tunneling.shtml) `lxtunnel.cern.ch`
is to be preferred over `lxplus.cern.ch` for tunneling, as this is its only purpose while `lxplus` provides a fully usable
environment.

## Using sshuttle

`sshuttle` allows forwarding of specific connections through the CERN network. It requires some configuration to forward the correct connections:

=== "from Davide"

    ```bash
    #!/bin/sh
    # From https://codimd.web.cern.ch/vjC8BHbTS7etHwJve-K2Uw
    case $1 in
        connect)
            sshuttle --dns -v --remote dgamba@lxplus.cern.ch 128.141.0.0/16 128.142.0.0/16 137.138.0.0/16 172.18.0.0/16 185.249.56.0/22 188.0.0.0/8 192.65.196.0/23 192.91.242.0/24 194.12.128.0/18 2001:1458::/32 2001:1459::/32 --daemon --pidfile /tmp/sshuttle.pid
            shift
        ;;
        disconnect)
            kill `cat /tmp/sshuttle.pid`
            shift
        ;;
        *)
            # unknown option
            echo  "Unknown option\nUsage:"
            echo  "\t $0 connect : to start VPN-like connection to CERN"
            echo  "\t $0 disconnect : to stop it"
    ;;
    esac
    ```

=== "from Riccardo"

    ```bash
    #!/bin/bash
    kinit

    IP=`host lxtunnel.cern.ch | awk 'NR==2 {print $4}'`
    echo $IP

    sshuttle --dns  -x $IP --remote=$IP \
    --pidfile /tmp/sshuttle.pid --python=python \
    --ssh-cmd 'ssh -o GSSAPIAuthentication=yes -o GSSAPIDelegateCredentials=yes'  \
            10.0.0.0/8      \
            100.64.0.0/10   \
            10.100.0.0/16   \
            10.254.0.0/16   \
            10.76.0.0/15    \
            128.141.0.0/16  \
            128.142.0.0/16  \
            137.138.0.0/16  \
            172.16.0.0/12   \
            185.249.56.0/22 \
            188.184.0.0/15  \
            188.184.0.0/16  \
            188.185.0.0/15  \
            188.185.0.0/16  \
            192.16.155.0/24 \
            192.16.156.0/22 \
            192.16.160.0/22 \
            192.16.164.0/23 \
            192.16.166.0/24 \
            192.65.183.0/24 \
            192.65.184.0/21 \
            192.65.192.0/22 \
            192.65.196.0/23 \
            192.91.236.0/22 \
            192.91.240.0/22 \
            192.91.242.0/24 \
            192.91.244.0/23 \
            192.91.246.0/24 \
            194.12.128.0/18
    ```

## SSH tunnel through lxplus/lxtunnel

*(from cern.ch/bblumi)*

you can use the following can create an ssh tunnel through the [lxplus service](https://information-technology.web.cern.ch/services/lxplus-service). 
This can be useful to access wikis.cern.ch, timber.cern.ch, issues.cern.ch, ect.

You can used SSH to create the tunnel (in a terminal):

=== "lxtunnel"

    ```bash
    ssh -D 8888 lxtunnel.cern.ch
    ```

=== "lxplus"

    ```bash
    ssh -D 8888 lxplus.cern.ch
    ```

Then set as SOCKS proxy in your network configuration `localhost:8888`. 

??? note "Other OS"
    On MacOS 10.15 this is done by `(System Preferences) -> Network -> Advanced -> Proxies`.

    It should be easy also on other operative systems, please Google :-)

!!! note "Hint: Browser Plugins"
    To only forward certain webpages through this tunnel, one can use browser plugins like `SwitchyOmega` 
    (for [Chrome](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif?hl=en), [FireFox](https://addons.mozilla.org/en-US/firefox/addon/switchyomega/)) 
    which allow you manual filtering.

---

Often we need to access our pc at CERN from the internet via 'lxplus'. To avoid to make two ssh's you can configure a new host by adding these lines on '~/.ssh/config':

!!! note "Hint: One Time Command"
    If you only want to connect once and not change your ssh-config, you can use
    
    ```bash
    ssh -J my_nice_username@lxtunnel.cern.ch my_local_username@my_office_pc.cern.ch
    ```


=== "via ProxyJump"
    ```bash
    Host lxtunnel
      HostName lxtunnel.cern.ch
      User my_nice_username

    Host office_cern
      User my_local_username
      HostName my_office_pc.cern.ch
      ProxyJump lxtunnel
    ```

=== "via ProxyCommand"

    ```bash
    Host lxtunnel
      HostName lxtunnel.cern.ch
      User my_nice_username

    Host office_cern
      ProxyCommand ssh -q lxtunnel nc my_office_pc.cern.ch 22
    ```

where you have to replace `my_nice_username`, `my_local_username` and `my_office_pc`.

And then simply type from the terminal
```bash
ssh office_cern
```

In that case first you need to enter you `my_nice_username` and `my_office_pc` passwords,
unless you delegate your Kerberos Credentials (for more details see again [CERN recommendations](https://security.web.cern.ch/recommendations/en/ssh_tunneling.shtml))
and/or have a [public key authentication](https://serverpilot.io/docs/how-to-use-ssh-public-key-authentication/) for your office-pc set up.

!!! note "ssh-config example"

    ```bash 
    # Delegate Kerberos credentials to all things CERN
    Host *.cern.ch lxplus lxplus? lxtunnel cs-ccr-dev? cs-ccr-optics? dev? optics?  
      User my_nice_username
      GSSAPITrustDns yes
      GSSAPIAuthentication yes
      GSSAPIDelegateCredentials yes
      ServerAliveInterval 60

    # shorthands, e.g. `ssh lxplus` `ssh lxplus8`
    Host lxplus? lxplus lxtunnel cs-ccr-dev? cs-ccr-optics?
      Hostname %h.cern.ch
    
    # shorthands, e.g. `ssh dev3`
    Host dev? optics?
      Hostname cs-ccr-%h.cern.ch

    # connect to office from inside GPN
    Host *office_cern
      HostName my_office_pc.cern.ch
      User my_local_username
      IdentityFile path_to_office_pc_private_key  # remove if not set up

    # connect to office from home
    Host extern_*
      ProxyJump lxplus.cern.ch
    ```

    Then you can connect from the GPN via `ssh office_cern` and from home `ssh extern_office_cern`.

    !!! warning 
        `ssh extern_dev3` will not work with this setup, as this will try to resolve `cs-ccr-extern_dev3.cern.ch` 

See also more info on the [ssh config file](https://linuxize.com/post/using-the-ssh-config-file/).

