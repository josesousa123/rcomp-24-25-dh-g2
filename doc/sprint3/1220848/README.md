# BUILDING 2 INFORMATION

## 1. OSPF dynamic routing

- Existing static routing tables on building 2 were erased.
### **Building 2 OSPF**:
  ```
  router ospf 1
    router-id 10.24.44.3
    network 10.24.44.0 0.0.0.255 area 0
    network 10.24.36.0 0.0.3.255 area 2
  ```

## 2. HTTP servers

- **Server-HTTP-B2-F0:** `10.24.38.145 /26`

### **Home Page for Building 2**:

![b2-html-page](./config/b2-html-page.png)

## 3. DHCPv4 service

### Excluded Addresses
```
ip dhcp excluded-address 10.24.38.1
ip dhcp excluded-address 10.24.37.129
ip dhcp excluded-address 10.24.36.1
ip dhcp excluded-address 10.24.38.129 10.24.38.190
ip dhcp excluded-address 10.24.37.1
```

### DHCP Pools

- **Floor 0 (VLAN 396):**
    ```
    ip dhcp pool b2-f0
        default-router 10.24.38.1
        network 10.24.38.0 255.255.255.128
        dns-server 10.24.38.140
        domain-name building-2.rcomp-24-25-dh-g2
    exit
    ```
  
- **Floor 1 (VLAN 397):**
    ```
    ip dhcp pool b2-f1
        default-router 10.24.37.129
        network 10.24.37.128 255.255.255.128
        dns-server 10.24.38.140
        domain-name building-2.rcomp-24-25-dh-g2
    exit
    ```
  
- **Wi-Fi (VLAN 398):**
    ```
    ip dhcp pool b2-wifi
        default-router 10.24.36.1
        network 10.24.36.0 255.255.255.0
        dns-server 10.24.38.140
        domain-name building-2.rcomp-24-25-dh-g2
    exit
    ```
  
- **DMZ (VLAN 399):** 
  - **no DHCP pool** (all addresses static)
  

- **VoIP (VLAN 400):**
    ```
    ip dhcp pool b2-voip
        default-router 10.24.37.1
        network 10.24.37.0 255.255.255.128
        dns-server 10.24.38.140
        domain-name building-2.rcomp-24-25-dh-g2
        option 150 ip 10.24.37.1
    exit
    ```


## 4. VoIP service

### Telephony service

- Switches connected to IP Phones configuration
    ```
    interface <interface>
      switchport mode access
      switchport voice vlan 400
      no switchport access vlan
    ```

- Automatic phone registration and directory number assignment
    ```
    telephony-service
        ip source-address 10.24.37.1 port 2000
        max-ephones 20
        max-dn 20
        auto assign 1 to 2
    exit
    
    ephone-dn 1
        number 2001
    exit
    
    ephone-dn 2
        number 2002
    exit
    ```

### Call Forwarding

- Building 1 (extensions 1...)
    ```
    dial-peer voice 1 voip
        destination-pattern 1...
        session target ipv4:10.24.44.2
    exit
    ```
- Building 2 (extensions 2...)
    ```
    dial-peer voice 2 voip
        destination-pattern 2...
        session target ipv4:10.24.44.3
    exit
    ```
- Building 3 (extensions 3...)
    ```
    dial-peer voice 3 voip
        destination-pattern 3...
        session target ipv4:10.24.44.4
    exit
    ```

### **Calling IP_Phone2 (2002) with IP_Phone1 (2001)**:

![b2-voip-service](./config/b2-voip-service.png)


## 5. DNS

- **Server-DNS-B2-F0:** `10.24.38.140 /26`
- **DNS Domain Name:** `rcomp-24-25-dh-g2`
- **DNS Local Domain Name:** `building-2.rcomp-24-25-dh-g2`

### **DNS Records for Building 2**:

![b2-dns-service](./config/b2-dns-service.png)

## 6. NAT (Network Address Translation)

### Interface configuration
```
interface FastEthernet1/0.396
    ip nat inside
    exit
interface FastEthernet1/0.397
    ip nat inside
    exit
interface FastEthernet1/0.398
    ip nat inside
    exit
interface FastEthernet1/0.399
    ip nat inside
    exit
interface FastEthernet1/0.400
    ip nat inside
    exit
    
interface FastEthernet1/0.390
    ip nat outside
    exit
```

### Redirection

#### Redirect HTTP/HTTPS requests to internal HTTPS server
```
ip nat inside source static tcp 10.24.38.145 80 10.24.44.3 80 
ip nat inside source static tcp 10.24.38.145 443 10.24.44.3 443 
```

#### Redirect DNS requests to internal DNS server
```
ip nat inside source static tcp 10.24.38.140 53 10.24.44.3 53
ip nat inside source static udp 10.24.38.140 53 10.24.44.3 53
```

## 7. Static Firewall (ACLs)

1. Block all spoofing, as far as possible. Internal spoofing from local networks, the DMZ may be excluded. External spoofing for traffic incoming from the backbone network.
2. All ICMP echo requests and echo replies are always allowed.
3. All traffic to the DMZ is to be blocked, except for the DNS service and HTTP/HTTPS services to the corresponding servers. Every traffic incoming from the DMZ is allowed.
4. All traffic directed to the router itself (with a destination IPv4 node address belonging to the router) is to be blocked, except for the traffic required for the described features to work.
5. Remaining traffic passing through the router should be allowed.

### Configuration

For Floor 0 (VLAN 396):
```
# Remove existing ACL 101
no access-list 101
# Block access to router interfaces and DMZ server
access-list 101 deny ip any host 10.24.38.1
access-list 101 deny ip any host 10.24.37.129
access-list 101 deny ip any host 10.24.36.1
access-list 101 deny ip any host 10.24.37.1
access-list 101 deny ip any host 10.24.38.129
# Allow ICMP echo replies to DMZ
access-list 101 permit icmp any 10.24.38.128 0.0.0.63 echo-reply
# Allow HTTP/HTTPS to DMZ
access-list 101 permit tcp any 10.24.38.128 0.0.0.63 eq 80
access-list 101 permit tcp any 10.24.38.128 0.0.0.63 eq 443
# Allow DNS to DMZ
access-list 101 permit tcp any 10.24.38.128 0.0.0.63 eq 53
access-list 101 permit udp any 10.24.38.128 0.0.0.63 eq 53
# Block all other traffic to DMZ
access-list 101 deny ip any 10.24.38.128 0.0.0.63
# Allow all outbound traffic from Floor 0
access-list 101 permit ip 10.24.38.0 0.0.0.127 any
# Allow DHCP traffic
access-list 101 permit udp any eq bootpc any eq bootps
# Apply ACL to Floor 0 interface
interface FastEthernet1/0.396
ip access-group 101 in
exit
```

For Floor 1 (VLAN 397):
```
# Remove existing ACL 102
no access-list 102
# Block access to router interfaces and DMZ server
access-list 102 deny ip any host 10.24.38.1
access-list 102 deny ip any host 10.24.37.129
access-list 102 deny ip any host 10.24.36.1
access-list 102 deny ip any host 10.24.37.1
access-list 102 deny ip any host 10.24.38.129
# Allow ICMP echo replies to DMZ
access-list 102 permit icmp any 10.24.38.128 0.0.0.63 echo-reply
# Allow HTTP/HTTPS to DMZ
access-list 102 permit tcp any 10.24.38.128 0.0.0.63 eq 80
access-list 102 permit tcp any 10.24.38.128 0.0.0.63 eq 443
# Allow DNS to DMZ
access-list 102 permit tcp any 10.24.38.128 0.0.0.63 eq 53
access-list 102 permit udp any 10.24.38.128 0.0.0.63 eq 53
# Block all other traffic to DMZ
access-list 102 deny ip any 10.24.38.128 0.0.0.63
# Allow all outbound traffic from Floor 1
access-list 102 permit ip 10.24.37.128 0.0.0.127 any
# Allow DHCP traffic
access-list 102 permit udp any eq bootpc any eq bootps
# Apply ACL to Floor 1 interface
interface FastEthernet1/0.397
ip access-group 102 in
exit
```

For Wi-Fi (VLAN 398):
```
# Remove existing ACL 103
no access-list 103
# Block access to router interfaces and DMZ server
access-list 103 deny ip any host 10.24.38.1
access-list 103 deny ip any host 10.24.37.129
access-list 103 deny ip any host 10.24.36.1
access-list 103 deny ip any host 10.24.37.1
access-list 103 deny ip any host 10.24.38.129
# Allow ICMP echo replies to DMZ
access-list 103 permit icmp any 10.24.38.128 0.0.0.63 echo-reply
# Allow HTTP/HTTPS to DMZ
access-list 103 permit tcp any 10.24.38.128 0.0.0.63 eq 80
access-list 103 permit tcp any 10.24.38.128 0.0.0.63 eq 443
# Allow DNS to DMZ
access-list 103 permit tcp any 10.24.38.128 0.0.0.63 eq 53
access-list 103 permit udp any 10.24.38.128 0.0.0.63 eq 53
# Block all other traffic to DMZ
access-list 103 deny ip any 10.24.38.128 0.0.0.63
# Allow all outbound traffic from Wi-Fi network
access-list 103 permit ip 10.24.36.0 0.0.0.255 any
# Allow DHCP traffic
access-list 103 permit udp any eq bootpc any eq bootps
# Apply ACL to Wi-Fi interface
interface FastEthernet1/0.398
ip access-group 103 in
exit
```

For VoIP (VLAN 400):
```
# Remove existing ACL 105
no access-list 105
# Block access to router interfaces and DMZ server
access-list 105 deny ip any host 10.24.38.1
access-list 105 deny ip any host 10.24.37.129
access-list 105 deny ip any host 10.24.36.1
access-list 105 deny ip any host 10.24.38.129
# Allow ICMP echo replies to DMZ
access-list 105 permit icmp any 10.24.38.128 0.0.0.63 echo-reply
# Allow HTTP/HTTPS to DMZ
access-list 105 permit tcp any 10.24.38.128 0.0.0.63 eq 80
access-list 105 permit tcp any 10.24.38.128 0.0.0.63 eq 443
# Allow DNS to DMZ
access-list 105 permit tcp any 10.24.38.128 0.0.0.63 eq 53
access-list 105 permit udp any 10.24.38.128 0.0.0.63 eq 53
# Block all other traffic to DMZ
access-list 105 deny ip any 10.24.38.128 0.0.0.63
# Allow all outbound traffic from VoIP network
access-list 105 permit ip 10.24.37.0 0.0.0.127 any
# Allow DHCP traffic
access-list 105 permit udp any eq bootpc any eq bootps
# Apply ACL to VoIP interface
interface FastEthernet1/0.400
ip access-group 105 in
exit
```

For Backbone (VLAN 390):
```
# Remove existing ACL 100
no access-list 100
# Block DMZ outbound traffic
access-list 100 deny ip 10.24.38.128 0.0.0.63 any
# Allow HTTP/HTTPS to DMZ
access-list 100 permit tcp any 10.24.38.128 0.0.0.63 eq 80
access-list 100 permit tcp any 10.24.38.128 0.0.0.63 eq 443
# Allow DNS to DMZ
access-list 100 permit tcp any 10.24.38.128 0.0.0.63 eq 53
access-list 100 permit udp any 10.24.38.128 0.0.0.63 eq 53

# Floor 0 access control
access-list 100 deny ip 10.24.38.0 0.0.0.127 any
access-list 100 deny ip any host 10.24.38.1
access-list 100 permit ip any 10.24.38.0 0.0.0.127

# Floor 1 access control
access-list 100 deny ip 10.24.37.128 0.0.0.127 any
access-list 100 deny ip any host 10.24.37.129
access-list 100 permit ip any 10.24.37.128 0.0.0.127

# Wi-Fi access control
access-list 100 deny ip 10.24.36.0 0.0.0.255 any
access-list 100 deny ip any host 10.24.36.1
access-list 100 permit ip any 10.24.36.0 0.0.0.255

# VoIP access control
access-list 100 deny ip 10.24.37.0 0.0.0.127 any
access-list 100 permit ip any 10.24.37.0 0.0.0.127

# Block DMZ server access
access-list 100 deny ip any host 10.24.38.129

# Allow ICMP echo replies to DMZ
access-list 100 permit icmp any 10.24.38.128 0.0.0.63 echo-reply
# Allow OSPF routing
access-list 100 permit ospf any any
# Allow access to backbone network
access-list 100 permit ip any 10.24.44.0 0.0.0.255

# Apply ACL to backbone interface
interface FastEthernet1/0.390
ip access-group 100 in
exit
```