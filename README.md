_42 School project, level 4_

**Узел** хост, компьютер, устройство  

**Transmission Control Protocol (TCP)** a communications standard that enables application programs and devices to exchange messages over a network. Is used to send packets across the internet.  
1) TCP establishes a connection between a source and its destination, which remains active until communication begins
2) TCP breaks data into smaller packets, while ensuring end-to-end delivery  

# Variable-length subnet masking (VLSM)

**Маска подсети** определяет по IP-адресу адрес подсети и адрес узла, не является частью IP-пакета (в отличие от IP-адреса)  

| **IP addresse = network prefix + host identifier:** | **$\textsf{\color{blue}11000000 10101000 0000000}$ $\textsf{\color{green}1 00000010}$** | **192.168.1.2**    |
|:--------------------|:----------------------------------------------------------------------------------------|:-------------------|
| **Маска подсети:**  | **$\textsf{\color{blue}11111111 11111111 1111111}$ $\textsf{\color{black}0 00000000}$** | **255.255.254.0**  |
| **$\textsf{\color{blue}Адрес сети}$:**     | **$\textsf{\color{blue}11000000 10101000 0000000}$ $\textsf{\color{blue}0 00000000}$**  | **192.168.0.0**    |

$\textsf{\color{green}диапазон адресов устройств в этой сети}$  

**Classless Inter-Domain Routing (CIDR)** a method for allocating IP addresses and for IP routing (slows the growth of routing tables on routers across the Internet, slows the exhaustion of IPv4 addresses).

IPv4: network prefix of 8 / 16 / 24 bits   
IPv6: interface identifier of 64 bits + ... (smaller subnets are never allocated to end users)  

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
| /8      | 255.0.0.0       | 16 777 216    | 
| /0      | 0.0.0.0         | 4 294 967 296 | entire IPv4 Internet


# Client IP addresses
* Client ip do not overlap  
* Private IP  
Cannot be used to access the Internet, remains only in the local network, never leaves the LAN.  
Reserved by the Internet Assigned Numbers Authority (IANA).  
    + `10.0.0.0` ... `10.255.255.255`     (Class A, for large networks,   8 network + 24 hosts)
    + `172.16.0.0` ... `172.31.255.255`   (Class B, for medium networks, 16 network + 16 hosts)
    + `192.168.0.0` ... `192.168.255.255` (Class C, for smaller networks, 24 network + 8 host)
* Local IP
    + from `127.0.0.1` to `127.255.255.254`

# A switch
* connects devices together in a single network
* distributes packets to its local network
* has no interface
* cannot talk directly to a network outside of its own

# A router
* connects networks together
* separates different networks
* has an interface for each network
* the range of possible IP addresses on one of its interfaces must not overlap with the range of its other interfaces
  
## Route table 
**Routing table** is stored in a router / network host, lists the routes to particular network destinations. 
**Destination** a network address, the end target of the packets of the host.  
**The route of default (0.0.0.0/0)** a network address, takes effect when no other route is available for an IP destination address. Uses the next hop address to send the packets without a specific destination. Matches any network.  
**Next hop** a network address, the next router on the packet's way. Every router maintains its routing table with a next hop address.  

# Solution
## Level 1:
A1: anything in [`104.96.23.0`;`104.96.23.255`] excluding `104.96.23.0` (the first number in the range of hosts = the network, cannot be used by a host), `104.96.23.255` (the last number = the broadcast address), `104.96.23.12` (already used)  
D1: Anything in [`211.191.0.0`;`211.191.255.255`], excluding `211.191.0.0`, `211.191.255.255`, `211.191.89.75`  
<img src="https://github.com/akostrik/net_practice/assets/22834202/429cb593-9681-44fd-bed8-f5629d8e2100" width="700" height="400">  

## Level 2:  
<img src="https://github.com/akostrik/net_practice/assets/22834202/5a34deda-b8a4-4701-925d-74a5bbe1add3" width="700" height="400">  

## Level 3:  
<img src="https://github.com/akostrik/net_practice/assets/22834202/c7741926-8cf2-4387-abff-9ab43eb73477" width="700" height="550">  

## Level 4:  
<img src="https://github.com/akostrik/net_practice/assets/22834202/e0e2e50c-1bfe-4f2c-ad24-6d9559294bb0" width="700" height="550">  

## Level 5:  

|A->R (17.33.126.126)    |B->R (17.33.126.126)                               |A->B (170.242.21.253)                             |
|:-----------------------|:--------------------------------------------------|:-------------------------------------------------|
|                        |B: dest. does not match any interface, rout. table |A: dest. does not match any interface, rout. table|
|A: send to A1           |$\textsf{\color{red}B: send to gateway 170.242.21.254 through intrf B1 (?)}$ |A: send to gateway 17.33.126.126 through intrf A1 |
|                        |                                                   |R: packet accepted                                |
|                        |                                                   |R: send to R2                                     |
|R: packet accepted      |R: packet accepted                                 |B: packet accepted                                |
|**R->A (17.33.126.125)**|**R-> B (170.242.21.253)**                         |**B->A (17.33.126.125)**                          |
|                        |                                                   |B: dest. does not match any interface, rout. table|
|R: send to R1           |R: send to R2                                      |B: send to gateway 170.242.21.254 through intrf B1| 
|                        |                                                   |R: packet accepted                                |
|                        |                                                   |R: send to R1                                     |
|A: packet accepted      |B: packet accepted                                 |A: packet accepted                                | 

<img src="https://github.com/akostrik/net_practice/assets/22834202/8abba568-5c19-4f2d-bb51-c5619502fe9b" width="700" height="550">  


