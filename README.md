_42 School project, level 4_

# TCP/IP addressing
_Маска подсети_ битовая маска для определения по IP-адресу адреса подсети и адреса узла (хоста, компьютера, устройства).  
В отличие от IP-адреса, маска подсети не является частью IP-пакета.  

| **IP-адрес:**       | **$\textsf{\color{blue}11000000 10101000 0000000}$ $\textsf{\color{green}1 00000010}$** | **192.168.1.2**    |     |
|:--------------------|:----------------------------------------------------------------------------------------|:-------------------|-----|
| **Маска подсети:**  | **$\textsf{\color{blue}11111111 11111111 1111111}$ $\textsf{\color{black}0 00000000}$** | **255.255.254.0**  | /23 |
| **Адрес сети:**     | **$\textsf{\color{blue}11000000 10101000 0000000}$ $\textsf{\color{blue}0 00000000}$**  | **192.168.0.0**    |     |

$\textsf{\color{blue}адрес сети}$  
$\textsf{\color{green}диапазон адресов устройств в этой сети}$  

# Configuration
## Check CIDR or Subnet mask
## Check client ip 
- Client ip do not overlap to other  
- Private ip do not access internet
-- from `10.0.0.0` to `10.255.255.255`
-- from `172.16.0.0` to `172.31.255.255`
-- from `192.168.0.0` to `192.168.255.255`
- Do not set local ip
-- from `127.0.0.1` to `127.255.255.254`
## Calculate available ip range in subnet

- Switch connects clients in same subnet  
- Router connects subnets
- Route table is configured from source ip to destination with CIDR (0.0.0.0/0)




![Screenshot from 2023-12-18 15-41-54](https://github.com/akostrik/net_practice/assets/22834202/429cb593-9681-44fd-bed8-f5629d8e2100)
