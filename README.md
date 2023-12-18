_42 School project, level 4_

# TCP/IP addressing
_Маска подсети_ битовая маска для определения по IP-адресу адреса подсети и адреса узла (хоста, компьютера, устройства) этой подсети.  
В отличие от IP-адреса маска подсети не является частью IP-пакета.  
Благодаря маске можно узнать, какая часть IP-адреса узла сети относится к адресу сети, а какая — к адресу самого узла в этой сети.  


Например, узел с IP-адресом 12.34.56.78 и маской подсети 255.255.255.0, с длиной префикса 24 бита (/24), находится в сети 12.34.56.0.

В случае адресации IPv6 адрес 2001:0DB8:1:0:6C1F:A78A:3CB5:1ADD с длиной префикса 32 бита (/32) находится в сети 2001:0DB8::/32.

Другой вариант определения — это определение подсети IP-адресов. Например, с помощью маски подсети можно сказать, что один диапазон IP-адресов будет в одной подсети, а другой диапазон соответственно в другой подсети.

Чтобы получить адрес сети, зная IP-адрес и маску подсети, необходимо применить к ним операцию поразрядной конъюнкции (побитовое И). Например

IP-адрес:       11000000 10101000 00000001 00000010 (192.168.1.2)
Маска подсети:  11111111 11111111 11111110 00000000 (255.255.254.0)
Адрес сети:     11000000 10101000 00000000 00000000 (192.168.0.0)
часть маски, определяющая адрес сети и состоящая из единиц;
адрес сети, который определяется маской подсети;
диапазон адресов устройств в этой сети.

<pre>IP-адрес:  <span style="background-color:Yellow">11000000 10101000 0000000</span><span style="background-color:Salmon">1 00000010</span> (192.168.1.2)
Маска подсети:  <span style="background-color:PaleGreen">11111111 11111111 1111111</span>0 00000000 (255.255.254.0)
Адрес сети:     <span style="background-color:Yellow">11000000 10101000 0000000</span>0 00000000 (192.168.0.0)
</pre>

<span style="color:blue">some *This is Blue italic.* text</span>

<span style="color:red">some **This is Red Bold.** text</span>


<style>
r { color: Red }
o { color: Orange }
g { color: Green }
</style>

# TODOs:

- <r>TODO:</r> Important thing to do
- <o>TODO:</o> Less important thing to do
- <g>DONE:</g> Breath deeply and improve karma

// resets
s { text-decoration:none; } //strike-through
em { font-style: normal; font-weight: bold; } //italic emphasis

// colors
s { color: green }
em { color: blue }

~~This is green~~

_this is blue_

<font color='red'>test blue color font</font>

U+1F534

$${\color{red}Red}$$

