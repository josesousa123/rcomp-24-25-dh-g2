ISP -> 87.5.127.205 /30
255.255.255.252 = 30

PC1-B2-F0 -> 10.24.38.10 /25
PC2-B2-F0 -> 10.24.38.20 /25

PC3-B2-F1 -> 10.24.37.130 /25
PC4-B2-F1 -> 10.24.37.140 /25

Laptop1-B2-F0 -> 10.24.36.10 /24
Laptop2-B2-F1 -> 10.24.36.20 /24

Server-B2-F0 -> 10.24.38.130 /26

Router-Backbone -> 10.24.32.1 /24
Router-B2 -> 

default gateways
B2-F0 -> 10.24.38.1 /25
B2-F1 -> 10.24.37.129 /25
B2-WIFI -> 10.24.36.1 /24
B2-DMZ -> 10.24.38.129 /26
B2-VoIP -> 10.24.37.1 /25

255.255.255.0 = 24
255.255.255.128 = 25
255.255.255.192 = 26

B1-PC1 -> 10.24.33.200 /26
PC2 -> 10.24.33.130 /26

10.24.44.1 -> RT-BK
10.24.44.2 -> RT-B1
10.24.44.3 -> RT-B2
10.24.44.4 -> RT-B3

FastEthernet1/0.390    10.24.44.3      YES manual up                    up
FastEthernet1/0.396    10.24.38.1      YES manual up                    up 


Vlan390                10.24.44.1      YES manual up                    up
Vlan391                10.24.33.193    YES manual up                    up
Vlan392                10.24.33.129    YES manual up                    up
Vlan393                10.24.32.129    YES manual up                    up
Vlan394                10.24.32.1      YES manual up                    up
Vlan395                10.24.33.1      YES manual up                    up
Vlan396                10.24.38.1      YES manual up                    up
Vlan397                10.24.37.129    YES manual up                    up
Vlan398                10.24.36.1      YES manual up                    up
Vlan399                10.24.38.129    YES manual up                    up
Vlan400                10.24.37.1      YES manual up                    up
Vlan401                10.24.43.1      YES manual up                    up
Vlan402                10.24.42.1      YES manual up                    up
Vlan403                10.24.40.1      YES manual up                    up
Vlan404                10.24.43.129    YES manual up                    up
Vlan405                10.24.41.1      YES manual up                    up