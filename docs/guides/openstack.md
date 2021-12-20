# Openstack virtual machines

## Introduction
Virtual machines can be created using CERN's cloud services.

The service is available at https://openstack.cern.ch/

Detailed documentation from CERN's IT department is available at:

https://clouddocs.web.cern.ch/index.html

In the following we will provide simple recipes for crating and accessing Windows or Linux Virtual Machines.

## Creating a Windows Virtual machine accessible from outside CERN

*(Prepared by G. Sterbini and G. Iadarola)*

 - You can create your Windows Virtual Machine using the [Openstack web interface](https://openstack.cern.ch/) by following [these instructions](https://clouddocs.web.cern.ch/tutorial_using_a_browser/create_a_windows_virtual_machine.html).
 - To access from outside CERN, ssk for a direct connection following [these instructions](https://espace.cern.ch/winservices-help/Terminal%20Services/Remote%20Desktop%20Gateway/Pages/Configuring-remote-connection-via-Remote-Desktop-Gateway.aspx). After ~5 min you should receive the confirmation that your machine is setup.
 - You can connect to the machine using Windows Remote Desktop (tested on Version 10), by opening the file provided by the previous step (remode desktop shortcut). 

Form inside the virtual machine, you can access also linux computers and services (e.g. lxplus), including those accessible only from inside CERN. The most efficient way is to use Start X-Win32 that can be installed using the CMF package installer from the CERN NICE services (https://winservices.web.cern.ch/winservices/).

## Other Operating Systems
 - [CentOS CC7](openstackCC7.md)
 - [CentOS CS8](openstackCS8.md)




