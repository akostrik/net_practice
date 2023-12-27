_42 School project, level 4_

# 1. CIDR or Subnet mask
TCP/IP addressing  
_Узел_ = хост, компьютер, устройство  
_Маска подсети_ определяет по IP-адресу адрес подсети и адрес узла. Не является частью IP-пакета (в отличие от IP-адреса).  

| **IP-адрес:**       | **$\textsf{\color{blue}11000000 10101000 0000000}$ $\textsf{\color{green}1 00000010}$** | **192.168.1.2**    |     |
|:--------------------|:----------------------------------------------------------------------------------------|:-------------------|-----|
| **Маска подсети:**  | **$\textsf{\color{blue}11111111 11111111 1111111}$ $\textsf{\color{black}0 00000000}$** | **255.255.254.0**  | /23 |
| **Адрес сети:**     | **$\textsf{\color{blue}11000000 10101000 0000000}$ $\textsf{\color{blue}0 00000000}$**  | **192.168.0.0**    |     |

$\textsf{\color{blue}адрес сети}$  
$\textsf{\color{green}диапазон адресов устройств в этой сети}$  

CIDR Sheet table
|     | Address	| Host  | Netmask
|-----|---------|-------|---------------
| /30 | 4       | 2     | 255.255.255.252
| /29 | 8       | 6     | 255.255.255.248
| /28 | 16      | 14    | 255.255.255.240
| /27 | 32      | 30    | 255.255.255.224
| /26 | 64      | 62    | 255.255.255.192
| /25 | 128     | 126   | 255.255.255.128
| /24 | 256     | 254   | 255.255.255.0
| /18 | 16384   | 16382 | 255.255.192.0
| /16 | 65536   | 65534 | 255.255.0.0


# 2. Client IP addresses
* Client ip do not overlap  
* Private IP  
Cannot be used to access the Internet, remains only in the local network, never leaves the LAN.  
Reserved by the Internet Assigned Numbers Authority (IANA).  
    + `10.0.0.0` ... `10.255.255.255`     (Class A, for large networks,   8 bits for the network + 24 for hosts)
    + `172.16.0.0` ... `172.31.255.255`   (Class B, for medium networks, 16 bits for the network + 16 for hosts)
    + `192.168.0.0` ... `192.168.255.255` (Class C, for smaller networks, 24 bits for the network + 8 for host)
* Local IP
    + from `127.0.0.1` to `127.255.255.254`

# 3. Calculate available IP range in subnet
* Switch connects clients in same subnet  
* Router connects subnets
* Route table is configured from source ip to destination with CIDR (0.0.0.0/0)




![Screenshot from 2023-12-18 15-41-54](https://github.com/akostrik/net_practice/assets/22834202/429cb593-9681-44fd-bed8-f5629d8e2100)
