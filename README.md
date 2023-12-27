_42 School project, level 4_

# TCP/IP addressing
_Маска подсети_ битовая маска для определения по IP-адресу адреса подсети и адреса узла (хоста, компьютера, устройства).  
В отличие от IP-адреса маска подсети не является частью IP-пакета.  
Узнать, какая часть IP-адреса узла сети относится к адресу сети, а какая — к адресу самого узла в этой сети.  

| IP-адрес:           | 11000000 10101000 00000001 00000010 (192.168.1.2)       |
|:--------------------|:--------------------------------------------------------|
| **Маска подсети:**  | **$\textsf{\color{green}11111111 11111111 1111111}$ 0 00000000 (255.255.254.0)**  |
| **Адрес сети:**     | 11000000 10101000 00000000 00000000 (192.168.0.0)   |

$\textsf{\color{green}часть маски, определяющая адрес сети}$  
адрес сети, который определяется маской подсети  
диапазон адресов устройств в этой сети  

$\textsf{\color{red}Red text}$

![Screenshot from 2023-12-18 15-41-54](https://github.com/akostrik/net_practice/assets/22834202/429cb593-9681-44fd-bed8-f5629d8e2100)
