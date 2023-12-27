_42 School project, level 4_

**Узел** хост, компьютер, устройство  

**Host** any device which sends or receive traffic, it can be client or server

**Transmission Control Protocol (TCP)** a communications standard that enables application programs and devices to exchange messages over a network. 
1) Establishes a connection between a source and its destination, which remains active until communication begins.
2) Breaks data into smaller packets, while ensuring end-to-end delivery.

# Variable-length subnet masking (VLSM)

**Маска подсети** определяет по IP-адресу адрес подсети и адрес узла, не является частью IP-пакета (в отличие от IP-адреса)  
`network prefix + host identifier` = `IP`   
`11000000.10101000.0000000+1.00000010` (`192.168.1.2`)  
`11111111.11111111.1111111+0.00000000` (`255.255.254.0`) mask  
`11000000.10101000.0000000+0.00000000` (`192.168.0.0`) network address

**Classless Inter-Domain Routing (CIDR)** a method for allocating IP addresses and for IP routing (slows the growth of routing tables on routers across the Internet, slows the exhaustion of IPv4 addresses).

IPv4: network prefix  8 / 16 / 24 bits   
IPv6: interface identifier 64 bits

IPv4 CIDR blocks  
| Netmask | Netmask         | Address       | Host  
|---------|:----------------|--------------:|-------:
| /32     | 255.255.255.255 | 1             | accessible by explicit routing rules (single-host network) 
| /31     | 255.255.255.254 | 2             | no available host addresses (unusable)
| /30     | 255.255.255.252 | 4             | 2     
| /29     | 255.255.255.248 | 8             | 6     
| /28     | 255.255.255.240 | 16            | 14    
| /27     | 255.255.255.224 | 32            | 30    
| /26     | 255.255.255.192 | 64            | 62    
| /25     | 255.255.255.128 | 128           | 126   
| /24     | 255.255.255.0   | 256           | 254   
| /23     | 255.255.254.0   | 512           | 510      
| /22     | 255.255.252.0   | 1 024         | 1 022      
| /21     | 255.255.248.0   | 2 048         | 2 046  
| /20     | 255.255.240.0   | 4 096         | 4 094  
| /19     | 255.255.224.0   | 8 192         | 8 190
| /18     | 255.255.192.0   | 16 384        | 16 382 
| /17     | 255.255.128.0   | 32 768        | 32 766  
| /16     | 255.255.0.0     | 65 536        | 65 534 
| /8      | 255.0.0.0       | 16 777 216    | 16 777 214
| /0      | 0.0.0.0         | 4 294 967 296 | entire IPv4 Internet


# Client IP addresses
* Client IP do not overlap  
* Private IP  
Cannot be used to access the Internet, remains only in the local network, never leaves the LAN.  
Reserved by the Internet Assigned Numbers Authority (IANA).
If an interface is connected directly / indirectly to the internet, it cannot have an IP address in the private IP.
    + `10.0.0.0` ... `10.255.255.255`     (Class A, for large networks,   8 network + 24 host)
    + `172.16.0.0` ... `172.31.255.255`   (Class B, for medium networks, 16 network + 16 host)
    + `192.168.0.0` ... `192.168.255.255` (Class C, for smaller networks, 24 network + 8 host)
* Local IP
    + `127.0.0.1` ... `127.255.255.254`

# Network devices
## Repeaters 
* regenerate signals  
* allow communications across greater distances  

## Hub = multi-port Repeaters
* facilitates scaling communication between additional hosts  
* everyone receive everyone else’s data  

## Bridge 
* sit between Hub connected hosts
* have 2 ports  
* learn which hosts are on each side

## Switch = combination of Hubs and Bridges
* its primary purpose is switching (moving data within networks)  
* connects devices together in a local network
* distributes packets to its local network
* has no interface
* cannot talk directly to a network outside of its own
* facilitate communication within network  
* multiple Ports  
* learn which hosts are on each port  
* hosts on a Network share the same IP address space

## Router
* its primary purpose is Routing (moving data ...)
* connects networks together
* separates different networks with the use of multiple interfaces (an interface = a network)
* the range of possible IP addresses on one of its interfaces must not overlap with the range of its other interfaces
* the internet behaves like a router
* facilitate communication between networks  
* provides a traffic control point (security, filtering, redirecting)  
* learns which networks it is attached to  
* know as Routes - Stored in Routing Table  

### Routing Table 
* all networks a Router knows about  
* has IP address in the Networks they are attached to   
* creates the Hierarchy in Network and the entire Internet  
* **Gateway** - each host’s way out of their local Network  
* **Routing table** is stored in a router / network host, lists the routes to particular network destinations. 
* **A route** = 2 fields = the destination of outbound packets + the next hop of the packets.
* **Destination** a network address, the end target of the packets of the host.  
* **The destination default = The route of default  =** `0.0.0.0/0` a network address, takes effect when no other route is available for an IP destination. Uses the next hop address to send the packets without a specific destination. Sends the packets to the first network address it encounters. Matches any network.  
* **Next hop** a network address, the next router interface / inernet inerface on the packet's way. Every router maintains its routing table with a next hop address.  
* A destination address of 122.3.5.3/24 sends the packets to the network 122.3.5.0.

# Solution
## Level 1
`104.99.23.0` A1 min    
`104.99.23.255` A1 max  
`104.99.23.0` != A1, the first number in the range of hosts i sused fot the network, it cannot be used by a host  
`104.99.23.255` != A1, it is the broadcast address  
`104.99.23.12` != A1, it is already used    
  
`211.191.0.0` D1 min  
`211.191.255.255` D2 max
`211.191.0.0` != D1  
`211.191.255.255` != D1   
`211.191.129.75` != D1  
<img src="https://github.com/akostrik/net_practice/assets/22834202/429cb593-9681-44fd-bed8-f5629d8e2100" width="700" height="400">  

## Level 2
B1: `255.255.255.224`, because B and A are on the same private network
  
`11000000.10101000.00111011.110+00000` (`255.255.255.224`) A1 min  
`11000000.10101000.00111011.110+11111` (`192.168.118.223`) A2 max   
`11000000.10101000.00111011.110+00000` (`255.255.255.224`) != A2  
`11000000.10101000.00111011.110+11111` (`192.168.118.223`) != A2  
`11000000.10101000.00111011.110+11110` (`192.168.118.222`) != A2  
  
C1, D1: any two address, where 
- the first 30 bits are identical for D and C
- the last 2 bits are not `11`, nor `00`
- the two address are nor identical
`11111111.11111111.11111111.111111+00` = `255.255.255.252` =`/30`  

<img src="https://github.com/akostrik/net_practice/assets/22834202/5a34deda-b8a4-4701-925d-74a5bbe1add3" width="700" height="400">  

## Level 3     
`01101000.11000110.01000010.1+0000000` (`104.198.132.128`) A1, B, C1 min $\textsf{\color{red}(проверить)}$  
`01101000.11000110.01000010.1+1111111` (`104.198.132.255`) A1, B, C1 max  
`01101000.11000110.01000010.1+0000000` (`104.198.132.128`) != A1, B, C1  
`01101000.11000110.01000010.1+1111111` (`104.198.132.255`) != A1, B, C1  
A1 != B  
A1 != C1  
B != C  
`11111111.11111111.11111111.1+0000000` (`255.255.255.128`) mask
<img src="https://github.com/akostrik/net_practice/assets/22834202/c7741926-8cf2-4387-abff-9ab43eb73477" width="700" height="550">  

## Level 4
`01000101.00100000.01110110.10+000100` (`69.32.118.132`) A1  
`11111111.11111111.11111111.11+000000` (`255.255.255.192`) we are free to choose a mask  
`01000101.00100000.01110110.10+000000` (`69.32.118.128`) B1, R min, because B1, R1, A1 are in the same network   
`01000101.00100000.01110110.10+111111` (`69.32.118.191`) B1, R max, excluding ...

R2, R3: we did not interact with them

<img src="https://github.com/akostrik/net_practice/assets/22834202/e0e2e50c-1bfe-4f2c-ad24-6d9559294bb0" width="700" height="550">  

## Level 5

|A->R `17.33.126.126`:    |B->R `17.33.126.126`: $\textsf{\color{red}(?)}$    |A->B `170.242.21.253`:                            |
|:------------------------|:--------------------------------------------------|:-------------------------------------------------|
|                         |B: dest. does not match any interface, rout. table |A: dest. does not match any interface, rout. table|
|A: send to A1            |B: send to gateway `170.242.21.254` through B1     |A: send to gateway `17.33.126.126` through A1 |
|                         |                                                   |R: accepted                                       |
|                         |                                                   |R: send to R2                                     |
|R: accepted              |R: packet                                          |B: accepted                                       |
|**R->A `17.33.126.125`:**|**R-> B `170.242.21.253`:**                        |**B->A `17.33.126.125`:**                         |
|                         |                                                   |B: dest. does not match any interface, rout. table|
|R: send to R1            |R: send to R2                                      |B: send to gateway `170.242.21.254` through B1    | 
|                         |                                                   |R: accepted                                       |
|                         |                                                   |R: send to R1                                     |
|A: accepted              |B:  accepted                                       |A: accepted                                       | 

A: only has 1 route through which it can send its packets, the destination default will send the packets to the only path available, no use to specify a destination. 

`11111111.11111111.11+000000.00000000` (`255.255.192.0`)  
`10101010.11110010.00+010101.11111101` (`170.242.21.253`)   
`10101010.11110010.00+010101.11111110` (`170.242.21.254`)  

`11111111.11111111.11111111.1+0000000` (`255.255.255.128`)  
`00010001.00100001.01111110.0+1111101` (`17.33.126.125`)  
`00010001.00100001.01111110.0+1111110` (`17.33.126.126`)  

<img src="https://github.com/akostrik/net_practice/assets/22834202/8abba568-5c19-4f2d-bb51-c5619502fe9b" width="700" height="550">  

## Level 6
Network A1 + R1 + S:  
`11111111.11111111.11111111.1+0000000` (`255.255.255.128`) mask  
`01011001.01011100.11110001.1+0000000` (`89.92.241.128`) the network address of A, internet sends to `89.92.241.228/25`  
`01011001.01011100.11110001.1+0000001` (`89.92.241.129`) min host address  
`01011001.01011100.11110001.1+1111110` (`89.92.241.254`) max host address  
`01011001.01011100.11110001.1+1100011` (`89.92.241.227`) A1  
`01011001.01011100.11110001.1+1100100` (`89.92.241.228`) R1  

Network R2 + Internet:  
`11111111.11111111.11111111.1111+0000` (`255.255.255.240`) mask  
`10100011.10101100.11111010.0000+1100` (`163.172.250.12`) R2  
`00001010.00000000.00000000.00000000` (`10.0.0.0`) table R    
`10100011.10101100.11111010.00000001` (`163.172.250.1`) table R   
  
Network Internet:  
`10100011.10101100.11111010.00000001` (`163.172.250.12`) table I, the next hop of the internet  

A1 -> Somewhere on the Net (8.8.8.8)  
A: dest. does not match any interface, table 0.0.0.0/0 -> to gateway 89.92.241.228 through A1  
S: pass to all connections  
R: accepted  
R: dest. does not match any interface, table 0.0.0.0/0 -> to gateway 163.172.250.1 through R2  
I: accepted, destination IP reached  
A: loop detected (?)  
  
Somewhere on the Net -> A1 (89.92.241.227)  
I: dest. does not match any interface, routing table 89.92.241.228/25 -> to gateway 163.172.250.12 through I1  
R: accepted  
R: send to R1  
S: pass to all connections  
R: loop detected (?)  
A: accepted  
  
<img src="https://github.com/akostrik/net_practice/assets/22834202/429c209c-84af-45b1-8211-724326f91bb5" width="720" height="600">  


