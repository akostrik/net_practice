# Vocabulary

## The Open Systems Interconnection model (OSI)
Сетевая модель стека сетевых протоколов OSI/ISO, взаимодействие сетевых устройств, передача двоичных данных от одного устройства к другому.  
Layers:
1) Physical
2) Data link (канальный): взаимодействие сетей на физическом уровне
3) Network: определение пути передачи данных
4) Transport: надёжная передача данных (протоколы ATP, CUDP, DCCP, FCP, IL, NBF, NCP, SCTP, SPX, SST, TCP, UDP)
5) Session: поддержание сеанса, позволяя приложениям взаимодействовать длительное время (протоколы H.245, ISO-SP, iSNS, L2F, L2TP, NetBIOS, PAP, PPTP, RPC, RTCP, SMPP, SCP, ZIP, SDP)
6) Presentation: преобразование протоколов и кодирование/декодирование данных (протоколы AFP, ICA, LPP, NCP, NDR, XDR, X.25 PAD)
7) Application: взаимодействие пользовательских приложений с сетью (протолоклы RDP, HTTP, SMTP, SNMP, POP3, FTP, XMPP, OSCAR, Modbus, SIP, TELNET)

## Variable-length subnet masking (VLSM)
**Маска подсети** определяет по IP-адресу адрес подсети и адрес узла.  
Не является частью IP-пакета (в отличие от IP-адреса). Например:  
`network prefix     + host identifier`   
`11000000.10101000.0000000+1.00000010` = `192.168.1.2`  
`11111111.11111111.1111111+0.00000000` = `255.255.254.0` mask  
`11000000.10101000.0000000+0.00000000` = `192.168.0.0` **network address**  

Calculator of mask ranges https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=28&cip=93.198.14.2&ctype=ipv4&printit=0&x=97&y=13

## IPv4 vs IPv6  
IPv4: network prefix  8 / 16 / 24 bits    
IPv6: interface identifier 64 bits  

## Classless Inter-Domain Routing (CIDR)
IPv4 CIDR blocks:  
| Netmask                 | nb address    | nb hosts  
|:------------------------|--------------:|-------:
| `/32`=`255.255.255.255` | 1             | accessible by explicit routing rules (single-host network) 
| `/31`=`255.255.255.254` | 2             | no available host addresses (unusable)
| `/30`=`255.255.255.252` | 4             | 2     
| `/29`=`255.255.255.248` | 8             | 6     
| `/28`=`255.255.255.240` | 16            | 14    
| `/27`=`255.255.255.224` | 32            | 30    
| `/26`=`255.255.255.192` | 64            | 62    
| `/25`=`255.255.255.128` | 128           | 126   
| `/24`=`255.255.255.0`   | 256           | 254   
| `/23`=`255.255.254.0`   | 512           | 510      
| `/22`=`255.255.252.0`   | 1 024         | 1 022      
| `/21`=`255.255.248.0`   | 2 048         | 2 046  
| `/20`=`255.255.240.0`   | 4 096         | 4 094  
| `/19`=`255.255.224.0`   | 8 192         | 8 190
| `/18`=`255.255.192.0`   | 16 384        | 16 382 
| `/17`=`255.255.128.0`   | 32 768        | 32 766  
| `/16`=`255.255.0.0`     | 65 536        | 65 534 
| `/8` =`255.0.0.0`       | 16 777 216    | 16 777 214
| `/0` =`0.0.0.0`         | 4 294 967 296 | entire IPv4 Internet

## Client IP addresses
Client IP do not overlap  
* **Private IP** cannot be used to access the Internet, remains in the local network, never leaves the LAN.  
If an interface is connected directly / indirectly to the internet, it cannot have an IP address in the private IP.
    + `10.0.0.0` ... `10.255.255.255`     (Class A, for large networks,   8 network + 24 host)
    + `172.16.0.0` ... `172.31.255.255`   (Class B, for medium networks, 16 network + 16 host)
    + `192.168.0.0` ... `192.168.255.255` (Class C, for smaller networks, 24 network + 8 host)
* **Local IP**
    + `127.0.0.1` ... `127.255.255.254`

## Repeater = повторитель = коаксиальный повторитель
* 1 OSI level
* regenerate signals  
* для увеличения расстояния сетевого соединения, организации двух ветвей
* меньшее задержка, чем с hub, т.к. два разъема для кабеля, нет необходимости концентрировать сигнал и распространять на остальные выходы

## Hub = multi-port repeater = сетевой концентратор = многопортовый повторитель
* 1 OSI level
* everyone receives everyone else’s data
* вытеснены сетевыми коммутаторами
 
## Bridge 
* 2 OSI level
* 2 ports between рub connected hosts

## Switch = сетевой коммутатор
* 2 OSI level 
* connects devices together in a local network, moving data within networks, distributes packets to its local network
* передаёт данные только непосредственно получателю
* no interface
* multiple ports
* cannot talk directly to a network outside of its own
* it is a combination of hubs and bridges
* Хранит таблицу коммутации, в которой указывается соответствие узла порту.
     + Режим обучения: при включении коммутатора, таблица пуста, поступающие на какой-либо порт данные передаются на все остальные порты. Коммутатор анализирует фреймы (кадры) и, определив MAC-адрес отправителя, заносит его в таблицу. Так коммутатор строит таблицу активных MAC-адресов.
     + Если на порт поступит кадр, предназначенный для хоста, MAC-адрес которого уже есть в таблице, то этот кадр будет передан только туда
     + Если MAC-адрес получателя не ассоциирован с каким-либо портом коммутатора, то кадр будет отправлен на все порты. 

## Network host
* a device connected to a network, which sends or receive traffic, it can be client or server
* when a host receives a packet:
    |accordigly to the routing table, the destination is ...|the packet goes to ...
    |:---------------------|--------------------------------------------
    |on the local network| the host directly
    |not on the local network| a local router
    |unknown, there is a default route| ?
    |unknown, there isn’t a default route| ?

## Router = маршрутизатор 
* 3 OSI level
* связывает разнородные сети различных архитектур
* separates networks with the use of interfaces (an interface <-> a network)
* пересылает пакеты между сегментами сети на основе правил и таблиц маршрутизации
* the range of possible IP addresses on one interface must not overlap with the range of its other interfaces
* a destination 122.3.5.3/24 sends the packets to the network 122.3.5.0
* here: the internet behaves like a router
* a traffic control point (security, filtering, redirecting)  
* when a router receives a packet:
    |accordigly to the routing table, the destination is ...|the packet goes to ...
    |:---------------------|--------------------------------------------
    |on an attached network| the host directly
    |not an attached network| another router
    |unknown, there is a default route| the default route
    |unknown, there isn’t a default route| is dropped (the source IP is informed)
* stores routes in its routing table
 
## Routing Table 
* every router / network host stores routing table
* contains information of how to reach systems that are attached to local and remote networks, lists the routes to particular network destinations, contains all networks the router knows about
* is generated from local configuration information and from routing protocol messages exchanged with neighboring systems
* has IP address
* **A route** = 2 fields = the destination + the next hop
* **Destination address** the end target of the packets
* **Default destination address = default route address =** `0.0.0.0/0` takes effect when no other route is available for an IP destination. Sends the packets to the first network address it encounters (or to the next hop address ?). Matches any network.
* **Next hop address** the next router / inetrnet inerface on the packet's way
* **Gateway** a host’s way out of its local network  

# Level 1 solution
A1:
`01101000.01100011.00010111.00000001` = `104.99.23.0` network address, cannot be used by a host  
`01101000.01100011.00010111.00000001` = `104.99.23.1` min host address   
`01101000.01100011.00010111.00001100` = `104.99.23.12` already used    
`01101000.01100011.00010111.11111110` = `104.99.23.254` max host address  
`01101000.01100011.00010111.11111111` = `104.99.23.255` the broadcast address, cannot be used by a host  

D1, D2:
`11010011.10111111.00000000.00000001` = `211.191.0.1` min  
`11010011.10111111.11111111.11111110` = `211.191.255.254` max

<img src="https://github.com/akostrik/net_practice/assets/22834202/429cb593-9681-44fd-bed8-f5629d8e2100" width="700" height="400">  

# Level 2 solution
B1:  
`11111111.11111111.11111111.111_00000` = `255.255.255.224` = `/27` mask (B and A are on the same network)   
`11000000.10101000.00111011.110_00001` = `192.168.59.193` A1 min   
`11000000.10101000.00111011.110_11110` = `192.168.59.222` A2 max   
  
C1, D1:  
`11111111.11111111.11111111.111111_00` (255.255.255.252`, `/30`) mask   
`********.********.********.******_01`  C
`********.********.********.******_10`  D
- the first 30 bits are identical    
- the last 2 bits are not `11`, nor `00`  

<img src="https://github.com/akostrik/net_practice/assets/22834202/5a34deda-b8a4-4701-925d-74a5bbe1add3" width="700" height="400">  

# Level 3 solution
`11111111.11111111.11111111.1_0000000` = `255.255.255.128` = `/27` mask
`01101000.11000110.01000010.1_0000001` = `104.198.132.128` min (?) 
`01101000.11000110.01000010.1_1111110` = `104.198.132.255` max  

<img src="https://github.com/akostrik/net_practice/assets/22834202/c7741926-8cf2-4387-abff-9ab43eb73477" width="700" height="550">  

# Level 4 solution
`11111111.11111111.11111111.11_000000` = `255.255.255.192` = `/26` we are free to choose a mask  
`01000101.00100000.01110110.10_000001` = `69.32.118.128` B1 min, R min (B1, R1, A1 are in the same network)  
`01000101.00100000.01110110.10_000100` = `69.32.118.132` A1  
`01000101.00100000.01110110.10_111110` = `69.32.118.191` B1 max, R max

R2, R3: we did not interact with them

<img src="https://github.com/akostrik/net_practice/assets/22834202/e0e2e50c-1bfe-4f2c-ad24-6d9559294bb0" width="700" height="550">  

# Level 5 solution

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

`11111111.11111111.11_000000.00000000` = `255.255.192.0` = `/26` mask  
`10101010.11110010.00_010101.11111101` = `170.242.21.253` min  
`10101010.11110010.00_010101.11111110` = `170.242.21.254` max  

`11111111.11111111.11111111.1_0000000` = `255.255.255.128` = `/25` mask  
`00010001.00100001.01111110.0_1111101` = `17.33.126.125` min  
`00010001.00100001.01111110.0_1111110` = `17.33.126.126` max  

<img src="https://github.com/akostrik/net_practice/assets/22834202/8abba568-5c19-4f2d-bb51-c5619502fe9b" width="700" height="550">  

# Level 6 solution
Network A1 R1 S:  
`11111111.11111111.11111111.1_0000000` = `255.255.255.128` = `/27` mask  
`01011001.01011100.11110001.1_0000000` = `89.92.241.128` the network address of A, internet sends to `89.92.241.228/25`  
`01011001.01011100.11110001.1_0000001` = `89.92.241.129` min  
`01011001.01011100.11110001.1_1100011` = `89.92.241.227` A1  
`01011001.01011100.11110001.1_1100100` = `89.92.241.228` R1  
`01011001.01011100.11110001.1_1111110` = `89.92.241.254` max  

Network R2 I:  
`11111111.11111111.11111111.1111_0000` = `255.255.255.240` = `/28` mask  
`10100011.10101100.11111010.0000_1100` = `163.172.250.12`R2  
`00001010.00000000.00000000.0000_0000` = `10.0.0.0` dest R    
`10100011.10101100.11111010.0000_0001` = `163.172.250.1` dest R   
  
Network I:  
`10100011.10101100.11111010.00000001` (`163.172.250.12`) table I, the next hop of the internet  

|A1 -> Somewhere on the Net (8.8.8.8):  
|:----------------------------------------
|A: dest. does not match any interface, table 0.0.0.0/0 -> to gateway 89.92.241.228 through A1  
|S: pass to all connections  
|R: accepted  
|R: dest. does not match any interface, table 0.0.0.0/0 -> to gateway 163.172.250.1 through R2 (почему не R1?)   
|I: accepted, destination IP reached  
|A: loop detected (потому что S: pass to all connection ?)  
|**Somewhere on the Net -> A1 (89.92.241.227):**  
|I: dest. does not match any interface, routing table 89.92.241.228/25 -> to gateway 163.172.250.12 through I1  
|R: accepted  
|R: send to R1 (почему не R2?)  
|S: pass to all connections  
|R: loop detected (потому что S: pass to all connections ?)  
|A: accepted  
  
<img src="https://github.com/akostrik/net_practice/assets/22834202/429c209c-84af-45b1-8211-724326f91bb5" width="720" height="600">  

# Level 7 solution
We need addresses for 3 networks and the ranges of networks must not overlap =>  
We split the last byte into 64 ranges by /30.  
We use the following 3 ranges:   
  
Network A R1:  
`11111111.11111111.11111111.111111_00` = `255.255.255.252` = `/30` mask  
`01100000.11000110.00001110.000000_01` = `96.198.14.1` min  
`01100000.11000110.00001110.000000_10` = `96.198.14.2` max  

Network R1 R2:    
`11111111.11111111.11111111.111111_00` = `255.255.255.252` = `/30` mask  
`01100000.11000110.00001110.111111_01` = `96.198.14.253` min  
`01100000.11000110.00001110.111111_10` = `96.198.14.254` max    

Network R2 C:  
`11111111.11111111.11111111.111111_00` = `255.255.255.252` = `/30` mask  
`01100000.11000110.00001110.000001_01` = `96.198.14.5` min   
`01100000.11000110.00001110.000001_10` = `96.198.14.6` max   
  
NB: /24  gives 1 range, doesn't suit here, `96.198.14.1` and `96.198.14.254` would be in [`93.198.14.0`, `93.198.14.255`]   
NB: /26 gives 4 ranges  
NB: /28 gives 16 ranges  
NB: /30 gives 64 ranges  
  
<img src="https://github.com/akostrik/net_practice/assets/22834202/3a01b40d-9b0a-41a3-8f63-2dcc8b4c499c" width="700" height="450">  

# Level 8 solution

I:  
`11111111.11111111.11111111.11_000000` = `255.255.255.192` = `/26` mask  
`10001101.11101111.11100101.00_000000` = `141.239.229.0/26` I routes these address  
`10001101.11101111.11100101.00_000001` = `141.239.229.1` I routes these address, min  
`10001101.11101111.11100101.00_111110` = `141.239.229.63` I routes these address, max  
All the receiving networks must be in this range and without overlapping.  
  
`11111111.11111111.11111111.1111_0000` = `255.255.255.240`, `/28` mask R23 R22, splits `/26` into 4 ranges:  
`10100011.10101010.11111010.0000_0001` = `163.170.250.1` not used ...  
`10100011.10101010.11111010.0000_1110` = `163.170.250.14` not used       
`10100011.10101010.11111010.0001_0001` = `163.170.250.17` network R2 C min ...  
`10100011.10101010.11111010.0001_1110` = `163.170.250.30` network R2 C max  
`10100011.10101010.11111010.0010_0001` = `163.170.250.33` network R2 D min ...  
`10100011.10101010.11111010.0010_1110` = `163.170.250.46` network R2 D max   
`10100011.10101010.11111010.0011_0001` = `163.170.250.49` network R1 R2 min ...   
`10100011.10101010.11111010.0011_1110` = `163.170.250.62` network R1 R2 max  

<img src="https://github.com/akostrik/net_practice/assets/22834202/ffa495de-52d7-4d2c-b362-a0cb2973a4a4" width="700" height="700">  

# Level 9 solution

<img src="https://github.com/akostrik/net_practice/assets/22834202/f959e183-552a-4e93-a129-90208de25709" width="700" height="600">  
