# Rack-Tracer
===================
Rack-Tracer module automatically updates the rack-awareness configuration in a hadoop cluster. This module generates an IP address to rack id mapping on regular intervals. This mapping is part of the configuration that makes a hadoop cluster rack-aware.

## INSTALLATION

In order to install this extension:
- copy 'Rack-Tracer' and 'initialization.json' to /mnt/flash
- enable the Command API interface:

```
management api http-commands
    no shutdown
```

The following are the parameters of the initialization.json file which must be entered before running the script

* Username_server  is the username used to access the server
* Rack_ID is the rack id in which the server is present
* Ip_address_server is the ip-address of the server
* Login_switch is the username to access the switch
* Password_switch is the password to access the switches
* File_path is the location of rack-topology.data and Locktest.txt
* Rack_topology_file is the name of the file which has server's ip address to rack-id mapping
* Lockets.txt is the file which has the state of the script whether it is locked or unlocked
* Wait_time is the random amount of time a file waits before accessing the Locktest.txt file.data
* Sleep_time is the amount of time after which a script runs periodically
* vServer_no is the number of virtual servers running on the host machine

```
  {
    "Rack_ID" : "India-BLR-Tower-A-01",
    "Username_server" : "hduser",
    "IPaddress_server" : "10.85.25.151",
    "Login_switch" : "admin",
    "Password_switch" : "admin" ,
    "File_path" : "/usr/local/hadoop/etc/hadoop/",
    "Rack_topology_file" : "rack-topology.data",
    "Lockfile" : "Locktest.txt",
    "Wait_time" : "10",
    "Sleep_time" : "20",
    "vServer_no" : "2",
    }
```
Copy the 'Locktest.txt' and 'rack-topology.data' to the namenode 
Rack-Tracer can then be started using any of the following methods:

1 - Execute directly from bash (from the switch, or a remote
    switch/server running Python):

```
(bash)# /mnt/flash/Rack-Tracer
```

2 - Configure an alias on the switch:

```
(config)# alias Rack-Tracer bash /mnt/flash/Rack-Tracer
```



## ASSUMPTIONS

* The switch is compatible with JSON format and supports Python programming language and eAPI is enabled.
* LLDP protocol should be enabled on all the hosts and the switches.
* Authentication ssh keys of the switches should be present on the hosts.
* Each host has a IP address.
* The topology follows the leaf-spine architecture.
* User configures the parameter correctly.
* The module is present on the TOR switch before starting the rack-aware HDFS.
* The configuration file (rack-topology.data) is already present on the Namenode.
* The file for accessing the critical section(Locktest.txt) should be present on the server.

## COMPATIBILITY 
Version 1.0 has been developed using Python and JSON. It is tested on Arista's switches that support eapi.
but should work on any system supporting Python 2.6 or
later. Please reach out to support@aristanetworks.com for
assistance if needed.

## LIMITATIONS

Any stale IP address is not removed by the module.
This module is designed for only rack-aware Hadoop cluster. It does not work on all computational clusters.
