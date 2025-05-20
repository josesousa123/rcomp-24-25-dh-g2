# Firewall Comands 

# B1 ( Router )

enable
configure terminal

interface FastEthernet1/0.390
ip access-group 100 in

access-list 100 deny ip 10.24.33.0 0.0.1.255 any
access-list 100 deny ip 10.24.32.0 0.0.0.255 any
access-list 100 permit icmp any any echo
access-list 100 permit icmp any any echo-reply
access-list 100 permit tcp any host 10.24.32.10 eq www
access-list 100 permit tcp any host 10.24.32.10 eq 443
access-list 100 permit udp any host 10.24.32.10 eq domain
access-list 100 permit udp any eq bootpc any eq bootps
access-list 100 permit udp any eq bootps any eq bootpc
access-list 100 permit ospf any any
access-list 100 permit udp any any eq tftp
access-list 100 permit tcp any any eq 2000
access-list 100 deny ip any host 10.24.44.2
access-list 100 deny ip any host 10.24.32.1
access-list 100 deny ip any host 10.24.33.1
access-list 100 permit ip any any

interface FastEthernet1/0.391
ip access-group 101 in

access-list 101 permit ip 10.24.33.192 0.0.0.63 any
access-list 101 permit icmp any any echo
access-list 101 permit icmp any any echo-reply
access-list 101 permit udp any eq bootpc any eq bootps
access-list 101 permit udp any eq bootps any eq bootpc
access-list 101 permit ospf 10.24.33.192 0.0.0.63 any
access-list 101 deny ip any host 10.24.33.193
access-list 101 permit ip any any

interface FastEthernet1/0.392
ip access-group 102 in

access-list 102 permit ip 10.24.33.128 0.0.0.63 any
access-list 102 permit icmp any any echo
access-list 102 permit icmp any any echo-reply
access-list 102 permit udp any eq bootpc any eq bootps
access-list 102 permit udp any eq bootps any eq bootpc
access-list 102 permit ospf 10.24.33.128 0.0.0.63 any
access-list 102 deny ip any host 10.24.33.129
access-list 102 permit ip any any

interface FastEthernet1/0.393
ip access-group 103 in

access-list 103 permit ip 10.24.32.128 0.0.0.127 any
access-list 103 permit icmp any any echo
access-list 103 permit icmp any any echo-reply
access-list 103 permit udp any eq bootpc any eq bootps
access-list 103 permit udp any eq bootps any eq bootpc
access-list 103 permit ospf 10.24.32.128 0.0.0.127 any
access-list 103 deny ip any host 10.24.32.129
access-list 103 permit ip any any

interface FastEthernet1/0.394
ip access-group 104 in

access-list 104 permit icmp any any echo
access-list 104 permit icmp any any echo-reply
access-list 104 permit udp any host 10.24.32.10 eq domain
access-list 104 permit tcp any host 10.24.32.10 eq 53
access-list 104 permit tcp any host 10.24.32.10 eq www
access-list 104 permit tcp any host 10.24.32.10 eq 443

interface FastEthernet1/0.395
ip access-group 105 in

access-list 105 permit ip 10.24.33.0 0.0.1.255 any
access-list 105 permit icmp any any echo
access-list 105 permit icmp any any echo-reply
access-list 105 permit udp any eq bootpc any eq bootps
access-list 105 permit udp any eq bootps any eq bootpc
access-list 105 permit ospf 10.24.33.0 0.0.1.255 any
access-list 105 deny ip any host 10.24.33.1
access-list 105 permit ip any any

end
copy running-config startup-config

# B2 ( Router )

enable
configure terminal

ip access-list extended 100
deny ip 10.24.38.0 0.0.0.127 any
deny ip 10.24.37.0 0.0.0.255 any
deny ip 10.24.36.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit tcp any host 10.24.38.10 eq www
permit tcp any host 10.24.38.10 eq 443
permit udp any host 10.24.38.10 eq domain
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf any any
permit udp any any eq tftp
permit tcp any any eq 2000
deny ip any host 10.24.44.3
deny ip any host 10.24.38.1
deny ip any host 10.24.37.1
permit ip any any
exit

ip access-list extended 101
permit ip 10.24.38.0 0.0.0.127 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.38.0 0.0.0.127 any
deny ip any host 10.24.38.1
permit ip any any
exit

ip access-list extended 102
permit ip 10.24.37.128 0.0.0.127 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.37.128 0.0.0.127 any
deny ip any host 10.24.37.129
permit ip any any
exit

ip access-list extended 103
permit ip 10.24.36.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.36.0 0.0.0.255 any
deny ip any host 10.24.36.1
permit ip any any
exit

ip access-list extended 104
permit icmp any any echo
permit icmp any any echo-reply
permit udp any host 10.24.38.10 eq domain
permit tcp any host 10.24.38.10 eq 53
permit tcp any host 10.24.38.10 eq www
permit tcp any host 10.24.38.10 eq 443
exit

ip access-list extended 105
permit ip 10.24.37.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.37.0 0.0.0.255 any
deny ip any host 10.24.37.1
permit ip any any
exit

interface FastEthernet1/0.390
ip access-group 100 in
exit

interface FastEthernet1/0.396
ip access-group 101 in
exit

interface FastEthernet1/0.397
ip access-group 102 in
exit

interface FastEthernet1/0.398
ip access-group 103 in
exit

interface FastEthernet1/0.399
ip access-group 104 in
exit

interface FastEthernet1/0.400
ip access-group 105 in
exit

end
copy running-config startup-config


# B3 ( Router )

enable
configure terminal

ip access-list extended 100
deny ip 10.24.43.0 0.0.0.127 any
deny ip 10.24.42.0 0.0.0.255 any
deny ip 10.24.41.0 0.0.0.255 any
deny ip 10.24.40.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit tcp any host 10.24.43.10 eq www
permit tcp any host 10.24.43.10 eq 443
permit udp any host 10.24.43.10 eq domain
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf any any
permit udp any any eq tftp
permit tcp any any eq 2000
deny ip any host 10.24.44.4
deny ip any host 10.24.43.1
deny ip any host 10.24.42.1
permit ip any any
exit

ip access-list extended 101
permit ip 10.24.43.0 0.0.0.127 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.43.0 0.0.0.127 any
deny ip any host 10.24.43.1
permit ip any any
exit

ip access-list extended 102
permit ip 10.24.42.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.42.0 0.0.0.255 any
deny ip any host 10.24.42.1
permit ip any any
exit

ip access-list extended 103
permit ip 10.24.40.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.40.0 0.0.0.255 any
deny ip any host 10.24.40.1
permit ip any any
exit

ip access-list extended 104
permit icmp any any echo
permit icmp any any echo-reply
permit udp any host 10.24.43.10 eq domain
permit tcp any host 10.24.43.10 eq 53
permit tcp any host 10.24.43.10 eq www
permit tcp any host 10.24.43.10 eq 443
exit

ip access-list extended 105
permit ip 10.24.41.0 0.0.0.255 any
permit icmp any any echo
permit icmp any any echo-reply
permit udp any eq bootpc any eq bootps
permit udp any eq bootps any eq bootpc
permit ospf 10.24.41.0 0.0.0.255 any
deny ip any host 10.24.41.1
permit ip any any
exit

interface FastEthernet1/0.390
ip access-group 100 in
exit

interface FastEthernet1/0.401
ip access-group 101 in
exit

interface FastEthernet1/0.402
ip access-group 102 in
exit

interface FastEthernet1/0.403
ip access-group 103 in
exit

interface FastEthernet1/0.404
ip access-group 104 in
exit

interface FastEthernet1/0.405
ip access-group 105 in
exit

end
copy running-config startup-config
