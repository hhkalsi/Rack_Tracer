# Rack_Tracer
===================
Rack-Tracer module automatically updates the ip address to rack mapping in the rack-awareness configuration on the namenode in a hadoop cluster.

## INSTALLATION
In order to install this extension:
- copy 'RackTracer' and 'initialization.json' to /mnt/flash
- enable the Command API interface:

```
management api http-commands
    no shutdown
```

Change Rack_ID, Username_server, IPaddress_server Login_switch, Password_switch, File_path and other parameters in initialization.json file to the ones appropriate for your installation.

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
"Kindly note" : "Username of the user in the server, IPaddress of the server, File location of this file on the server, User Login of the switch, Password of the switch, Wait_time is the range for random time the switch will wait before access the Lockfile"
}
```

portAuto can then be started using any of the following methods:

1 - Execute directly from bash (from the switch, or a remote
    switch/server running Python):

```
(bash)# /mnt/flash/portAuto
```

2 - Configure an alias on the switch:

```
(config)# alias portAuto bash /mnt/flash/portAuto
```

3 - Schedule a job on the switch:
    e.g.: In order to run portAuto every 12 hours, use:We have enclosed Rack_Tracer_module(python script) and initialization.json file.

The following are the parameters of the initialization.json file which must be entered before running the script

Username_server  is the username used to access the server
Rack_ID is the rack id in which the server is present
Ip_address_server is the ip-address of the server
Login_switch is the username to access the switch
Password_switch is the password to access the switches
File_path is the location of rack-topology.data and Locktest.txt
Rack_topology_file is the name of the file which has server's ip address to rack-id mapping
Lockets.txt is the file which has the state of the script whether it is locked or unlocked
Wait_time is the random amount of time a file waits before accessing the Locktest.txt file.data
Sleep_time is the amount of time after which a script runs periodically
vServer_no is the number of virtual servers running on the host machine


Assumptions

The switch is compatible with JSON format and supports Python programming language and eAPI is enabled.
LLDP protocol should be enabled on all the hosts and the switches.
Authentication ssh keys of the switches should be present on the hosts.
Each host has a IP address.
The topology follows the leaf-spine architecture.
User configures the parameter correctly.
The module is present on the TOR switch before starting the rack-aware HDFS.
The configuration file (rack-topology.data) is already present on the Namenode.
The file for access the critical section(Locktest.txt) should be present on the server.

Constraints and Tradeoffs

Any stale IP address is not removed by the module.
This module is designed for only rack-aware Hadoop cluster. It does not work on all computational clusters.
