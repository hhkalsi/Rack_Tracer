# Rack_Tracer
We have enclosed Rack_Tracer_module(python script) and initialization.json file.

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
