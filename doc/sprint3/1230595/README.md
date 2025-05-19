# BUILDING 3 INFORMATION

## 1. OSPF dynamic routing

* Existing static routing tables on building 3 were erased.

### **Building 3 OSPF**:

```
router ospf 1
  router-id 10.24.44.4
  network 10.24.44.0 0.0.0.255 area 0
  network 10.24.40.0 0.0.3.255 area 3
```

## 2. HTTP servers

* **Server-HTTP-B3-F0:** `10.24.43.145 /26`

## 3. DHCPv4 service

### Excluded Addresses

```
ip dhcp excluded-address 10.24.43.1
ip dhcp excluded-address 10.24.42.1
ip dhcp excluded-address 10.24.40.1
ip dhcp excluded-address 10.24.43.129 10.24.43.190
ip dhcp excluded-address 10.24.41.1
```

### DHCP Pools

* **Floor 0 (VLAN 401):**

  ```
  ip dhcp pool b3-f0
      default-router 10.24.43.1
      network 10.24.43.0 255.255.255.128
      dns-server 10.24.43.135
      domain-name building-3.rcomp-24-25-dh-g2
  exit
  ```

* **Floor 1 (VLAN 402):**

  ```
  ip dhcp pool b3-f1
      default-router 10.24.42.1
      network 10.24.42.0 255.255.255.0
      dns-server 10.24.43.135
      domain-name building-3.rcomp-24-25-dh-g2
  exit
  ```

* **Wi-Fi (VLAN 403):**

  ```
  ip dhcp pool b3-wifi
      default-router 10.24.40.1
      network 10.24.40.0 255.255.255.0
      dns-server 10.24.43.135
      domain-name building-3.rcomp-24-25-dh-g2
  exit
  ```

* **DMZ (VLAN 404):**

    * **no DHCP pool** (all addresses static)

* **VoIP (VLAN 405):**

  ```
  ip dhcp pool b3-voip
      default-router 10.24.41.1
      network 10.24.41.0 255.255.255.0
      dns-server 10.24.43.135
      domain-name building-3.rcomp-24-25-dh-g2
      option 150 ip 10.24.41.1
  exit
  ```

## 4. VoIP service

### Telephony service

* Switches connected to IP Phones configuration

  ```
  switchport mode access
  switchport voice vlan 405
  no switchport access vlan
  ```

* Automatic phone registration and directory number assignment

  ```
  telephony-service
      ip source-address 10.24.41.1 port 2000
      max-ephones 20
      max-dn 20
      auto assign 1 to 2
  exit

  ephone-dn 1
      number 3001
  exit

  ephone-dn 2
      number 3002
  exit
  ```

### Call Forwarding

* Building 1 (extensions 1...)

  ```
  dial-peer voice 1 voip
      destination-pattern 1...
      session target ipv4:10.24.44.2
  exit
  ```
* Building 2 (extensions 2...)

  ```
  dial-peer voice 2 voip
      destination-pattern 2...
      session target ipv4:10.24.44.3
  exit
  ```
* Building 3 (extensions 3...)

  ```
  dial-peer voice 3 voip
      destination-pattern 3...
      session target ipv4:10.24.44.4
  exit
  ```

### **Calling IP\_Phone2 (3002) with IP\_Phone1 (3001)**:

![b3-voip-service](./config/b3-voip-service.png)

## 5. DNS

* **Server-DNS-B3-F0:** `10.24.43.135 /26`
* **DNS Domain Name:** `rcomp-24-25-dh-g2`
* **DNS Local Domain Name:** `building-3.rcomp-24-25-dh-g2`

## 6. NAT (Network Address Translation)

### Interface configuration

```
interface FastEthernet1/0.401
    ip nat inside
    exit
interface FastEthernet1/0.402
    ip nat inside
    exit
interface FastEthernet1/0.403
    ip nat inside
    exit
interface FastEthernet1/0.404
    ip nat inside
    exit
interface FastEthernet1/0.405
    ip nat inside
    exit

interface FastEthernet1/0.390
    ip nat outside
    exit
```

## Redirection

```
# Redirect HTTP/HTTPS requests to our internal HTTPS server
ip nat inside source static tcp 10.24.43.145 80 10.24.44.4 80
ip nat inside source static tcp 10.24.43.145 443 10.24.44.4 443

# Redirect DNS requests to our internal DNS server
ip nat inside source static tcp 10.24.43.135 53 10.24.44.4 53
ip nat inside source static udp 10.24.43.135 53 10.24.44.4 53
```

## 7. Static Firewall (ACLs)

